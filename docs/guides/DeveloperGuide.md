# PASS Developer Guide (Planned)

**Status:** Architecture guidance only; no code projects or public APIs exist yet.

## 1. Solution boundaries

The planned solution separates abstractions, orchestration, SQL Server metadata access, EF Core integration, MVC generators, templates, CLI and future Visual Studio integration. See [Component Architecture](../architecture/ComponentArchitecture.md).

## 2. Engineering rules

- Keep `PASS.Core` provider-neutral.
- Keep database discovery read-only.
- Model dependencies as typed edges with evidence and provenance.
- Keep planning separate from generation and application.
- Generate candidates outside the target project.
- Keep approval decisions bound to plan/candidate hashes.
- Use Roslyn only for supported C# transformations.
- Treat Razor, JavaScript, TypeScript, CSS, JSON, XML/MSBuild and SQL with suitable strategies.
- Add tests for success, conflicts, stale plans, cancellation, rollback and idempotency.

## 3. Proposed project references

`PASS.Abstractions` is the low-level contract layer. `PASS.Core` consumes it. Provider and generator assemblies implement or consume the contracts. `PASS.CLI` and future `PASS.VSIX` call shared services. Avoid circular references and UI dependencies in the core.

## 4. Extension model

Provider and template extensions must declare versions, capabilities, supported framework/provider ranges and trust requirements. Discovery must be explicit; untrusted templates must not be executed automatically.

## 5. Implementation status

Do not create public API stability guarantees until interfaces, compatibility policy and package versioning have been reviewed and tested.
