# RFC-0001: Project Aware Smart Scaffolder (PASS)

- **Status:** Draft
- **Author:** Rashedul Haque Ronjon
- **Created:** 2024
- **Target Audience:** .NET Architects, Senior Developers, Open Source Contributors

## 1. Summary
This RFC proposes PASS, a smart scaffolding tool for ASP.NET Core that uses persistent project configuration (`pass.json`) and Roslyn AST merging to prevent the destruction of custom code during database schema changes.

## 2. Motivation
The current Microsoft scaffolder is destructive. It forces developers to choose between the speed of scaffolding and the safety of manually writing code. As applications scale, this friction costs thousands of developer hours.

## 3. Detailed Design
Please refer to the following documents in this repository:
- [System Architecture](../architecture/SystemArchitecture.md)
- [Roslyn Merging Strategy](../architecture/Roslyn_Merging.md)

## 4. Unresolved Questions & Call for Feedback
We are seeking feedback from the .NET community on the following:
1. **Razor Views:** How should PASS handle complex customizations in `.cshtml` files? Is using Partial Views strictly for form fields a viable workaround?
2. **EF Core Migrations:** Should PASS integrate with EF Core Migrations, or should it only read the final DB state?
3. **Configuration Conflict:** If a developer changes the theme in `pass.json`, should PASS update all previously scaffolded views, or only new ones?
