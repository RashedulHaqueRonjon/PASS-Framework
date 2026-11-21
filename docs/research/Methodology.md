# Research Methodology

**Status:** Proposed methodology; no empirical results have been collected.

## 1. Research approach

The project will use a Design Science Research (DSR) approach: identify a practical problem, define objectives for a solution, design and develop an artifact, demonstrate it in representative scenarios, evaluate its behaviour and communicate the results. The artifact is the PASS architecture and, later, its reference implementation.

The methodology must distinguish architecture validation, software verification and empirical evaluation. A successful build is not evidence of developer productivity; a positive survey is not proof of safe reconciliation.

## 2. Awareness domains and capabilities

### 2.1 Awareness domains

1. **Project Awareness:** project structure, target framework, SDK, packages, folders, naming, conventions and project-level configuration.
2. **Database Awareness:** SQL Server objects, schemas, columns, types, nullability, keys, constraints, relationships, indexes and supported views.
3. **Developer/Preference Awareness:** explicitly selected personal defaults, kept distinct from shared team configuration.
4. **Code Awareness:** syntax, symbols, references, customizations, generated markers, ownership and supported language-specific transformations. This does not imply understanding business intent.
5. **Application Awareness:** relationships among entities, `DbContext`, controllers, services, view models, Razor views, scripts, routing, authorization and tests.
6. **Generation-History Awareness:** prior plans, generator/template versions, schema fingerprints, manifest entries, baselines, approvals and applied transactions.

### 2.2 Capabilities

1. **Incremental Scaffolding and Reconciliation:** A cross-cutting capability, compares the current application and database with their previous generation state, then creates a safe incremental generation plan.
2. **Extensible Architecture:** A cross-cutting architecture property, allows the addition of database providers, templates, UI frameworks, IDE integrations and external generators.

## 3. Design principles to evaluate

- Read-only inspection by default.
- Database-first authority for the initial mode.
- Dependency-impact analysis in response to changes to any tracked artifact.
- A probable-outcome plan before candidate code generation.
- Explicit approval before candidate preparation and separate approval before project application.
- No silent change, even for formatting, metadata or apparently insignificant updates.
- Stop/report on ambiguous, destructive or unsupported conflicts.
- Reproducible plans and generated output for equivalent inputs.
- Rollback limited to the exact approved transaction and its recorded backups.

## 4. Evaluation dimensions

### 4.1 Correctness and impact coverage

Measure whether the planner identifies all expected impacted artifacts and avoids proposing unrelated changes. Classify true positives, false positives, true negatives and false negatives by scenario.

### 4.2 Preservation and conflict handling

Introduce controlled developer modifications, then perform schema and project changes. Measure preserved customizations, detected conflicts, missed conflicts and unintended data loss. The target for silent loss of developer changes is zero.

### 4.3 Productivity and usability

Measure end-to-end task time, configuration re-entry, manual edits, review effort and conflict-resolution time. Use a structured usability instrument such as the System Usability Scale only with a documented participant protocol.

### 4.4 Performance and resource use

Measure planning time, candidate preparation time, validation time, apply time, CPU and memory. Separate planning, code generation, compilation and test execution rather than reporting a single unexplained time.

### 4.5 Reproducibility

Repeat equivalent runs with identical database snapshots, project files, configuration, package lock state, generator version and template version. Compare plan identifiers/content hashes and generated outputs.

## 5. Baselines

Use three distinct comparison conditions where applicable:

- Standard Microsoft tooling with its normal supported options.
- Microsoft-supported customization facilities, such as partial classes and T4 templates for EF Core reverse engineering.
- PASS prototype with explicit planning, approval, manifest and reconciliation.

Do not compare a deliberately weak baseline with a fully optimized PASS configuration. Give each approach equivalent requirements, time, project inputs and feature scope.

## 6. Reporting

Report scenario definitions, tool and SDK versions, hardware, operating system, database provider/version, repetitions, raw observations, exclusions, summary statistics, confidence intervals where appropriate, and threats to validity. Preserve scripts and sample inputs so another researcher can reproduce the experiment.
