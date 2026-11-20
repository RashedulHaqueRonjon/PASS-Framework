# ADR-0002: Plan Before Generation and Require Explicit Approval

- **Status:** Accepted for the conceptual design
- **Date:** 2026-11-19

## Context

Even apparently minor file, configuration, project, template or markup changes can affect an application. A conventional dry-run that only prevents destructive changes is not strict enough for the project's stated safety requirement.

## Decision

PASS uses two approval gates:

1. A read-only plan and probable-outcome report is produced before source-code generation.
2. An authorized user approves candidate preparation in isolated staging.
3. The exact diff and validation report are shown.
4. An authorized user separately approves application of the exact candidate hashes and listed operations.

No project or database mutation occurs without approval. A generic `--yes` cannot bypass the gates. CI requires a trusted approval record or protected environment gate bound to the plan digest.

## Consequences

- Candidate generation is separated from target-project writes.
- Newly discovered scope invalidates the plan.
- Rollback is limited to the exact approved transaction and pre-authorized rollback behaviour.
- The CLI and future VSIX must share this workflow.
