# DASS/PASS: A Conceptual Framework for Deterministic, Project-Aware Scaffolding in ASP.NET Core MVC

**Author:** Rashedul Haque Ronjon
**Status:** Draft / Pre-Implementation Research Proposal

## Abstract
Scaffolding is a foundational feature of modern web frameworks, designed to accelerate the creation of CRUD (Create, Read, Update, Delete) interfaces. However, in ASP.NET Core MVC, scaffolding suffers from a "Destructive Regeneration" problem: as application requirements evolve and database schemas change, re-running the standard scaffolder overwrites custom business logic and UI modifications. This paper proposes DASS/PASS (Database/Project Aware Smart Scaffolder), a framework that introduces persistent project configuration (`dass.json`) and uses Roslyn-based Abstract Syntax Tree (AST) merging to perform intelligent, incremental code generation. DASS aims to bridge the gap between rapid prototyping and enterprise-grade iterative development.

## 1. Introduction
Microsoft’s ASP.NET Core MVC scaffolder is highly effective for initial setup but lacks "application memory." Every time a developer scaffolds a new entity, they must manually apply their established conventions (e.g., Bootstrap 5 dark mode, server-side pagination, Syncfusion grids). Furthermore, when database columns are added, the scaffolder overwrites the existing file, forcing the developer to manually re-integrate their custom logic. DASS/PASS is proposed as an intelligent wrapper that understands the database schema, the project's established conventions, and the existing codebase.

## 2. Problem Statement
The core issues with existing scaffolders include:
1. **Destructive Regeneration:** Schema changes require re-scaffolding, which destroys manual edits.
2. **Loss of Context:** Scaffolders do not remember previously selected UI themes, validation rules, or architectural patterns.
3. **Repetitive Configuration:** Developers must repeatedly select the same options (e.g., "Use Layout Page," "Generate Views") for every new table.
4. **Inconsistency:** Over time, manual re-edits lead to inconsistent UI/UX across different modules.

## 3. Proposed Solution: DASS/PASS
DASS/PASS introduces three primary innovations:
1. **Project Memory (`dass.json`):** A persistent configuration file at the project root that stores UI and architectural decisions. Subsequent scaffolds read this file automatically.
2. **Roslyn-Based Safe Regeneration:** By parsing existing C# files into SyntaxTrees, DASS can detect missing properties (new DB columns) and inject them into the existing class without deleting custom methods or properties.
3. **Incremental Scaffolding:** DASS only generates what is missing. If a controller exists, it adds missing actions. If a view exists, it updates the HTML safely.

## 4. Expected Contributions
* A fully documented, open-source architectural blueprint for smart scaffolding.
* A reference implementation for safely merging generated C# code using Roslyn.
* Empirical evidence demonstrating a reduction in developer effort and an increase in code consistency over the traditional Microsoft scaffolder.
