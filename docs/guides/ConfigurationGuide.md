# PASS Configuration Guide (Proposed)

**Status:** Conceptual. See [PASS JSON Schema](../architecture/PASS_JSON_Schema.md) and [`pass.schema.json`](../architecture/pass.schema.json).

## 1. Where the profile belongs

Place `pass.json` in the root of the ASP.NET Core application that PASS manages. It does not belong automatically in the PASS framework repository.

## 2. What belongs in the profile

Shared generation choices such as database provider alias, source-of-truth mode, CSS framework, theme preference, layout preference, pagination/search/sorting and generation/conflict policies.

## 3. What does not belong

- Passwords, tokens, certificates or connection-string secrets.
- A duplicate target framework that disagrees with `.csproj`.
- Package versions that belong in `Directory.Packages.props`.
- Database schema definitions that are authoritative in the live database in database-first mode.
- Personal preferences that should not be shared with the team.

## 4. Precedence

Operation-scoped CLI override > project `pass.json` > optional personal preference > documented default. Temporary overrides do not persist unless the user separately approves a configuration change.

## 5. Changes to configuration

Changing a shared setting triggers impact analysis for every generated module that consumes it. PASS must present the complete probable impact before candidate generation; candidate preparation and application each require approval. A theme or grid change is not permission to silently update all views or add packages.
