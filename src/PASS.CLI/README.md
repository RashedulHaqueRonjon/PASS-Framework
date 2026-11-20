# PASS.CLI

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Proposed `dotnet pass` entry point for inspect, plan, prepare, review, apply, adopt, doctor and rollback operations. The CLI must use PASS.Core services.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
