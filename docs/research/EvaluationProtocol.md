# Evaluation Protocol

**Status:** Planned protocol template. Execute only after a prototype and baseline environments exist.

## 1. Experimental questions

Evaluate configuration reuse, impact-analysis completeness, regeneration safety, conflict detection, approval workflow usability, total developer effort and reproducibility.

## 2. Experimental environment to record

For every run, record:

- Operating system and edition/build.
- CPU, memory and storage.
- .NET SDK/runtime, ASP.NET Core, EF Core and Roslyn versions.
- Visual Studio version where applicable.
- SQL Server edition/version and compatibility level.
- Database provider and connection mode.
- Git commit, PASS version, template version and package lock state.
- Exact commands, settings, database snapshot and project state.

## 3. Required comparison groups

A. Relevant Microsoft default workflow.  
B. Microsoft workflow plus applicable supported customization mechanisms.  
C. PASS prototype.

Run EF Core reverse engineering and MVC controller/view scaffolding as separate test tracks when appropriate. Record flags such as overwrite/force and template customizations. Do not generalize an outcome from one workflow to all Microsoft scaffolding.

## 4. Scenario suite

| ID | Scenario | Expected observation |
|---|---|---|
| S01 | First project initialization | Read-only inspection; proposed profile; no write until approved. |
| S02 | Add a second entity | Existing approved conventions are reused. |
| S03 | Add a database column | Plan identifies dependent entity, mapping, view model, controller, Razor, script and tests as applicable. |
| S04 | Rename a database column | Rename ambiguity is reported; no destructive application without explicit mapping/approval. |
| S05 | Change data type/nullability | Compatibility and validation impacts are reported. |
| S06 | Add/remove foreign key | Relationship-dependent artifacts are identified. |
| S07 | Developer modifies generated C# | Baseline/user/new-output three-way comparison detects custom change. |
| S08 | Developer modifies Razor | Razor-specific reconciliation or conflict; no Roslyn-only assumption. |
| S09 | Change a shared PASS feature | All modules using that setting are impact-analysed. |
| S10 | Change controller route/action | Relevant links, scripts, route consumers and tests are examined; database is not changed by implication. |
| S11 | Change project dependency | Affected generators/build outputs and compatibility are identified. |
| S12 | Repeat identical operation | Idempotency and deterministic output are assessed. |
| S13 | Adopt pre-existing scaffold | Baseline and ownership classifications require review/approval. |
| S14 | Introduce unresolved conflict | Operation stops and reports; no project mutation. |
| S15 | Simulate apply failure | Approved rollback/restore procedure is verified. |

## 5. Metrics and definitions

- **Impact recall:** expected impacted artifacts correctly identified / all expected impacted artifacts.
- **Impact precision:** correctly identified impacted artifacts / all artifacts identified as impacted.
- **Preservation rate:** intentionally preserved developer changes / all developer changes marked for preservation.
- **Conflict recall:** known conflicts detected / all injected conflicts.
- **Silent-loss count:** developer changes lost without explicit approval; target is zero.
- **Plan accuracy:** predicted operations and risks compared with the final staged diff and observed apply result.
- **Task time:** wall-clock and active developer time, reported separately.
- **Manual intervention:** count and duration of required manual edits/resolutions.
- **Reproducibility:** proportion of repeated identical-input runs producing equivalent plans and outputs.
- **Build/test outcome:** compilation and relevant functional/security test results after application.

- ## 6. Repetition and analysis

Use repeated runs sufficient to characterize variability. Report median, interquartile range and/or mean and standard deviation as suitable. Select inferential tests only after considering sample size, distribution and paired/unpaired design. For developer studies, justify participant recruitment and sample size, obtain appropriate consent, and document survey instruments.

## 7. Validity controls

- Use the same baseline project and schema snapshots.
- Give each approach equivalent requirements and feature settings.
- Separate tool execution time from build and test time.
- Preserve raw logs and output diffs.
- Predefine expected affected artifacts before running each test.
- Include negative tests and intentionally ambiguous changes.
- Disclose unsupported features and excluded runs.

## 8. Results template

No result should be entered without evidence. For each scenario record: input revision, expected impact set, observed impact set, plan, approved actions, final diff, build/test outcome, conflicts, lost changes, time, resource use and notes.
