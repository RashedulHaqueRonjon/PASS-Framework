# PASS Generated-Artifact Manifest

## 1. Purpose

The manifest records provenance and reconciliation history for artifacts managed by PASS. It is needed to distinguish the previous generated baseline from the current developer-visible file and the newly proposed generated candidate.

Proposed project-local paths:

```text
.pass/
├── manifest.json
├── baselines/
├── plans/
├── transactions/
└── staging/          # temporary; normally outside the project or ignored by Git
```

The team should decide which manifest/history files are shared in source control. Baselines needed for reproducible team reconciliation must be preserved or recoverable. Temporary candidate and secret-bearing local state must not be committed.

## 2. Conceptual manifest entry

```json
{
  "manifestVersion": 1,
  "artifactId": "mvc:Customer:entity",
  "path": "Models/Customer.g.cs",
  "artifactType": "CSharpEntity",
  "owner": "pass-generated",
  "generator": "PASS.Generators.Mvc",
  "generatorVersion": "0.1.0-conceptual",
  "templateId": "entity-sqlserver-default",
  "templateVersion": "1",
  "schemaFingerprint": "sha256:illustrative-only",
  "baselineHash": "sha256:illustrative-only",
  "lastAppliedTransaction": null,
  "dependencies": [
    "database:dbo.Customer",
    "configuration:pass.json"
  ]
}
```

Values above are illustrative; no runtime manifest format is implemented.

## 3. Ownership classes

- **PASS-generated:** generated and managed by PASS; compare with baseline before replacement.
- **Developer-owned:** manually maintained; PASS must not overwrite.
- **Extensible:** generated shell with explicit, documented extension points or separately owned partial/custom files.
- **Modified-generated:** a PASS-generated artifact whose current content differs from its baseline; reconcile or report conflict.
- **Adopted/unknown:** an existing artifact registered during adoption; ownership and baseline confidence must be reviewed.

Ownership is evidence, not permission to destroy. A generated marker alone is not sufficient to overwrite a file if the current content has unapproved changes.

## 4. Hashes and fingerprints

Record hashes for the previous baseline and relevant current inputs. Normalize only what is formally specified; do not hash a normalized representation if doing so would hide meaningful source changes. Include schema, configuration, generator and template versions in plan reproducibility metadata.

## 5. Retention and security

Do not store secrets or full connection strings. Baseline retention must be documented. Transactions must record changed paths, pre-change hashes, backup locations, candidate hashes, approvals, validation results and rollback status. Access to transaction records should follow project permissions.
