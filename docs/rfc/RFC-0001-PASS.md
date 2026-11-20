# RFC-0001: Project Aware Smart Scaffolder (PASS)

- **Status:** Draft — open for conceptual and architecture review
- **Author:** Rashedul Haque Ronjon
- **Original draft history:** Earlier project notes may predate the public repository; preserve verified original dates separately.
- **Current repository:** https://github.com/RashedulHaqueRonjon/PASS-Framework
- **Target:** Database-first ASP.NET Core MVC applications

## 1. Summary

This RFC proposes PASS, a project-aware scaffolding and reconciliation framework that remembers shared project conventions, inspects database and application state, maps dependencies among generated artifacts, produces a probable-outcome plan before code generation, and applies reviewed changes only after explicit authorization.

PASS complements Microsoft's existing tooling. It does not claim that standard scaffolding always overwrites custom code; the proposal builds on available EF Core reverse-engineering, partial-class and template customization capabilities while investigating broader lifecycle coordination and safe cross-artifact change management.

## 2. Goals

- Reuse project-wide settings from `pass.json`.
- Support an initial SQL Server/EF Core/database-first workflow.
- Trace impact among database, entity, `DbContext`, view model, controller, Razor, client scripts, project dependencies and tests.
- Track generated artifact ownership and baselines.
- Require planning before candidate generation and separate approval before application.
- Stop and report ambiguous/destructive conflicts.
- Provide reproducible CLI automation, then a Visual Studio integration.

## 3. Non-goals for the initial scope

- Replacing Microsoft's scaffolding tools.
- AI inference of business rules.
- Automatic database DDL or migration execution.
- Guaranteed arbitrary merging of every custom C# or Razor file.
- Supporting every database provider or MVC architecture from the first release.

## 4. Core decisions

- Six awareness domains: project, database, developer/preference, code, application and generation-history awareness.
- Code Awareness is used instead of Logic Awareness in the current design.
- Database-first is the initial source-of-truth mode.
- Planning is read-only and precedes code generation.
- Candidate preparation and application have separate approval gates.
- The dependency graph discovers impact in response to changes to any tracked artifact; write direction is controlled by source-of-truth and artifact rules.

## 5. Proposed workflow

1. Inspect project and database read-only.
2. Resolve `pass.json` and project authorities.
3. Build/refresh artifact dependency graph.
4. Produce the plan and probable-outcome report.
5. Obtain approval to prepare candidates.
6. Generate in isolated staging; reconcile against manifest/baseline.
7. Show exact diffs and validation/risk report.
8. Obtain separate approval to apply exact candidate hashes.
9. Apply transactionally and record audit/rollback state.

## 6. Unresolved design questions

1. Which Razor extension-point patterns offer the best balance between customization and predictable generation?
2. How should adoption confidence be represented for projects with no previous generation manifest?
3. Which schema-object types are included in the first SQL Server provider?
4. Which dependency relationships are statically discoverable and which require explicit developer declarations?
5. What approval-record format is suitable for protected CI workflows?
6. How should template extension packages be signed, trusted and versioned?
7. What is the appropriate baseline comparison for EF Core reverse engineering versus MVC view/controller scaffolding?

## 7. Feedback requested

Please challenge the source-of-truth policy, cross-artifact impact graph, approval model, conflict classifications, manifest schema and evaluation protocol. Concrete counterexamples and reproducible scenarios are particularly valuable.

## 8. Status disclaimer

This RFC specifies a proposed design. It does not describe a currently implemented or released PASS tool. Status changes must be supported by source code, tests and reproducible evidence.
