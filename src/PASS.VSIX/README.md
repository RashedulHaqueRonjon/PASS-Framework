# PASS.VSIX

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Future Visual Studio integration. It should invoke shared PASS application services and display the same plan, approval, diff and conflict information as the CLI.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
