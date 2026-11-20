# Sample: SchemaEvolution

**Status:** Planned sample; not implemented.

## Purpose

Provide repeatable SQL Server snapshots demonstrating changes to a Customer-like entity and the cross-artifact impact expected from PASS.

## Planned snapshots

- `v1`: initial table and MVC module.
- `v2-add-column`: add a nullable field.
- `v3-rename-column`: introduce a controlled rename mapping.
- `v4-change-type`: change a type/length with compatibility analysis.
- `v5-foreign-key`: add or remove a relationship.
- `v6-delete-column`: test a destructive schema change.

Actual schema and field names will be established from the retained screenshots or original database if recovered. Each snapshot must be deterministic and include seed data plus expected impact-set files.

## Core test

Change the database schema, then check the plan for entity, DbContext, view model, controller, Razor/HTML, JavaScript/AJAX, tests, project dependencies and migration-drift observations. The plan must explain which are updated, preserved, reviewed or unchanged. It must not modify the database or project before approval.
