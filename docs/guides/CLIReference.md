# PASS CLI Reference (Proposed)

**Status:** Proposed command design; commands are not implemented or executable yet.

The proposed tool command is `dotnet pass`. It is intended to be distributed as a .NET tool package whose command name is `pass`.

## Read-only commands

```powershell
dotnet pass inspect --project .\MyApp\MyApp.csproj
dotnet pass plan add --table dbo.Customer --project .\MyApp\MyApp.csproj
dotnet pass plan sync --entity Customer
dotnet pass plan adopt --entity Customer
```

`plan` must not create candidate source files or modify the target project/database. It displays the impacted artifacts, proposed operations, probable outcome, risks, assumptions and conflicts.

## Approval-gated candidate preparation

```powershell
dotnet pass prepare --plan <plan-id>
```

This requires an explicit authorized approval and prepares candidate files in isolated staging only. It does not apply them to the target project.

## Review and apply

```powershell
dotnet pass review --plan <plan-id>
dotnet pass apply --plan <plan-id>
```

`review` displays the exact diff and validation results. `apply` requires a separate explicit approval tied to the same plan and candidate hashes. If any relevant input changes, the plan becomes stale and must be regenerated.

## Rollback

```powershell
dotnet pass plan rollback --transaction <transaction-id>
dotnet pass apply --plan <rollback-plan-id>
```

A manual rollback is planned and approved like any other mutation. Automatic rollback after a failed apply is permitted only when the exact rollback action was included in and approved with the original transaction plan.

## Proposed options

- `--project`: target project file.
- `--table`: database object, schema-qualified where appropriate.
- `--entity`: existing application module/entity.
- `--provider`: database provider (initially SQL Server).
- `--connection-name`: name of a secure application connection setting, not a connection string secret.
- `--format`: human-readable or structured JSON report.
- `--output`: explicit report output path; writing the report is itself an operation.

There is no generic `--yes` bypass. CI/non-interactive approval must use a trusted approval record or protected environment gate bound to the plan digest.
