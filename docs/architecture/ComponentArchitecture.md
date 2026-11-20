# PASS Component Architecture

**Status:** Proposed component boundaries; no projects or interfaces are implemented yet.

## 1. Planned components

| Planned project | Responsibility | Must not own |
|---|---|---|
| `PASS.Abstractions` | Provider-neutral contracts, models and result types. | SQL Server-specific code, CLI UI or VSIX APIs. |
| `PASS.Core` | Orchestration, configuration resolution, normalized project/schema models, dependency graph, planning and policy decisions. | Provider-specific SQL, command-line parsing or Visual Studio UI. |
| `PASS.Database.SqlServer` | Read-only SQL Server metadata discovery and normalization. | MVC view generation or file application. |
| `PASS.EFCore` | EF Core metadata/reverse-engineering integration and model/DbContext generation coordination. | Direct database DDL execution by default. |
| `PASS.Generators.Mvc` | MVC controllers, view models, Razor views and related artifact generation. | Core policy or Visual Studio UI. |
| `PASS.Templates` | Versioned templates and template metadata. | Unreviewed arbitrary file writes. |
| `PASS.CLI` | Command parsing, human-readable/JSON reports and explicit approval interaction. | Independent business logic or merge algorithms. |
| `PASS.VSIX` | Future Visual Studio entry points and presentation; calls shared PASS services. | A forked generation engine. |

## 2. Proposed abstractions

The following are conceptual contract names, not implemented APIs:

- `IProjectInspector`
- `IDatabaseSchemaProvider`
- `IPassConfigurationProvider`
- `IDependencyGraphBuilder`
- `IImpactAnalyzer`
- `IExecutionPlanBuilder`
- `ICandidateGenerator`
- `IArtifactManifestStore`
- `IReconciliationStrategy`
- `IValidationRunner`
- `IApprovalService`
- `ITransactionalFileApplier`
- `IRollbackService`

Use immutable request/result models where practical. Providers should return structured diagnostics instead of making silent assumptions.

## 3. Dependency direction

`PASS.Abstractions` should be the lowest-level shared contract assembly. `PASS.Core` depends on abstractions. Database and EF Core adapters implement provider contracts. MVC generators consume normalized project/schema/configuration models. CLI and VSIX depend on application services, not on each other's UI code.

Circular project references are to be avoided. A component may publish capability metadata so the planner can determine whether a requested feature is supported.

## 4. Candidate versus application boundaries

Generators write only to an isolated candidate workspace. They do not directly overwrite the target project. A separate reconciler creates an exact candidate diff. A validator inspects the candidate. Only the transactional applier may modify the target, and only after the approved plan and candidate hashes are verified.

## 5. Error handling

Diagnostics should include a stable code, severity, affected artifact, explanation, evidence, proposed resolution and whether execution is blocked. Fatal/ambiguous conflicts block the affected plan. Warnings must still be shown to the approver; warnings do not authorize silent changes.

## 6. Future extension points

Future provider adapters may support other databases like PostgreSQL, My SQL, and Excel or Text file tables. Future generators may support API projects or alternative UI stacks. Extension discovery must be explicit, versioned and trusted; templates/extensions must not execute arbitrary code merely because they are present in a repository.
