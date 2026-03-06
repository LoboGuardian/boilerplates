# actix

Rust + Actix-web + SQLx + PostgreSQL

## Idea

Uno de los frameworks web más rápidos del mundo según TechEmpower benchmarks. Basado en el modelo de actores. Para cuando el rendimiento es el requisito principal y el equipo conoce Rust.

## Stack

- **Rust** — lenguaje (edition 2021)
- **Actix-web 4** — framework HTTP (actor-based)
- **Tokio** — async runtime
- **SQLx** — async SQL type-safe sin ORM
- **PostgreSQL** — base de datos
- **serde / serde_json** — serialización
- **actix-web-httpauth** — middleware de autenticación
- **jsonwebtoken** — JWT
- **tracing + tracing-actix-web** — structured logging
- **validator** — validación de structs con derive

## Structure

```
src/
  handlers/         # Actix handlers (request → response)
  services/         # Lógica de negocio
  db/
    queries/        # Funciones con sqlx::query! macros
    mod.rs          # Pool setup
  models/           # Structs de dominio
  dto/              # Request/Response types con Serde + Validator
  middleware/       # Auth JWT, logging
  errors.rs         # AppError con ResponseError impl
  config.rs         # Config desde env
  main.rs           # App setup, routes, server
migrations/
.env.example
Cargo.toml
```

## Decisions

- `sqlx::query!` verifica SQL en compile time — las queries inválidas no compilan.
- `AppError` implementa `ResponseError` de Actix — handlers devuelven `Result<_, AppError>`.
- `web::Data<AppState>` para estado compartido (pool, config) — sin globals.
- Rutas registradas con `web::scope` para agrupar por versión/recurso.
- `#[derive(Validate)]` en DTOs — validación automática antes de llegar al handler.
