# PASS Benchmarking Plan

**Status:** Planned; no benchmark results are available.

## 1. Separate time measurements

Record separately:

- Read-only inspection time.
- Dependency graph and plan generation time.
- Candidate generation time after approval.
- Reconciliation/diff time.
- Build and test validation time.
- Human review and approval time.
- Apply and rollback time.
- Total end-to-end elapsed time and active developer time.

## 2. Performance measures

Measure median and variability for elapsed time, CPU, peak memory, file count, total bytes processed and graph size. Test increasing numbers of entities and dependency edges. Include cold and warm runs and state the cache policy.

## 3. Quality measures

Performance must be interpreted alongside impact precision/recall, preservation rate, conflict recall, false positives, false negatives, silent-loss count, build success and functional-test success. A faster run that silently loses customization is a failure.

## 4. Reproducibility

Pin SDK, package, generator and template versions. Use the same database snapshot, machine/environment and project state for comparisons. Publish the scripts, raw data, environment description and analysis method. Do not publish fabricated or illustrative timings as experimental results.
