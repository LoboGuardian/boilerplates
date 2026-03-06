# dotnet-api

.NET 9 Web API + C# + Entity Framework Core + PostgreSQL

## Idea

API REST moderna con el stack Microsoft. .NET 9 con Minimal APIs o Controllers, EF Core como ORM, y el ecosistema NuGet. Ideal para equipos con background C# o requisitos de integración con Azure.

## Stack

- **.NET 9** — runtime y SDK
- **C# 13** — lenguaje con tipos modernos
- **ASP.NET Core** — framework web
- **Entity Framework Core** — ORM con migrations
- **PostgreSQL** — base de datos (via Npgsql)
- **ASP.NET Core Identity + JWT** — autenticación
- **FluentValidation** — validación de requests
- **Serilog** — structured logging
- **xUnit + Moq** — testing

## Structure

```
src/
  MyApp.Api/                  # Proyecto principal
    Controllers/              # API Controllers (o Endpoints/ para Minimal API)
    Middleware/               # Auth, error handling, logging
    DTOs/                     # Request y Response records
    Extensions/               # IServiceCollection extensions (DI setup)
    Program.cs
  MyApp.Application/          # Lógica de negocio (CQRS con MediatR opcional)
    Services/
    Interfaces/
  MyApp.Domain/               # Entidades de dominio y reglas de negocio
    Entities/
    Exceptions/
  MyApp.Infrastructure/       # EF Core, repositorios, servicios externos
    Persistence/
      AppDbContext.cs
      Migrations/
    Repositories/
tests/
  MyApp.Api.Tests/
  MyApp.Application.Tests/
```

## Decisions

- Clean Architecture en capas: Api → Application → Domain ← Infrastructure.
- Records de C# para DTOs — inmutables y con value equality por defecto.
- Minimal APIs para endpoints simples; Controllers para lógica compleja.
- `IOptions<T>` para configuración tipada — nunca `IConfiguration` directo en servicios.
- EF Core migrations versionadas — nunca `EnsureCreated()` en producción.
