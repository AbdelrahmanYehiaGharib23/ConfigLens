# ConfigLens

> A .NET developer tool that makes configuration resolution transparent.

## The Problem

In .NET applications, configuration values can come from multiple sources:

* `appsettings.json`
* `appsettings.{Environment}.json`
* Environment Variables
* User Secrets
* Command-line arguments
* Other configuration providers

When the same configuration key exists in multiple sources, it can be difficult for developers to understand:

* Where the final value came from
* Which source overrode another source
* Why a specific value was selected
* Whether the same configuration exists in multiple places

Developers can see the final configuration value, but they may not always know **why that value won**.

## The Idea

**ConfigLens** is a developer tool for .NET applications that analyzes configuration sources and explains how the final configuration value was resolved.

Instead of showing only:

```text
ConnectionStrings:DefaultConnection
= <final value>
```

ConfigLens aims to show:

```text
ConnectionStrings:DefaultConnection

appsettings.json
        ↓
    Value A

appsettings.Development.json
        ↓
    Value B

Environment Variable
        ↓
    Value C

-------------------------
Final Value: Value C
Winner: Environment Variable
```

This gives developers a clear **Configuration Resolution Trace**.

## Core Features

### Configuration Resolution

Show the final value of a configuration key and the source that provided it.

### Override Chain

Show how different configuration sources override each other.

### Configuration Conflict Detection

Detect keys that are defined in multiple configuration sources and highlight potential conflicts.

### Configuration Source Explorer

Allow developers to inspect configuration keys and their origins.

## Example

Given:

```json
// appsettings.json
{
  "Redis": {
    "ConnectionString": "localhost:6379"
  }
}
```

and:

```json
// appsettings.Development.json
{
  "Redis": {
    "ConnectionString": "localhost:6380"
  }
}
```

ConfigLens could explain:

```text
Redis:ConnectionString

Defined in:
✓ appsettings.json
✓ appsettings.Development.json

Final Source:
appsettings.Development.json

Reason:
Development configuration overrides the base configuration.
```

## Planned MVP

The first version will focus on:

1. Reading configuration sources
2. Flattening configuration keys
3. Resolving final values
4. Identifying the source of each value
5. Displaying the override chain
6. Detecting duplicate/conflicting configuration keys

## Planned Technologies

* C#
* .NET
* ASP.NET Core
* `IConfiguration`
* Configuration Providers
* JSON
* CLI
* Unit Testing

## Future Ideas

Possible future extensions include:

* Docker environment analysis
* Git integration
* Azure configuration support
* Configuration diff between environments
* Secret detection
* Configuration impact analysis
* Web dashboard

## Project Status

**Idea / Planning**

The project is currently in the planning stage. The repository will be used to define the problem, MVP, architecture, and implementation roadmap before development begins.

## Goal

ConfigLens aims to make configuration behavior easier to understand and debug for .NET developers.

> **Don't just show the configuration value. Explain why it is the value.**
