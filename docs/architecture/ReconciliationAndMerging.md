# PASS Reconciliation, Dependency Impact and Approval Workflow

**Status:** Core proposed safety specification. This document is authoritative for the conceptual design.

## 1. Objectives

PASS must identify how a change to any tracked source or artifact affects the rest of the application. It must not assume that preserving a C# method is sufficient. A schema or project change may affect entity models, `DbContext`, controllers, view models, Razor/HTML, JavaScript/AJAX, routing, validation, tests, project dependencies, configuration and—in a separately selected workflow—migration or SQL scripts.

The planner must show the probable outcome before candidate code generation. No project or database mutation may occur without explicit approval by an authorized user.

## 2. Dependency graph

Represent tracked objects as graph nodes. Examples:

- Database database/schema/table/column/constraint/view.
- Entity and navigation property.
- `DbContext` and entity mapping.
- View model / DTO.
- Service and repository.
- Controller/action/route.
- Razor view (Create/Edit/Details/List/Delete) and partial/view component.
- JavaScript/TypeScript/AJAX request and response contract.
- Search, sort and pagination configuration.
- Test and fixture.
- `pass.json` setting.
- `.csproj`, package reference, MSBuild property and SDK configuration.
- Migration/model snapshot in a future migrations-first mode.
- PASS template, generator version and manifest entry.

Edges are typed and directional, for example: `maps-to`, `generates`, `consumes`, `renders`, `calls`, `configured-by`, `builds-with`, `tests` and `baseline-of`. Maintain reverse indexes so a change to any node can find its dependents. Reverse lookup is for impact discovery; it does not mean every edge permits a write in both directions.

## 3. Example: a database column is added

Suppose `dbo.Customer.Email` is added in the live database in database-first mode. The planner should investigate the following dependency chain, as applicable:

1. Database schema snapshot/fingerprint changes.
2. Generated entity property and data type/nullability mapping.
3. `DbContext` mapping or configuration (only if needed).
4. View models/DTOs and mapping profiles.
5. Controller/service binding, validation and query projections.
6. Razor Create/Edit forms and List/Details displays according to profile and user intent.
7. JavaScript/AJAX payloads, grid column definitions and client validation where they consume that field.
8. Search/sort allowlists and query specifications if the feature is enabled for that property.
9. Unit/integration/snapshot tests and seed fixtures.
10. Project/package files only if a genuinely required dependency changes; do not alter them speculatively.
11. Database DDL is not generated to recreate a change that already exists in the authoritative database. No database write occurs.
12. Existing migrations/model snapshot are checked for drift, but do not override database-first authority.

Not every item must be changed for every column. The planner must state why each artifact is included, excluded or requires review.

## 4. Change in the reverse direction

A change to a controller, Razor view, JavaScript contract, entity, `DbContext`, `pass.json` or `.csproj` must also trigger impact discovery:

For modern ASP.NET Core projects, use `.csproj`/MSBuild as the project-definition artifact. `project.json` is a legacy format and is not part of the initial target. If a legacy project is encountered, report it as a compatibility/adoption issue rather than silently converting it.

- Controller route/action change: inspect route consumers, links, scripts, API clients and tests. Do not change the database merely because a controller changed.
- Razor view change: inspect its view model, referenced properties, forms, validation and client scripts. Do not regenerate the entity unless the model is inconsistent and the selected source-of-truth rules justify a proposal.
- Entity property change: compare against live schema and mapping. In database-first mode, a schema-incompatible manual property is a conflict or explicit customization, not authority to change the database.
- `DbContext` mapping change: inspect entity/schema correspondence and query behaviour; report disagreements.
- `pass.json` feature change: identify all modules that consume the setting, associated templates, dependencies, tests and generated artifacts. A project-wide change must preview every affected module.
- `.csproj` or package change: inspect generators and code that depend on package/API versions; do not silently add, remove or upgrade a package.
- Test change: identify the behaviour/artifact under test; tests are evidence and should not be rewritten just to make a failing generation pass.

The graph must identify all impacted nodes in both discovery directions while the source-of-truth policy controls which transformations are valid.

## 5. Change classes and proposed action types

For each impacted node, assign one of:

- `CreateCandidate`
- `UpdateCandidate`
- `DeleteCandidate` (high risk; explicit explanation and approval required)
- `Preserve`
- `ReviewRequired`
- `NoChange`
- `Unsupported`
- `Conflict`

A planner must not silently interpret missing files, manually deleted code or unknown ownership as permission to recreate or delete content.

## 6. Read-only plan before code generation

`plan` must not generate source code, write to the target project, update `pass.json`, alter `.csproj`, create migration files, modify the database or execute scripts. It analyses inputs and produces a probable-outcome report containing:

- Unique plan ID and digest.
- Target solution/project and selected source-of-truth mode.
- Input fingerprints: database schema, project files, `pass.json`, manifest, generator/template versions.
- User-requested change and discovered changes.
- Affected dependency graph and artifact paths.
- Proposed operation for every artifact and its reason.
- Expected package/configuration/project changes.
- Expected build/test work.
- Database implications and explicit statement that no database write is included by default.
- Assumptions, unsupported items, warnings, conflicts and risks.
- Probable outcome and uncertainty level.
- Backup and rollback feasibility.

The report must be shown before any candidate code generation. If a report is exported to a file, that file write is itself an operation and must be explicitly requested/approved.

## 7. Two explicit approval gates

### Gate 1 — approve candidate preparation

An authorized user approves the specific plan ID/digest to permit PASS to generate candidate files in an isolated staging workspace. This is not approval to modify the target project or database.

**Authorization meaning:** in an individual local project, the approver must be the project owner/developer operating an account with permission to modify the target. In a team or enterprise project, authorization must follow the repository/project approval policy (for example, a designated maintainer or protected CI environment reviewer). An interactive confirmation prompt is necessary but must not override a stricter project policy. The plan itself cannot nominate or authorize its own approver.

### Candidate review

PASS displays the exact candidate diff, file list, validation results and updated risk report. If preparation reveals new dependencies, changes or conflicts that were not in the plan, invalidate the plan and create a revised plan. Never expand the approved scope silently.

### Gate 2 — approve application

An authorized user separately approves the exact candidate hashes and operation list. Only then may PASS apply the change transaction. The approval is scoped to that plan; it is not standing permission for future runs.

A generic `--yes` switch must not bypass these gates. Non-interactive/CI operation requires a trusted approval record or protected environment gate bound to the plan digest and the exact candidate operations.

## 8. Conflict policy

Stop and report the affected operation if:

- A generated file has unclassified or conflicting developer modifications.
- A property has an incompatible manual type or mapping.
- A database rename cannot be distinguished from a drop/add safely.
- Database schema and EF model/migration state disagree beyond the selected authority policy.
- An operation would delete or materially alter developer-owned content.
- The planner cannot determine the affected dependency set with sufficient confidence.
- Required provider/template support is missing.
- A plan input changes after approval.

The report should include evidence, affected files, conflict type, possible resolutions and the consequences of each. The user must decide. Do not pick a destructive option automatically.

## 9. Transaction and rollback

Before application, snapshot the original bytes and hashes of every file to be changed and prepare candidate files outside the target. Maintain a transaction journal. Apply files through a controlled sequence with atomic replacement where supported. Validate the resulting project.

If validation fails, PASS may automatically restore the exact pre-transaction state only if that rollback was explicitly included in the approved plan. Otherwise preserve the backup and stop for a new rollback plan and approval. A manual rollback is itself a planned mutation and requires explicit approval.

Database changes are not part of the ordinary file transaction. SQL scripts or migrations are separate privileged artifacts and execution requires a separate database change-control process.

## 10. Stale plan invalidation

Before prepare and before apply, recompute the relevant input fingerprints. If the database schema, current file, configuration, package graph, baseline, generator or template version has changed, reject the stale plan and require re-analysis. Do not apply an old diff to a changed project.

## 11. Determinism and idempotency

For identical database snapshot, project files, configuration, manifest, generator version, template version and dependency state, the same plan and candidate output should be produced. Re-running an already applied operation with unchanged inputs should result in `NoChange`, not duplicate properties/actions/files.

## 12. Language-specific strategy

- **C#:** Roslyn syntax and semantic analysis for supported transformations. Prefer partial classes and supported EF Core extension hooks over merging arbitrary user methods.
- **Razor:** Razor-aware templates and component/partial boundaries; do not treat `.cshtml` as an ordinary C# syntax tree.
- **JavaScript/TypeScript/CSS/HTML:** preserve separate user-owned files and use explicit extension points or language-specific parsers where supported.
- **JSON/XML/MSBuild:** parse structurally; preserve unknown/user settings or stop if safe merge is not possible.
- **SQL:** generate reviewable scripts; never execute them as an incidental side effect of application scaffolding.

## 13. Observability

Plans and transactions should record operator/approver identity, timestamps, plan digest, candidate hashes, file operations, validation results, warnings, conflicts and rollback status. Do not log credentials, secret values or sensitive database contents.
