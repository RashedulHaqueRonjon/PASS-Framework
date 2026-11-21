# PASS User Guide (Proposed Workflow)

**Status:** Conceptual guide; PASS is not yet implemented. The commands below are proposed interface examples, not currently executable commands. For explanations of technical terms and PASS-specific terminology used in this guide, see the [PASS Glossary and Technical Terminology](../Glossary.md).


## 1. Intended user workflow

1. Open an existing ASP.NET Core MVC application.
2. Run read-only project/database inspection.
3. Initialize or review the shared `pass.json` profile.
4. Select a table or an existing module to add/synchronize.
5. Review the dependency-impact plan and probable outcome.
6. Approve candidate preparation.
7. Review exact file diffs and validation results.
8. Separately approve application of the exact changes.
9. Review the transaction record and any follow-up warnings.

## 2. Project memory

`pass.json` stores shared PASS preferences. PASS detects build facts from the project files and does not treat the profile as permission to change the target framework, package references, security policies or database.

## 3. New module versus existing module

- **Add:** propose a new module from a database object using current approved project conventions.
- **Sync:** analyse an existing module against current schema and project state.
- **Adopt:** register an existing module, review ownership and establish a confirmed baseline.

These operations have different impact sets and must not be conflated.

## 4. Approval and safety

The plan is read-only. Approving candidate preparation does not approve project writes. PASS then prepares candidate output in staging and displays an exact diff. A second approval is required to apply that exact diff. A changed input invalidates the plan. Unresolved conflicts stop the affected operation.

## 5. Screenshots

Use the retained Customer CRUD screenshots under `docs/images/` as visual references. The screenshots are not a substitute for a written requirements checklist or source code. Record exact field names, labels, validation, layout, styling and interactions when the images are visually inspected.
