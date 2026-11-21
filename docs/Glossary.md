
# PASS Glossary and Technical Terminology

**Project:** PASS — Project Aware Smart Scaffolder

**Document status:** Conceptual research and architecture reference.

This glossary defines technical abbreviations, specialist terminology and PASS-specific concepts used throughout the repository.

Its purpose is to maintain consistent terminology and make the research, architecture and implementation documentation accessible to readers with different technical backgrounds.

## A. Acronyms and Abbreviations

| Term | Full Form | Definition |
|---|---|---|
| .NET | .NET Platform | Microsoft's development platform for building and running applications and services. |
| C# | C Sharp | A programming language commonly used for developing .NET applications. |
| HTML | HyperText Markup Language | The standard markup language for structuring web content. |
| MSBuild | Microsoft Build Engine | The build platform used by .NET projects to evaluate project files and execute build processes. |
| NuGet | NuGet Package Manager | The package-management system used by .NET projects to consume and distribute libraries. |
| T4 | Text Template Transformation Toolkit | A template-based code-generation technology used in Visual Studio and supported .NET development workflows. |
| YAML | YAML Ain't Markup Language | A human-readable data serialization format commonly used for configuration files and CI/CD workflows. |
| DSR | Design Science Research | A research approach focused on designing, developing and evaluating artifacts to address practical problems. |
| ADR | Architecture Decision Record | A document recording an important architectural decision, its context and consequences. |
| API | Application Programming Interface | A defined interface through which software components communicate. |
| AST | Abstract Syntax Tree | A tree representation of source-code syntax used for analysis and transformation. |
| CI | Continuous Integration | Automated validation of code and repository changes. |
| CI/CD | Continuous Integration / Continuous Delivery (or Deployment) | Practices for automating software integration, testing and delivery. |
| CLI | Command-Line Interface | A text-based interface for executing commands and interacting with software. |
| CRUD | Create, Read, Update, Delete | The four fundamental data-management operations. |
| CSS | Cascading Style Sheets | A language used to define the presentation and visual appearance of web pages. |
| DDL | Data Definition Language | SQL statements used to define or modify database structures, such as tables and indexes. |
| DTO | Data Transfer Object | An object used to transfer data between application layers or systems. |
| EF Core | Entity Framework Core | Microsoft's cross-platform object-relational mapper for .NET. |
| IDE | Integrated Development Environment | Software providing facilities for writing, building, debugging and managing applications. |
| JSON | JavaScript Object Notation | A structured text format commonly used for configuration and data exchange. |
| LTS | Long-Term Support | A software release-support designation providing an extended support period. |
| MVC | Model-View-Controller | An architectural pattern separating application data, presentation and request-handling responsibilities. |
| MVP | Minimum Viable Product | The smallest implementation that contains sufficient functionality to demonstrate and evaluate the central value proposition of a proposed product. |
| ORM | Object-Relational Mapper | A technology that maps relational database structures to programming-language objects. |
| RFC | Request for Comments | A document proposing a design or specification for review and discussion. |
| SDK | Software Development Kit | A collection of tools and libraries used to develop software for a particular platform. |
| SQL | Structured Query Language | A language used to define, query and manipulate relational databases. |
| STS | Standard Term Support | A release-support designation with a shorter support period than LTS. |
| UI | User Interface | The visual and interactive elements through which users interact with an application. |
| VSIX | Visual Studio Extension | A package format used to distribute and install extensions for Microsoft Visual Studio. |
| XML | Extensible Markup Language | A structured markup format used for configuration and data representation. |

## B. Microsoft and .NET Technologies

### ASP.NET Core

A cross-platform framework for building web applications, APIs and services using .NET.

### Entity Framework Core (EF Core)

An object-relational mapper that enables .NET applications to work with relational databases through entities, contexts and database mappings.

### Microsoft Scaffolding

Microsoft-provided tooling for generating application code, database models, controllers and views from supported project and database inputs.

### Roslyn

The .NET compiler platform providing C# and Visual Basic language parsing, syntax analysis, semantic analysis and code-transformation capabilities.

### Razor

A templating syntax used in ASP.NET Core to generate dynamic HTML through `.cshtml` files.

### Visual Studio Extension (VSIX)

A distributable extension package that integrates additional functionality into Microsoft Visual Studio.

## C. Software Architecture and Code Generation

### Artifact

A software development output or component, including source files, database objects, configuration files, generated code, views, scripts and tests.

### Baseline

A recorded reference state of an artifact or project used to identify subsequent changes.

### Candidate Generation

The preparation of proposed generated files in an isolated staging environment before their application to the target project.

### Code Awareness

The ability of PASS to analyse source code, syntax, symbols, dependencies, existing customizations and generated-code ownership.

### Dependency Graph

A representation of relationships between project artifacts that supports forward and reverse dependency analysis.

### Deterministic Generation

Generation in which equivalent inputs and pinned generator/template versions are expected to produce equivalent outputs.

### Diff

A comparison showing the differences between two versions of a file, configuration or other artifact.

### Generated-Artifact Provenance

Recorded information identifying which generator, template, configuration and input state produced an artifact.

### Incremental Scaffolding

The generation or updating of selected application components without unnecessarily regenerating unrelated components or restarting the entire scaffolding configuration process.

### Manifest

A structured record containing information about generated artifacts, their ownership, source inputs, versions, baselines and generation history.

### Reconciliation

The process of comparing generated candidates with existing project artifacts and determining how proposed changes can be applied while preserving developer-owned modifications.

### Rollback

The controlled restoration of the previously recorded state following an approved operation, subject to the availability and validity of recovery data.

### Staging

An isolated workspace in which candidate changes are generated and reviewed before they are applied to the actual project.

### Source of Truth

The designated authoritative source for a particular category of information.

For example, in PASS database-first mode, the live SQL Server schema is authoritative for database structure.

## D. PASS-Specific Concepts

### DASS

Database Aware Smart Scaffolder, an earlier working name associated with the project. PASS (Project Aware Smart Scaffolder) is the current project name.

### Developer/Preference Awareness

The ability of PASS to retain and reuse explicitly selected developer preferences without confusing personal preferences with shared team configuration.

### Generation-History Awareness

The ability of PASS to use previous generation records, manifests, baselines, approvals and transaction history when analysing subsequent scaffolding operations.

### Impact Analysis

The process of identifying project artifacts that may be affected by a proposed change to a database object, source file, project setting or dependency.

### Project Memory

The persistent record of approved project-wide scaffolding conventions and preferences, primarily maintained through `pass.json`.

### PASS Profile

The versioned, project-level configuration file that stores PASS-specific generation preferences and policies.

### Approval Gate

A mandatory authorization checkpoint before a particular stage of an operation can proceed.

PASS uses separate approval gates for candidate preparation and application of reviewed changes.

### Probable-Outcome Report

A report describing the anticipated changes, affected artifacts, risks, assumptions, dependencies and potential conflicts before candidate generation.

### Database-First Mode

A development approach in which the existing live database schema is the authoritative source for database structure and the application models are generated or derived from it.

### Migrations-First Mode

A development approach in which EF Core models and migration history are designated as the authoritative source for intended database structure. This is a potential future PASS capability, not part of the initial supported mode.

---

## E. Terminology and Usage Conventions

1. Use **PASS** consistently when referring to Project Aware Smart Scaffolder.
2. Use `pass.json` when referring to the PASS project configuration file.
3. Use **Code Awareness**, not Logic Awareness, for the current architecture.
4. Use **database-first** when referring to the initial supported source-of-truth mode.
5. Use **candidate generation** for generating proposed outputs in isolated staging.
6. Use **application** when referring to applying approved candidate changes to the target project.
7. Use **reconciliation** when referring to the comparison and controlled integration of generated and existing artifacts.
8. Distinguish proposed capabilities from implemented and experimentally verified capabilities.

## F. Document Maintenance

This glossary should be updated whenever new architectural concepts, technologies, abbreviations or PASS-specific terminology are introduced.

Definitions should remain consistent across the README, research proposal, RFC, architecture specifications, developer guides and implementation documentation.
