# PASS Troubleshooting (Planned Diagnostics)

**Status:** Proposed diagnostic catalogue; no executable diagnostic codes exist yet.

| Condition | Required behaviour |
|---|---|
| Invalid or unknown `pass.json` schema version | Stop; identify the field/version and migration path. |
| Database unavailable | Stop database-dependent planning; do not guess schema. |
| Insufficient metadata permissions | Report missing metadata and required read-only permissions. |
| Database/EF model drift | Report both states under database-first authority; do not run migrations. |
| Unknown file ownership | Mark for adoption/review; do not overwrite. |
| Manual modification to generated file | Compare baseline/current/candidate; merge only when supported and unambiguous. |
| Razor merge unsupported | Stop that artifact and explain manual extension-point options. |
| New dependency required | Include package/project changes in plan; require approval. |
| Stale plan | Reject; repeat inspection and planning. |
| Candidate build fails | Show diagnostics; do not apply. |
| Apply partially fails | Follow only the rollback policy approved in the transaction plan; otherwise preserve recovery files and stop. |
| Output path escapes project root | Reject as unsafe. |

Future diagnostics should have stable codes, severity, affected artifact, evidence, remediation guidance and links to the relevant architecture section.
