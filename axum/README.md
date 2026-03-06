# axum

Rust + Axum + SQLx + PostgreSQL

## Idea

API web en Rust con máximo performance y seguridad de memoria. Axum es el framework web del ecosistema Tokio. SQLx provee queries async type-safe sin ORM. Para cuando performance y correctness son innegociables.

## Stack

- **Rust** — lenguaje (edition 2021)
- **Axum** — framework web async sobre Tokio
- **Tokio** — async runtime
- **SQLx** — async SQL con queries verificadas en compile time
- **PostgreSQL** — base de datos
- **serde / serde_json** — serialización
- **tower** — middleware (rate limiting, CORS, auth)
- **jsonwebtoken** — JWT
- **tracing** — structured logging
- **cargo-watch** — live reload en desarrollo

## Structure

```
src/
  api/
    handlers/       # Axum handlers por recurso
    middleware/     # Auth extractor, logging
    routes.rs       # Router principal
  db/
    queries/        # Queries SQL embebidas con sqlx::query!
    mod.rs          # Pool setup
  models/           # Structs de dominio
  dto/              # Request/Response types con Serde
  config.rs         # Config desde env (envy crate)
  error.rs          # Error types centralizados con IntoResponse
  main.rs           # Setup: config, pool, router, server
migrations/         # SQL migrations (sqlx-cli)
.env.example
Cargo.toml
```

## Decisions

- `sqlx::query!` macro verifica las queries contra la BD en compile time — cero SQL inválido en runtime.
- Error type centralizado que implementa `IntoResponse` — los handlers devuelven `Result<_, AppError>`.
- Extractors de Axum para validación de request (`Json<T>`, custom `AuthUser` extractor).
- `Arc<AppState>` como estado compartido entre handlers — no globals.
- `cargo sqlx prepare` genera metadata offline para CI sin BD disponible.
