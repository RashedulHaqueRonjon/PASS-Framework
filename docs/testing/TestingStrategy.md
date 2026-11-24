# PASS Testing Strategy

**Status:** Planned test strategy; no tests have been implemented.

## 1. Test layers

- **Unit tests:** configuration validation, source-of-truth decisions, dependency graph, impact traversal, plan determinism, conflict classification and hash validation.
- **Database integration tests:** SQL Server metadata discovery, permissions, type mapping, foreign keys, views and schema evolution.
- **Generation snapshot tests:** generated C#, Razor, JSON and project artifacts compared against approved snapshots.
- **End-to-end tests:**   
*Success pat*h: inspect → plan → approve prepare → prepare → review → approve apply → apply → verify → complete.  
*Failure path*: inspect → plan → approve prepare → prepare → review → approve apply → apply → verification failure → rollback → restore pre-application state → verify restoration → report recovery result.
- **Security tests:** path traversal, untrusted metadata/template content, injection, secret leakage, authorization bypass and unsafe SQL sorting.
- **Failure-injection tests:** database disconnect, staging failure, file-write failure, validation failure and rollback failure.

## 2. Mandatory safety tests

1. `plan` does not alter project/database hashes.
2. Candidate preparation without approval is rejected.
3. Application without second approval is rejected.
4. An approval cannot be reused for a different plan or candidate hash.
5. Any changed input invalidates a plan.
6. An ambiguous destructive conflict stops the affected operation.
7. Developer-owned files are never overwritten.
8. A failed operation restores only the exact pre-approved transaction state.
9. Identical inputs produce deterministic plan/candidate output.
10. Repeated application does not create duplicate code.

## 3. Test data

Use version-controlled schema scripts and deterministic seed data. Include add, rename, drop, type change, nullability change, foreign-key changes, manually modified code, modified Razor, missing files and schema/model drift.

## 4. CI policy

During the conceptual phase, CI validates documentation and JSON syntax only. Build/test jobs should activate only after real solution/project/test files exist. Never report skipped tests as passed tests.
