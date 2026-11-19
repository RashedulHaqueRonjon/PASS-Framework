# Roslyn Strategy — PASS Code Reconciliation

This document is retained as a link target for the original architecture outline. The expanded normative design is now in [ReconciliationAndMerging.md](ReconciliationAndMerging.md).

Roslyn is proposed for supported C# syntax and semantic analysis, not as a universal merge engine for every application artifact. PASS should prefer partial classes, partial methods, EF Core customization hooks and separate developer-owned extension files. A generated file that has been manually modified must be compared with its recorded baseline and new candidate.

C# transformations require syntax and semantic validation. Razor `.cshtml`, JavaScript, TypeScript, CSS, JSON, XML/MSBuild and SQL require their own strategies. A C# syntax tree cannot safely represent the whole MVC application.

The policy is: plan first; approval before candidate generation; exact diff review; separate approval before apply; stop/report ambiguous or destructive conflicts; record a rollback-capable transaction.
