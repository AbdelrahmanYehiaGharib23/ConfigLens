# ConfigLens

## Configuration Explainability Tool for .NET

ConfigLens is a developer-focused CLI tool that explains where an ASP.NET Core configuration value comes from and why it became the effective runtime value.

## Problem

ASP.NET Core applications can load configuration from multiple sources, such as:

* `appsettings.json`
* `appsettings.{Environment}.json`
* Environment Variables
* User Secrets
* Command Line Arguments

When the final configuration value is different from what a developer expects, it can be difficult to determine which source provided the value and which source overrode another.

This can lead to time-consuming debugging, especially when the application works differently between development, testing, and production environments.

## Proposed Solution

ConfigLens provides an explanation for a configuration key instead of only displaying its final value.

For example:

```text
configlens explain "ConnectionStrings:DefaultConnection"
```

Possible output:

```text
Configuration Key:
ConnectionStrings:DefaultConnection

Effective Value:
Server=ProductionServer

Source:
Environment Variables

Other Values:

appsettings.json
    Server=LocalServer

Environment Variables
    Server=ProductionServer

Explanation:
The Environment Variable overrides the value
provided by appsettings.json.
```

## Main Goal

The main goal of ConfigLens is to answer three questions:

1. What is the final configuration value?
2. Where did this value come from?
3. Why did this source become the effective source?

## MVP Features

* Explain a specific configuration key.
* Detect available configuration sources.
* Display the value provided by each source.
* Identify the effective value.
* Explain which source overrides another source.
* Provide a simple CLI interface.

## Example Commands

```bash
configlens explain "ConnectionStrings:DefaultConnection"
```

```bash
configlens explain "Logging:LogLevel:Default"
```

## Future Features

* Watch configuration changes in real time.
* Export results as JSON.
* Generate HTML diagnostic reports.
* Visualize configuration precedence.
* Add CI/CD integration.
* Add VS Code integration.
* Support additional .NET configuration scenarios.

## Target Users

* .NET Developers
* Backend Developers
* Full Stack Developers
* DevOps Engineers
* Teams working with multiple environments

## Expected Benefits

ConfigLens can reduce the time developers spend investigating unexpected configuration behavior.

Instead of manually checking multiple configuration sources, developers can use one command to understand the final value and its origin.

This can be particularly useful when troubleshooting:

* Different behavior between developers' machines.
* Development vs production configuration.
* Environment variables overriding configuration files.
* Unexpected connection strings.
* Logging configuration issues.
* Missing or overridden application settings.

## Technology

The initial implementation is planned with:

* C#
* .NET
* .NET CLI
* ASP.NET Core Configuration APIs

## Project Status

This project is currently at the idea and design stage.

The initial goal is to build a small Proof of Concept and validate the configuration tracing approach before expanding the tool.

## License

To be decided during implementation.
