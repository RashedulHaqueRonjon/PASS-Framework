# Contributing to PASS

Thank you for considering a contribution to PASS (Project Aware Smart Scaffolder).

## Current phase

PASS is in the **conceptual research and RFC phase**. The architecture and requirements are being discussed; the proposed source-code projects are not implemented yet. Please do not interpret proposed commands, components, diagrams or screenshots as a released product.

## Useful contributions now

- Review the research questions and related-work coverage.
- Challenge assumptions about EF Core reverse engineering, MVC scaffolding and template customization.
- Review the database-first source-of-truth decision.
- Review the approval-before-generation and approval-before-application workflow.
- Identify dependency-propagation and reconciliation edge cases.
- Review security, rollback, reproducibility and evaluation plans.
- Suggest sample schemas and repeatable schema-evolution scenarios.

Use the GitHub issue templates for architecture feedback, bug reports about documentation, and feature proposals. General discussion is available through the repository issue tracker unless GitHub Discussions is enabled.

## Proposed workflow for documentation contributions

1. Open or identify an issue describing the problem or proposed change.
2. State the affected requirement, document and architecture decision.
3. Explain alternatives and consequences, including safety and compatibility effects.
4. Submit a pull request with narrowly scoped changes.
5. Update related documents when a decision changes; do not update only one isolated section if the change affects other artifacts.
6. Do not claim implementation or test results unless they have actually been produced and can be reproduced.

## Future code contribution requirements

When implementation begins, the project will add compiler/build requirements, coding standards, tests, package policies, contribution labels and a release process. Until then, code-specific contribution instructions are provisional.

## Architecture decisions

Material decisions should be recorded as Architecture Decision Records (ADRs) under `docs/architecture/decisions/`. Accepted decisions should be reflected consistently in the README, RFC, architecture documents, guides, configuration schema and tests.

## Code of Conduct

All contributors must follow [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).
