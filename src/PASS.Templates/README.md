# PASS.Templates

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Versioned, inspectable templates and metadata. Templates are inputs to candidate generation and must not bypass PASS approval or trust rules.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
