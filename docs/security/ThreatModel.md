# PASS Threat Model

**Status:** Preliminary conceptual threat model; requires review before implementation.

## 1. Assets to protect

- Application source code and developer customizations.
- Database credentials and schema/data confidentiality.
- Database integrity and availability.
- Project build configuration and package dependencies.
- Generation plans, approvals, manifests and rollback backups.
- CI identities, signing/approval material and extension/template trust.

## 2. Trust boundaries

- PASS CLI/VSIX process versus target project files.
- PASS process versus SQL Server connection.
- Trusted project profile versus personal/local secrets.
- Trusted built-in templates versus third-party templates/extensions.
- Local operator versus CI service identity/approver.
- Candidate staging versus target-project application.

## 3. Threats and mitigations

| Threat | Proposed mitigation |
|---|---|
| Credential leakage | Reference connection-string names; never persist secret values in pass.json, manifest or logs. |
| Unauthorized file modification | Explicit plan approval and separate apply approval; least-privilege file permissions. |
| Destructive regeneration | Baselines, ownership classes, exact diffs, conflict stop/report and transaction backups. |
| Stale approval replay | Bind approvals to plan digest, input fingerprints and candidate hashes; reject replay/stale input. |
| Path traversal | Canonicalize and validate output paths; restrict writes to approved roots and staging. |
| Malicious database metadata | Treat metadata as untrusted data; escape identifiers and never execute embedded instructions. |
| SQL injection in generated queries | Parameterize values; allowlist sort/filter identifiers; test generated queries. |
| Unsafe templates/extensions | Explicit trust, version and capability policy; isolate candidate generation; no implicit execution of untrusted plugins. |
| CI approval bypass | Protected environments or trusted signed approval records bound to exact plan digest. |
| Secret leakage in diagnostics | Redact credentials and sensitive values; test logs and reports. |
| Incomplete rollback | Pre-capture file state, journal every operation, test failure injection and clearly disclose irreversible external effects. |

## 4. Database access

Read-only metadata access is the default. PASS must not use an application's privileged runtime identity when a restricted schema-inspection identity is sufficient. Database change scripts are separate reviewed deliverables and are never executed as an incidental part of application scaffolding.

## 5. Generated web application security

Generated MVC code must use server-side validation, authorization policies, anti-forgery protection for cookie-authenticated state-changing requests, safe model binding/overposting controls, parameterized queries, allowlisted sorting and safe error handling. Feature selection does not authorize weakening existing security controls.

## 6. Residual risks

Static analysis cannot prove business correctness. A valid syntax tree can still encode incorrect behaviour. Custom application code and third-party templates may be impossible to reconcile automatically. PASS must prefer an explicit unresolved conflict over an unsafe guess.
