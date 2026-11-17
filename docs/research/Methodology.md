# Methodology & Evaluation Plan

## 1. Design Science Research (DSR)
The development of PASS follows the Design Science Research methodology, which involves creating and evaluating innovative artifacts (the PASS tool and its architecture) intended to solve identified organizational problems (destructive scaffolding).

## 2. The Six Awareness Layers
PASS is built on six interconnected awareness layers:
1. **Project Awareness:** Reading `pass.json` to understand UI themes, libraries (e.g., Syncfusion, Bootstrap), and layout choices.
2. **Database Awareness:** Parsing schema metadata (tables, foreign keys, data types, constraints, etc.) to generate accurate models.
3. **Developer Awareness:** Remembering previous choices (e.g., "The developer always prefers FluentValidation over DataAnnotations").
4. **Code Awareness:** Using Roslyn to parse existing code and ensure new generated code integrates perfectly.
5. **Application Awareness:** Ensuring new scaffolded modules use existing DI (Dependency Injection) containers and shared services.
6. **Incremental Awareness:** Comparing the DB schema to the existing code to calculate the "diff" before generating.

## 3. Proposed Evaluation Metrics (Future Empirical Study)
Once the tool is built, we will conduct a controlled experiment comparing the Microsoft Scaffolder against PASS using a medium-scale database (e.g., 20 tables).

### Quantitative Metrics:
1. **Time to Scaffold 10 Entities:** Measuring the speed of initial setup vs. subsequent setups.
2. **Regeneration Accuracy:** Developer scaffolds `Customers`, adds a `CalculateDiscount()` method. DB adds an `Email` column. We measure how many manual lines of code must be changed post-scaffold (Microsoft will require re-writing the whole method; PASS should require 0 lines).
3. **Maintainability Index (MI):** Using Visual Studio Code Metrics to compare the maintainability of generated code.
4. **Cyclomatic Complexity:** Ensuring PASS's advanced features (pagination, search) do not create overly complex, unmaintainable code.
5. **Lines of Code (LOC) Modified:** Calculating the "churn" created by standard scaffolding vs. PASS.

### Qualitative Metrics:
1. **Developer Experience (DX) Survey:** A System Usability Scale (SUS) survey completed by .NET developers using both scaffolders.
