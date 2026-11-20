# ADR-0001: Database-First as the Initial Source of Truth

- **Status:** Accepted for the conceptual MVP baseline
- **Date:** 2026-11-19

## Context

PASS targets database-first ASP.NET Core MVC applications. The database schema and EF Core model/migration state can disagree. Treating both as equal authorities would make generation decisions ambiguous.

## Decision

The initial supported mode is **database-first**. The live SQL Server schema is authoritative for database structure. Generated EF Core entities and `DbContext` mappings are derived representations. Migrations/model snapshots may be inspected for drift but must not override the live schema. PASS does not execute DDL or migrations in ordinary scaffolding.

A future migrations-first mode must be separately selected, designed, versioned and tested. Mixed/unclear authority stops automatic synchronization.

## Consequences

- The first database adapter is SQL Server and read-only for inspection.
- Schema changes flow into application artifact impact analysis.
- Proposed database changes are separate SQL/migration review artifacts.
- The current `pass.json` schema accepts only `databaseFirst`.
