# ADR-0004: Cross-Artifact Dependency and Impact Graph

- **Status:** Accepted for the conceptual design
- **Date:** 2026-11-19

## Context

An application change rarely affects only one file. A database property may influence its entity, mapping, view model, controller, Razor views, scripts, query features and tests. A controller, view, project setting or package change may also affect other dependents.

## Decision

PASS maintains typed, directional dependency edges and forward/reverse indexes. Any change to a tracked node triggers impact discovery across dependent nodes. The graph reports proposed updates, preserves, review requirements, conflicts and no-change decisions.

Reverse dependency discovery does not mean a change can be propagated as a write in either direction. Source-of-truth rules and artifact-specific policies decide which transformations are valid. For example, a controller change does not authorize a database schema change.

## Consequences

- Every plan lists affected artifacts and explains why they are included/excluded.
- New generators/providers must publish dependency metadata.
- Impact precision and recall become evaluation metrics.
