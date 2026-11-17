# Roslyn Merging Strategy (Safe Regeneration)

The most critical feature of PASS is preventing the destruction of custom code. We will use the .NET Compiler Platform (Roslyn) to achieve this.

## The Problem
If a developer scaffolds `Customer.cs`, they might add:
```csharp
public class Customer {
    public int Id { get; set; }
    public string Name { get; set; }
    
    // Custom Logic
    public string GetFullTitle() {
        return $"Customer: {Name}";
    }
}
