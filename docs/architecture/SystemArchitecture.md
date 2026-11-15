# System Architecture

DASS/PASS is designed as a cross-platform .NET CLI tool (`dotnet dass`) with an accompanying Visual Studio Extension (VSIX) that acts as a UI wrapper.

## Core Components

```text
[ VSIX / CLI Input ]
         │
         ▼
┌───────────────────────────────────────────────┐
│             DASS.Core Engine                  │
│                                               │
│  [1. Configuration Manager]                   │
│      - Reads/Writes `dass.json`               │
│                                               │
│  [2. Database Analyzer]                       │
│      - Reads EF Core Models / SQL Schema      │
│      - Detects new columns (e.g., `Email`)    │
│                                               │
│  [3. Code Analyzer (Roslyn)]                  │
│      - Parses existing `Customer.cs`          │
│      - Identifies custom methods              │
│                                               │
│  [4. Generation Engine]                       │
│      - Loads T4/Razor templates               │
│      - Applies `dass.json` themes (Dark Mode) │
│                                               │
│  [5. Merge Engine]                            │
│      - AST diffing and safe injection         │
└───────────────────────────────────────────────┘
         │
         ▼
[ Generated / Updated Files: Models, Controllers, Views, DB Context ]
