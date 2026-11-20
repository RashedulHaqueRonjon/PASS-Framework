# Database Providers and Source-of-Truth Policy

## 1. Initial provider

The first planned provider is Microsoft SQL Server. Its responsibility is read-only discovery and normalization of supported database metadata for planning and generation.

The initial provider should inspect, as supported and tested:

- Database and schema identity.
- Tables and columns.
- SQL types, length/precision/scale and nullability.
- Primary and foreign keys.
- Unique/check/default constraints.
- Indexes.
- View definitions/metadata where permissions allow.
- Relationship cardinality and delete/update behaviour where discoverable.
- Stored procedures and parameters as a later, separately specified capability.

## 2. Database-first is the initial authority

In version 1, the live SQL Server schema is the authority for database structure. EF Core entity classes and `DbContext` mappings are derived representations. Existing EF Core migrations/model snapshots may be inspected for drift, but they must not silently override the live database schema.

The provider must use read-only credentials for inspection where possible. PASS must not issue DDL, apply migrations, insert/update/delete data or change database permissions during normal planning, candidate preparation or application of application files.

If a developer requests a proposed database change, PASS may create a separate SQL script or migration proposal as a review artifact. Executing it is a distinct, privileged operation outside the default scaffolding transaction and requires its own explicit plan, authorization, backup and recovery strategy.

## 3. Conflicting database and EF Core state

Examples include a live column absent from the model snapshot, a model property absent from the database, a migration not applied to the target database, or an entity property manually changed from the schema type.

PASS should classify the mismatch, show evidence and determine whether the selected database-first policy makes a safe projection possible. If mapping is ambiguous, stop and report. Do not automatically apply migrations or alter the database to make the representations agree.

## 4. Future migrations-first mode

A future mode may select EF Core migrations/model snapshot as the schema authority. In that mode the target database is compared for drift; it is not treated as the authority for model generation. The mode needs its own ADR, configuration version, test fixtures and migration/script approval flow.

A project with mixed or unclear authority must be marked unsupported for automatic synchronization until an authorized maintainer selects and documents one mode.

## 5. Provider abstraction

A provider adapter should return a normalized schema model and diagnostics. It should not generate MVC code directly. Future adapters (for example PostgreSQL) must declare supported object types, type mapping rules, limitations and version compatibility.

## 6. Metadata safety

Database identifiers, comments, extended properties and object names are untrusted input. Treat them as data, never as executable template instructions. Quote identifiers safely, parameterize metadata queries and validate generated identifiers and output paths.
