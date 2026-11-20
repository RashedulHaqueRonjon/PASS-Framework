# PASS.Database.SqlServer

**Status:** Planned component; no `.csproj` or implementation code exists yet.

Read-only SQL Server metadata provider for schemas, tables, columns, keys, relationships, constraints, indexes and supported views. No DDL execution in the MVP.

## Initial responsibilities

See [Component Architecture](../../docs/architecture/ComponentArchitecture.md) and [System Architecture](../../docs/architecture/SystemArchitecture.md). Project references and public contracts must be finalized before creating this project.

## Required tests

Tests should cover normal behaviour, unsupported inputs, conflict cases, stale plans, deterministic output and the approval invariants applicable to this component.
