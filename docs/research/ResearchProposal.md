# PASS: Research Proposal

**Full name:** Project Aware Smart Scaffolder (PASS)  
**Author:** Rashedul Haque Ronjon  
**Status:** Conceptual research proposal / pre-implementation  
**Primary domain:** Database-first ASP.NET Core MVC development
**Terminology:** Reference to the [PASS Glossary and Technical Terminology](../Glossary.md) for definitions of abbreviations and specialist terminology used in this proposal

## Abstract

This proposal introduces PASS, a project-aware scaffolding and change-reconciliation framework for database-first ASP.NET Core MVC applications. PASS investigates how persistent project conventions, database-schema inspection, code and application analysis, generated-artifact provenance, dependency-impact analysis and approval-gated reconciliation can support the evolution of generated application code. The proposed system complements existing Microsoft tooling rather than replacing it. Its principal research concern is not initial CRUD generation alone, but the traceable and safe coordination of dependent artifacts as database schemas and application requirements change.

PASS is currently conceptual. The architecture, prototypes, evaluation protocol and research questions are proposed; no implementation performance or preservation results are claimed.

## 1. Background and motivation

Database-first scaffolding can generate useful entity and application code. In a continuing application, however, the database schema, data model, controllers, view models, Razor views, client-side scripts, tests, package references and project conventions evolve together. A change to one artifact may make another artifact stale or inconsistent.

Microsoft's ecosystem already provides valuable building blocks, including EF Core reverse engineering, partial classes, partial model-configuration hooks and T4 template customization. PASS does not claim these mechanisms are absent. The research gap to investigate is whether a unified project-level process can coordinate configuration memory, cross-artifact impact analysis, provenance, explicit planning, approval and reconciliation across a wider MVC application lifecycle.

## 2. Problem statement

The problem addressed is the lack of a unified, project-scoped and approval-governed workflow for maintaining consistency and safely reconciling generated artifacts across successive database-first scaffolding operations.

The problem includes:

1. Repeated selection and re-application of project conventions.
2. Incomplete visibility into which files and components depend on a changed database object or project setting.
3. Difficulty distinguishing generator-owned code from developer-owned modifications.
4. Risk of inconsistent artifacts after changes to entities, controllers, `DbContext`, Razor views, scripts or project dependencies.
5. Insufficiently explicit planning, authorization, conflict handling and rollback before changes are applied.
6. Difficulty reproducing generation results across team members and environments.

This formulation avoids attributing destructive behaviour to all Microsoft scaffolding workflows. Instead, it focuses the research on the specific challenges of project-wide configuration consistency, cross-artifact impact analysis, generated-code provenance, developer customization preservation and controlled regeneration.

## 3. Aim and objectives

**Aim:** Design and evaluate a deterministic, project-aware scaffolding and reconciliation workflow that improves traceability, consistency and protection of developer modifications during database-first ASP.NET Core MVC evolution.

Objectives:

- Specify a versioned, team-shareable `pass.json` profile.
- Inspect project and SQL Server schema metadata without modifying the project or database.
- Represent relationships among schema objects and application artifacts as a dependency graph.
- Identify impact in dependent artifacts when any tracked artifact changes.
- Produce a probable-outcome execution plan before candidate code generation.
- Require explicit approval before generating candidate artifacts and separate approval before applying them.
- Track generated baselines and ownership with a manifest.
- Use language-appropriate mechanisms, including Roslyn for supported C# analysis/transformation and Razor-aware strategies for `.cshtml`.
- Stop and report ambiguous or destructive conflicts.
- Evaluate the design through reproducible scenarios and fair baselines.

## 4. Proposed contribution

The proposed contribution is a coordinated workflow comprising:

1. **Project memory:** shared scaffolding conventions persisted in `pass.json`.
2. **Six awareness domains:** project, database, developer/preference, code, application and generation-history awareness.
3. **Dependency-impact graph:** links schema and application artifacts, including reverse-impact lookup.
4. **Execution planning:** read-only inspection and impact/outcome report before generation.
5. **Approval gates:** approval to prepare candidate outputs, followed by separate approval to apply the exact reviewed changes.
6. **Artifact provenance:** manifest and baselines for generator ownership and three-way reconciliation.
7. **Safe application:** staged writes, validation, transaction records and an explicitly authorized rollback strategy.

Incremental scaffolding is a system capability spanning the awareness domains. Extensibility is a cross-cutting architectural property, not an additional awareness domain.

## 5. Scope and assumptions

The initial research and implementation scope is conventional ASP.NET Core MVC, SQL Server and EF Core. Database-first is the only initial source-of-truth mode. The live database schema is authoritative for database structure; generated EF Core entities and mappings are derived application artifacts. PASS must not execute DDL or migrations against a database as part of normal scaffolding.

A future migrations-first mode may be studied separately. It must select EF Core migrations/model snapshot as the authority and use the live database for drift detection. PASS must not silently combine database-first and migrations-first authority.

Code Awareness is included now. Automated inference of business intent or business rules is out of scope. Such a future Logic Awareness capability would require explicit rule specifications, formal mappings and possibly AI-assisted interpretation, with human verification and a separate research study.

## 6. Research questions

- **RQ1 — Configuration consistency:** To what extent does persistent project configuration reduce repeated setup effort and variation across generated modules?
- **RQ2 — Impact analysis:** How accurately does the dependency graph identify artifacts affected by a change to a schema object, source file, project setting or dependency?
- **RQ3 — Preservation and reconciliation:** How effectively can the proposed manifest and reconciliation strategy preserve developer-owned changes while applying safe generated changes?
- **RQ4 — Approval and control:** Does the plan/prepare/review/apply workflow provide sufficient transparency and meaningful user control without imposing unacceptable effort?
- **RQ5 — Productivity:** How does the workflow affect total task time, manual edits and conflict-resolution effort compared with fair baseline approaches?
- **RQ6 — Reproducibility:** To what extent do equivalent project, schema, configuration and generator inputs produce equivalent plans and outputs?

## 7. Fair comparison with existing approaches

The evaluation should distinguish at least:

- **Baseline A:** the relevant standard Microsoft workflow, with its normal options.
- **Baseline B:** Microsoft-supported customization approaches where applicable, including partial classes, partial model-configuration hooks and customized EF Core T4 templates.
- **Candidate C:** PASS's proposed project profile, impact analysis, manifest, staged reconciliation and approval gates.

EF Core database reverse engineering and MVC controller/view scaffolding are distinct workflows and should be evaluated separately where their capabilities differ. Do not assume that every standard scaffolding run overwrites files or that a developer must rewrite an entire custom method. Record exact tool versions, commands, options and results.

## 8. Expected outcomes (not yet demonstrated)

Expected outcomes include a coherent architecture, a reference implementation, a reproducible scenario suite and empirical evidence about consistency, change-impact coverage, preservation, conflicts, developer effort and performance. These are research targets, not claims of achieved results.

## 9. Limitations and threats to validity

The first implementation will be limited by provider coverage, the difficulty of understanding arbitrary custom code, language-specific merge capabilities, project diversity and the quality of recorded baselines. A dependency graph can identify likely impact but cannot infer all business intent. A syntactically successful merge does not prove semantic correctness. Human review and automated tests remain necessary.

## 10. Status

This document describes a research proposal. Implementation, performance measurements, user studies and validation results will be added only after they have been completed and reproducible evidence is available.
