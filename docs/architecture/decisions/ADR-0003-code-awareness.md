# ADR-0003: Code Awareness, Not Logic Awareness, in the Initial Model

- **Status:** Accepted for the current conceptual scope
- **Date:** 2026-11-19

## Context

“Logic Awareness” is currently vague. Reliable understanding of business intent would require explicit business-rule/system/method specifications, formal mapping to source code and likely AI-assisted interpretation with human validation.

## Decision

Use **Code Awareness** in the current PASS model. It covers syntax, symbols, references, code conventions, customizations, generated markers and artifact ownership. Do not claim that PASS understands the developer's business logic or can infer intent.

A future Logic Awareness feature may be researched only after a method for expressing business rules and mapping specifications to code has been defined. Any AI-assisted interpretation must remain reviewable, evidence-backed and subject to human approval.

## Consequences

- The six awareness domains use Code Awareness.
- Business-rule inference is a non-goal of the initial scope.
- Documentation must not use “logic-aware” as a current capability claim.
