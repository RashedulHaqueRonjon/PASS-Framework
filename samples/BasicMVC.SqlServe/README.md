# Sample: BasicMVC.SqlServer

**Status:** Planned reconstruction sample; not implemented.

## Purpose

Recreate a conventional ASP.NET Core MVC database-first Customer CRUD application that can serve as the first demonstration project for PASS and as a baseline for Microsoft scaffolding comparison.

## Inputs to recover from screenshots

The repository contains PASS and Microsoft screenshot files for Customer List, Create, Edit, Details and Delete screens. Exact field names and visual details must be transcribed from the full-resolution images before the sample is finalized. Do not invent them based only on filenames.

## Planned contents

```text
BasicMVC.SqlServer/
├── Database/
│   ├── Schema.sql
│   └── SeedData.sql
├── WebApp/                 # ASP.NET Core MVC project, created in implementation phase
├── ScreenshotReferences.md
└── README.md
```

## Reconstruction procedure

1. Open the retained PASS and Microsoft screenshots and capture exact visible requirements for all five CRUD screens.
2. Record the underlying Customer table columns, SQL types, nullability, keys and constraints from the original database/project if recoverable.
3. If the database is lost, create a new documented SQL Server schema matching the confirmed screenshot fields; mark assumptions separately.
4. Create a conventional ASP.NET Core MVC database-first project using the selected .NET baseline and EF Core SQL Server provider.
5. Reproduce the Microsoft baseline using the exact documented scaffolding version/options.
6. Recreate the PASS prototype output separately using the same database, data, framework and UI assets.
7. Capture new screenshots at the same viewport and compare each screen.

## Acceptance checklist

- [ ] Customer List screen matches confirmed columns/actions.
- [ ] Create screen matches confirmed fields and validation.
- [ ] Edit screen loads and updates the correct record.
- [ ] Details screen displays the intended fields.
- [ ] Delete screen confirms the correct record and prevents accidental deletion.
- [ ] Server-side validation and anti-forgery protection work.
- [ ] Screenshots are labelled as baseline, prototype or implementation output.
