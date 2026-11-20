# PASS.EFCore

**Status:** Planned component; no `.csproj` or implementation code exists yet.

EF Core integration for reverse-engineered entities, DbContext and model metadata. Database-first schema remains authoritative in the initial mode.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
