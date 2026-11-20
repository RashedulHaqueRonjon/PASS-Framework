# PASS Configuration and Precedence

## 1. Purpose of `pass.json`

`pass.json` is the shared, version-controlled project profile for PASS-specific generation choices and policies. It belongs in the root of an ASP.NET Core application managed by PASS. Do **not** put a runtime `pass.json` in the PASS framework repository root simply because the framework itself is under development.

Do not store passwords, access tokens, private certificates or full connection strings in `pass.json`. Store a connection-string name or provider alias; obtain secrets from the application's normal secure configuration mechanism.

## 2. Authority by information type

| Information | Authoritative source in initial mode |
|---|---|
| Database tables, columns, keys and relationships | Live SQL Server database schema (database-first) |
| PASS generation preferences and policy | `pass.json` |
| Target framework and project references | `.csproj` / imported MSBuild files |
| SDK selection | `global.json` and installed SDK policy |
| Team-wide NuGet versions | `Directory.Packages.props` where central package management is used |

For current ASP.NET Core projects, the project definition is normally the MSBuild **`.csproj`** file. The old `project.json` project format belongs to earlier .NET Core tooling and is not the planned baseline. PASS may detect legacy projects as a separate adoption/compatibility case, but must not treat `project.json` as the current project file or silently migrate it.
| Existing developer customizations | Current user files compared with recorded baseline/manifest |
| Generated provenance | PASS manifest and baseline store |
| Business intent | Explicit developer requirements; not inferred in MVP |

## 3. Configuration precedence

For a PASS operation, resolve settings in this order:

1. Explicit, operation-scoped command-line overrides.
2. Validated project-level `pass.json` values.
3. Explicitly configured personal preferences, if enabled and permitted by policy.
4. Documented PASS defaults.

A command-line override applies only to that operation unless the user separately approves a change to `pass.json`. Do not silently persist temporary overrides.

Project facts such as target framework and installed packages are detected from project/build files, not overwritten because `pass.json` contains a preferred value.

## 4. Initial database-first mode

`database.sourceOfTruth` is `databaseFirst` in the initial schema. The live schema drives generated model shape. EF Core migration snapshots can be inspected for drift but are not an alternate authority in this mode. See [Database Providers](DatabaseProviders.md) and ADR-0001.

## 5. Approval policy

The required default is `planOnly` and `approvalRequired: true`:

- `plan`: read-only; no target file, configuration, project or database changes and no source-code generation.
- `prepare`: requires explicit approval; generates candidates in isolated staging only.
- `review`: shows exact candidate diffs, probable outcomes and validation results.
- `apply`: requires a second explicit approval for the exact plan and candidate hashes.

No generic `--yes` flag may bypass these approvals. Non-interactive execution requires a trusted, externally approved authorization record or protected CI approval mechanism bound to the plan digest. A stale plan must be rejected and regenerated.

## 6. Feature settings do not authorize side effects

Selecting soft delete, audit trail, a UI framework or a grid library expresses a desired generated feature; it does not authorize changing the database, adding a package, modifying project files or altering security policy. Those effects must appear in the plan and receive explicit approval. Database writes are disabled by default.

## 7. Schema evolution

Increment `schemaVersion` only through a documented migration process. PASS must validate configuration before preparing candidates and must stop on unknown incompatible versions. A migration should preserve unknown user-owned fields where safe or report that it cannot do so.
