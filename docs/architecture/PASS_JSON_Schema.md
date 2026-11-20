# `pass.json` Schema and Project Profile

**Status:** Proposed schema version 1 for the conceptual/MVP design.

## 1. Purpose

`pass.json` stores shared PASS-specific generation preferences and policies for an ASP.NET Core MVC application. It should normally be committed to that application's source control so team members use consistent settings.

It is not a replacement for `.csproj`, `global.json`, MSBuild properties, application configuration or database schema. It must not contain secrets.

## 2. Example

```json
{
  "schemaVersion": 1,
  "database": {
    "provider": "SqlServer",
    "sourceOfTruth": "databaseFirst",
    "defaultSchema": "dbo",
    "connectionStringName": "DefaultConnection"
  },
  "ui": {
    "cssFramework": "Bootstrap5",
    "theme": "dark",
    "layout": "existing",
    "gridProvider": "native"
  },
  "features": {
    "pagination": {
      "enabled": true,
      "mode": "server",
      "pageSize": 10
    },
    "search": {
      "enabled": true,
      "global": true,
      "column": true
    },
    "sorting": {
      "enabled": true,
      "mode": "allowlisted"
    },
    "ajaxCrud": false,
    "validation": "DataAnnotations",
    "auditTrail": false,
    "softDelete": false,
    "antiForgery": true
  },
  "generation": {
    "defaultMode": "planOnly",
    "requireApprovalToPrepare": true,
    "requireApprovalToApply": true,
    "conflictPolicy": "stopAndReport",
    "manifestPath": ".pass/manifest.json",
    "baselinePath": ".pass/baselines",
    "allowDatabaseWrites": false
  }
}
```

## 3. Schema file

The machine-readable JSON Schema is `pass.schema.json` in this directory. The example above and that schema must be kept consistent. The schema is intentionally restrictive in version 1; unsupported values should produce a validation error rather than be silently ignored.

## 4. Important modelling decisions

- `sourceOfTruth` is explicitly `databaseFirst` in version 1. A future `migrationsFirst` mode needs a separate accepted design and tests; do not activate it by changing a string without implementing its semantics.
- Target framework is detected from `.csproj`; it is not a freely overridden PASS preference.
- `layout: existing` means reuse the project's detected layout rather than create/replace it.
- A grid provider is optional. A commercial provider must not become a mandatory dependency of `PASS.Core`.
- Feature flags do not authorize side effects. For example, `softDelete: true` does not authorize PASS to add a column to a live database.
- The generation policy requires a read-only plan, approval to prepare, exact diff review and a separate approval to apply.
- Connection strings are referenced by name only; secret values remain in secure application configuration.

## 5. Schema evolution

`schemaVersion` identifies the shape/meaning of this file, not the PASS binary version. Generator, template and manifest versions are recorded separately in generation history. An incompatible schema version must stop the operation and explain the required migration.
