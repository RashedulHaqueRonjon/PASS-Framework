# PASS Community Discussion Topics

This list invites specific technical feedback during the conceptual/RFC phase.

## 1. Microsoft tooling and research baseline

- Which exact EF Core reverse-engineering operations should be compared?
- Which MVC controller/view scaffolding workflows should be tested separately?
- Which Microsoft-supported customization facilities should be included in the strongest baseline?

## 2. Database-first authority

- What metadata is essential for a SQL Server-first MVP?
- How should the planner report drift between live schema, EF Core model snapshot and existing entities?
- Which database changes require explicit manual mapping, such as a rename or type conversion?

## 3. Dependency-impact graph

- Which edges can be inferred from code, project files and templates?
- Which relationships require a developer-supplied declaration?
- How should the graph represent impact from a controller, Razor view, client script or package change?
- What evidence should be shown for an artifact marked affected or unaffected?

## 4. Approval and rollback

- Is the two-gate workflow (approve staging, then approve exact diff/application) sufficiently clear?
- How should authorized approvers be represented for local and CI usage?
- What backup retention and transaction journal format are practical?
- Which failures should trigger a pre-authorized automatic rollback?

## 5. Generated code and Razor

- Which files should be generated-only, developer-owned or extensible?
- Which C# changes can be safely handled with Roslyn and partial classes?
- Which Razor component/partial patterns are most maintainable?
- How should manually deleted generated artifacts be treated?

## 6. Configuration and ecosystem

- Which shared settings belong in `pass.json`?
- Which project facts should always be detected from `.csproj`/MSBuild rather than duplicated?
- Which optional UI libraries should have adapters?
- How should templates and providers be versioned and trusted?

## 7. Research evaluation

- Which impact precision/recall and preservation tests are essential?
- How should developer time and manual intervention be measured fairly?
- What sample databases and schema-evolution scenarios are representative?
- Which threats to validity should be addressed?
