# PASS.Abstractions

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Provider-neutral contracts, immutable request/result models, diagnostics, identifiers and normalized project/schema/artifact types. Keep this assembly free of SQL Server, CLI and Visual Studio dependencies.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
