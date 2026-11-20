# Security Policy

## Project status

PASS is currently a conceptual research/RFC project. There is no released PASS executable or supported production deployment at this stage.

## Reporting a vulnerability

Please do not publish credentials, connection strings, private customer data or exploit details in a public issue. Use the repository's **Report a vulnerability** private reporting facility if it is enabled. If that facility is unavailable, contact the repository maintainer privately through a verified contact channel before disclosing technical details.

## Security design priorities

The proposed design will address:

- Read-only database access for schema inspection by default.
- No automatic database DDL execution during ordinary scaffolding.
- No credentials or secrets in `pass.json`, manifests or logs.
- Explicit approval before candidate generation and before applying project changes.
- Least-privilege file and database permissions.
- Safe handling of templates and untrusted database metadata.
- Output-path validation and protection against path traversal.
- Parameterized database access and allowlisted sort expressions.
- Anti-forgery protection, authorization and server-side validation in generated MVC features.
- Auditable plans, approvals, transactions and rollback records.

See [Threat Model](docs/security/ThreatModel.md). A security response time or supported-version guarantee will be published only after a maintained implementation and release process exist.
