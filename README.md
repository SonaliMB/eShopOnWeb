# eShopOnWeb — ASP.NET Core Web Application & Software Quality Engineering

[![.NET 8](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet\&logoColor=white)](https://dotnet.microsoft.com/)
[![ASP.NET Core](https://img.shields.io/badge/ASP.NET%20Core-8.0-512BD4?logo=dotnet\&logoColor=white)](https://learn.microsoft.com/aspnet/core/)
[![C#](https://img.shields.io/badge/C%23-12-239120?logo=csharp\&logoColor=white)](https://learn.microsoft.com/dotnet/csharp/)
[![Docker](https://img.shields.io/badge/Docker-Supported-2496ED?logo=docker\&logoColor=white)](https://www.docker.com/)
[![Azure](https://img.shields.io/badge/Azure-Deployment%20Support-0078D4?logo=microsoftazure\&logoColor=white)](https://azure.microsoft.com/)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?logo=githubactions\&logoColor=white)](https://github.com/features/actions)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Overview

**eShopOnWeb** is an ASP.NET Core reference application demonstrating a single-process web application architecture and deployment model.

This repository is based on the **Microsoft eShopOnWeb reference application** and retains its original application purpose and architecture. It provides an example of building a web application with ASP.NET Core, application/domain separation, Entity Framework Core, ASP.NET Core Identity, a public API, Blazor-based administration functionality, automated tests, Docker support, and Azure deployment resources.

The repository is also organized to make the application's **testing, automation, CI/CD, and engineering practices** easier to understand and evaluate.

> **Attribution:** The underlying eShopOnWeb application is a Microsoft reference application. This repository should not be interpreted as an original implementation of the eShopOnWeb application by the repository owner.

---

## What This Project Demonstrates

The repository provides a practical example of a modern .NET web application's structure, including:

* ASP.NET Core web application development
* C# application development
* Separation of application/domain concerns and infrastructure
* Entity Framework Core
* ASP.NET Core Identity
* Public API implementation
* Blazor administration components
* Unit testing
* Integration testing
* Functional testing
* Public API integration testing
* Docker-based execution
* Development container support
* Azure infrastructure definitions
* GitHub Actions workflows
* Centralized NuGet package management

The repository contains separate source and test projects rather than placing the entire application in a single project.

---

## Technology Stack

| Area                    | Technology                                 |
| ----------------------- | ------------------------------------------ |
| Language                | C#                                         |
| Framework               | ASP.NET Core 8.0                           |
| Runtime                 | .NET 8                                     |
| Web                     | ASP.NET Core MVC / Web                     |
| API                     | ASP.NET Core Web API                       |
| UI / Administration     | Blazor                                     |
| ORM                     | Entity Framework Core                      |
| Authentication          | ASP.NET Core Identity                      |
| Database                | SQL Server / Entity Framework Core         |
| Testing                 | .NET test projects                         |
| Containerization        | Docker / Docker Compose                    |
| Cloud                   | Microsoft Azure                            |
| Infrastructure          | Azure infrastructure files / Bicep         |
| CI/CD                   | GitHub Actions                             |
| Package Management      | Central NuGet Package Management           |
| Development Environment | Dev Containers / GitHub Codespaces support |

The `main` branch targets ASP.NET Core 8.0, and the solution contains separate projects for the web application, infrastructure, public API, Blazor components, and multiple test layers.

---

# Architecture

The application follows a layered structure that separates core application concerns from infrastructure and presentation concerns.

```text
                         ┌───────────────────────┐
                         │       Web Application  │
                         │   ASP.NET Core / MVC   │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │    ApplicationCore    │
                         │ Entities / Interfaces │
                         │ Services / Specs      │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │    Infrastructure     │
                         │ EF Core / Identity    │
                         │ Data Access            │
                         └───────────┬───────────┘
                                     │
                                     ▼
                              ┌──────────────┐
                              │   Database   │
                              └──────────────┘


       ┌───────────────────┐
       │    Public API     │
       └───────────────────┘

       ┌───────────────────┐
       │   Blazor Admin    │
       └───────────────────┘
```

The source solution currently contains:

* `ApplicationCore`
* `Infrastructure`
* `Web`
* `PublicApi`
* `BlazorAdmin`
* `BlazorShared`

as well as separate testing projects.

---

# Project Structure

```text
eShopOnWeb/
│
├── .ado/
├── .devcontainer/
├── .github/
│   └── workflows/
│
├── .images/
├── .vscode/
│
├── infra/
│
├── src/
│   ├── ApplicationCore/
│   ├── BlazorAdmin/
│   ├── BlazorShared/
│   ├── Infrastructure/
│   ├── PublicApi/
│   └── Web/
│
├── tests/
│   ├── FunctionalTests/
│   ├── IntegrationTests/
│   ├── PublicApiIntegrationTests/
│   └── UnitTests/
│
├── .dockerignore
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CodeCoverage.runsettings
├── Directory.Packages.props
├── docker-compose.yml
├── docker-compose.override.yml
├── docker-compose-webapp.yml
├── eShopOnWeb.sln
├── global.json
├── LICENSE
├── MTT-Notes.md
├── README.md
└── azure.yaml
```

This structure reflects the current repository rather than introducing an artificial project structure.

---

# Application Projects

## ApplicationCore

Contains core application/domain concerns used by the solution.

The project is intended to remain independent of infrastructure-specific implementation details.

## Infrastructure

Contains infrastructure-related implementation, including persistence and application infrastructure.

Entity Framework Core is used for data access.

## Web

Contains the primary ASP.NET Core web application.

Most of the application's user-facing functionality is available through this project.

## PublicApi

Provides the application's public API used by other parts of the solution, including the administration functionality.

## BlazorAdmin

Contains the Blazor-based administration functionality.

The administration area communicates with the application's server through the Public API.

## BlazorShared

Contains shared Blazor components and supporting code.

---

# Test Strategy

One of the useful aspects of this repository is that testing is separated into multiple projects.

```text
                         Test Strategy
                              │
              ┌───────────────┼────────────────┐
              │               │                │
              ▼               ▼                ▼
        Unit Tests      Integration Tests   API Tests
              │               │                │
              └───────────────┼────────────────┘
                              │
                              ▼
                       Functional Tests
```

## Unit Tests

Location:

```text
tests/UnitTests
```

Used for testing application behavior in an isolated manner.

## Integration Tests

Location:

```text
tests/IntegrationTests
```

Used for testing interactions between application components and infrastructure.

## Public API Integration Tests

Location:

```text
tests/PublicApiIntegrationTests
```

Provides a dedicated test project for API integration scenarios.

## Functional Tests

Location:

```text
tests/FunctionalTests
```

Provides functional-level testing of the web application.

The solution file explicitly includes all four test projects.

> **Note:** This README intentionally does not publish a test count, pass percentage, code coverage percentage, or quality metric because those values should only be reported from an actual test execution.

---

# CI/CD

The repository contains GitHub Actions workflows under:

```text
.github/workflows/
```

The workflows include build/test and deployment-related automation.

The repository also contains Azure deployment resources and configuration, allowing the application to be used with Azure deployment workflows.

CI/CD-related components should be viewed together with:

```text
.github/workflows/
infra/
azure.yaml
```

The existing repository includes a GitHub Actions workflow for the eShopOnWeb build/test and deployment process.

> **Important:** The presence of workflow definitions does not by itself guarantee that every workflow currently succeeds in every environment. Workflow status should be verified through the GitHub Actions tab for the current commit.

---

# Docker Support

The repository includes Docker and Docker Compose configuration.

Relevant files include:

```text
docker-compose.yml
docker-compose.override.yml
docker-compose-webapp.yml
.dockerignore
```

The application can be built and started using Docker Compose from the repository root.

```bash
docker-compose build
docker-compose up
```

The existing configuration exposes the Web application and Public API on the ports documented by the original project.

---

# Development Container

The repository contains a `.devcontainer` configuration.

This can be used with:

* Visual Studio Code Dev Containers
* GitHub Codespaces
* compatible development-container environments

The development container is intended to provide a configured development environment without requiring every project dependency to be installed directly on the host machine.

---

# Running Locally

## Prerequisites

The current project targets **ASP.NET Core 8.0 / .NET 8**.

Depending on the selected execution method, you may also need:

* .NET 8 SDK
* SQL Server, or the configured in-memory database option
* Entity Framework Core tooling
* Docker Desktop, if using Docker
* Azure Developer CLI (`azd`), if deploying through Azure Developer CLI

---

## Clone the Repository

```bash
git clone https://github.com/SonaliMB/eShopOnWeb.git
cd eShopOnWeb
```

---

## Restore Dependencies

```bash
dotnet restore
```

The repository uses central NuGet package management through:

```text
Directory.Packages.props
```

---

# Database Configuration

The application supports a persistent database configuration using SQL Server.

The original project documentation also describes an in-memory database option.

For the in-memory configuration, the Web application's `appsettings.json` can contain:

```json
{
  "UseOnlyInMemoryDatabase": true
}
```

For SQL Server usage, configure the appropriate connection strings in the application's configuration.

Do not commit passwords, tokens, or other sensitive credentials to the repository.

---

# Entity Framework Core Database Setup

From the Web project directory, the original application documentation provides the following migration commands:

```bash
dotnet tool restore

dotnet ef database update \
  -c catalogcontext \
  -p ../Infrastructure/Infrastructure.csproj \
  -s Web.csproj

dotnet ef database update \
  -c appidentitydbcontext \
  -p ../Infrastructure/Infrastructure.csproj \
  -s Web.csproj
```

These migrations create the application's catalog/cart database and identity database.

The first application startup also seeds the database with sample data.

---

# Run the Application

The application can be run locally using the Web project.

From:

```text
src/Web
```

run:

```bash
dotnet run --launch-profile Web
```

The Public API project also needs to be running for administration functionality.

From:

```text
src/PublicApi
```

run:

```bash
dotnet run
```

The original application documentation describes the Web application as available at:

```text
https://localhost:5001/
```

with the administration area at:

```text
https://localhost:5001/admin
```

The exact local URL can vary depending on the launch profile and local environment.

---

# Running Tests

The solution contains separate test projects for:

```text
tests/UnitTests
tests/IntegrationTests
tests/PublicApiIntegrationTests
tests/FunctionalTests
```

To restore and build the solution:

```bash
dotnet restore
dotnet build --no-restore
```

To execute the complete test suite:

```bash
dotnet test
```

For more targeted execution, individual test projects can be executed directly, for example:

```bash
dotnet test tests/UnitTests/UnitTests.csproj
```

```bash
dotnet test tests/IntegrationTests/IntegrationTests.csproj
```

```bash
dotnet test tests/PublicApiIntegrationTests/PublicApiIntegrationTests.csproj
```

```bash
dotnet test tests/FunctionalTests/FunctionalTests.csproj
```

> Test results should be taken from the actual execution environment. This README intentionally does not state that all tests currently pass because that has not been independently verified as part of this README update.

---

# Code Coverage

The solution includes:

```text
CodeCoverage.runsettings
```

which is included as a solution item.

This provides configuration that can be used when collecting coverage information.

Coverage percentages are intentionally not published here unless they have been generated from an actual test run.

---

# Azure Deployment

The repository contains Azure-related deployment resources, including:

```text
infra/
azure.yaml
```

The original eShopOnWeb documentation also supports deployment using the Azure Developer CLI (`azd`).

Typical Azure Developer CLI commands include:

```bash
azd auth login
azd init
azd up
```

Deployment requires an appropriately configured Azure subscription and environment.

Do not place Azure credentials, secrets, or private configuration values directly in source control.

---

# Engineering Practices Demonstrated

The repository provides examples of several software engineering practices:

### Application Architecture

* Layered application structure
* Separation of application and infrastructure concerns
* Dependency-based project organization

### Testing

* Unit testing
* Integration testing
* API integration testing
* Functional testing

### Development

* Centralized package version management
* `.editorconfig`
* Git configuration
* Solution-level project organization

### DevOps

* GitHub Actions workflows
* Docker
* Docker Compose
* Azure deployment configuration
* Infrastructure-as-code resources
* Development containers

These statements are based on the files and projects currently present in the repository.

---

# Security Considerations

When running the application locally or deploying it to Azure:

* Do not commit passwords or API keys.
* Do not commit Azure credentials.
* Do not commit production connection strings containing credentials.
* Use environment-specific configuration for secrets.
* Review GitHub Actions configuration before enabling deployment.
* Use GitHub repository secrets/variables or the appropriate Azure secret-management mechanism for deployment credentials.

The original application documentation also describes the use of Azure Key Vault for sensitive deployment data in its Azure deployment scenario.

---

# Repository Quality Notes

This repository is based on a Microsoft reference application. Therefore, it should be evaluated in two contexts:

1. **The original eShopOnWeb application and architecture**
2. **Any additional changes or engineering work made in this repository**

This distinction is intentionally documented so that the repository does not misrepresent Microsoft-authored reference application functionality as original work.

---

# Original Project & References

The underlying application is the Microsoft **eShopOnWeb ASP.NET Core Reference Application**.

Original project:

https://github.com/dotnet-architecture/eShopOnWeb

The reference application is associated with Microsoft's free resource:

**Architecting Modern Web Applications with ASP.NET Core and Azure**

https://aka.ms/webappebook

The original project documentation describes eShopOnWeb as a sample/reference application intended to demonstrate architectural principles and patterns rather than as a complete production e-commerce platform.

---

# License

This repository contains an MIT License.

See:

```text
LICENSE
```

for the applicable license terms.

---

# Repository Links

* **Repository:** https://github.com/SonaliMB/eShopOnWeb
* **Source:** `src/`
* **Tests:** `tests/`
* **CI/CD:** `.github/workflows/`
* **Infrastructure:** `infra/`
* **Development Container:** `.devcontainer/`
* **Docker:** `docker-compose.yml`

---

# Future Improvements

Potential future improvements can include:

* Expanding automated test coverage where appropriate
* Improving test reporting in CI
* Adding clearer CI quality gates
* Adding automated security/dependency checks
* Improving API documentation
* Adding application screenshots and architecture diagrams
* Improving deployment environment configuration
* Adding additional end-to-end automation where valuable
* Documenting measurable test and build results from actual CI executions

These are proposed improvements, not claims about functionality currently implemented in the repository.

---

## Disclaimer

This repository is based on the Microsoft eShopOnWeb reference application.

Any modifications, testing improvements, documentation improvements, automation changes, or DevOps changes made in this repository should be considered separately from the original Microsoft reference implementation.

No performance, test-pass, coverage, deployment-success, or production-readiness claims are made here unless supported by verifiable project results.
