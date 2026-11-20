# Sample: ExistingProject.Adoption

**Status:** Planned sample; not implemented.

## Purpose

Demonstrate onboarding an existing ASP.NET Core MVC project that may have been scaffolded by Microsoft or developed manually. PASS must not assume it owns existing files.

## Required scenarios

- Inspect `.sln`, `.csproj`, package references, folders, namespaces, controllers, models, DbContext, Razor views and configuration read-only.
- Detect database/provider and schema metadata without storing secrets.
- Propose a `pass.json` profile from observed facts and explicit user choices.
- Classify artifacts as PASS-generated, developer-owned, extensible, modified-generated or adopted/unknown.
- Ask the authorized user to review and approve the adoption baseline.
- Show uncertain ownership and unsupported files as review items; never silently take ownership.

## Acceptance criteria

- Inspection makes no changes.
- Adoption planning makes no changes.
- Candidate manifest is staged separately.
- Baseline creation requires approval.
- Subsequent plans can distinguish known generated content from developer modifications.
