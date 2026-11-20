# PASS.Core

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Orchestration, configuration resolution, project inspection coordination, dependency graph, impact planner, execution plans, approval policy and transaction coordination. It must not write target files directly.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
