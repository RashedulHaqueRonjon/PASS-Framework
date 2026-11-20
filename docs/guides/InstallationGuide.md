# PASS Installation Guide (Future)

**Status:** Planning only. No PASS package or executable has been published.

## 1. Planned prerequisites

- A supported .NET SDK selected by the implementation's `global.json`.
- An ASP.NET Core MVC target project.
- SQL Server access sufficient for read-only metadata discovery.
- EF Core packages/provider versions compatible with the target application.
- Optional Visual Studio support only after the VSIX project and compatibility matrix exist.

## 2. Framework baseline

The current proposal uses .NET 10 LTS as the primary implementation baseline. .NET 11 STS may be tested separately. Recheck the official lifecycle, SDK feature band, Visual Studio and OS support before development or release. The `global.json` in this pack selects the .NET 10 SDK line with `latestFeature` roll-forward.

**Windows note:** Microsoft's current installation matrix may restrict .NET 10/11 support on Windows 10 to specified LTSC/Enterprise editions. Check the exact Windows edition and current compatibility matrix; a supported Windows 11 development environment may be necessary.

## 3. Future installation flow

After an actual package is released, this guide will document package ID, local/global tool installation, version pinning, update/uninstall, project initialization and secure connection configuration. Do not attempt installation using the proposed command examples before a package exists.
