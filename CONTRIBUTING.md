# Contributing to PASS

First off, thank you for considering contributing to PASS! We are currently in the **Research and Request for Comments (RFC)** phase. 

## How Can I Contribute Right Now?
Since the source code has not been written yet, we need your brainpower, not your keyboard!

### 1. Architectural Review (For .NET Architects)
Please review our [System Architecture](docs/architecture/SystemArchitecture.md) and [Roslyn Merging Strategy](docs/architecture/Roslyn_Merging.md). 
* Are there edge cases where Roslyn AST merging will fail (e.g., highly customized Razor views)?
* How should PASS handle complex entity relationships (e.g., many-to-many join tables)?

### 2. Answer the RFC Questions
Go to [Discussion Topics](docs/rfc/DiscussionTopics.md) and open a GitHub Issue to answer any of the questions listed there. We are particularly interested in the Developer Experience (DX).

### 3. Academic Feedback
If you are a researcher, please review our [Research Proposal](docs/research/ResearchProposal.md). Are our proposed evaluation metrics (Cyclomatic Complexity, Maintainability Index, Developer Effort) sufficient to prove the value of this tool?

## When Coding Begins
Once the architecture is finalized, we will need:
* C# developers experienced with `Microsoft.CodeAnalysis` (Roslyn).
* T4/Razor template developers.
* xUnit testing experts.

## Code of Conduct
Please be respectful and constructive in all discussions. We are building a tool to make developers' lives easier.
