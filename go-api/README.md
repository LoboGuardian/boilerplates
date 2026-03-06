# go-api

Go HTTP API + Chi + sqlc + PostgreSQL

## Idea

A pragmatic Go REST API. No ORM — raw SQL with `sqlc` generates type-safe Go code from your queries. Chi provides lightweight routing without magic. Fits teams that value explicitness and performance.

## Stack

- **Go 1.23+** — language
- **Chi** — lightweight HTTP router (stdlib-compatible)
- **sqlc** — generates type-safe Go from SQL queries
- **pgx** — PostgreSQL driver
- **golang-migrate** — database migrations
- **go-playground/validator** — struct validation
- **slog** — structured logging (stdlib)
- **testify** — assertions in tests
- **Air** — live reload for development

## Structure

```
cmd/
  api/
    main.go       # Entry point: wires up server, config, DB
internal/
  api/
    handlers/     # HTTP handlers (one file per resource)
    middleware/   # Auth, logger, CORS
    routes.go     # Route registration
  db/
    queries/      # .sql files (input for sqlc)
    sqlc/         # Auto-generated Go code (do not edit)
    migrations/   # SQL migration files
  config/         # Config struct loaded from env
  service/        # Business logic (between handlers and DB)
sqlc.yaml
.env.example
Makefile          # Common commands: migrate, generate, build, test
```

## Decisions

- `internal/` enforces Go's package visibility rules — nothing inside can be imported by external packages.
- `sqlc` over an ORM: SQL is explicit, queries are optimized, and generated code is fully typed.
- Handlers call services; services call DB layer — strict layering, no DB access from handlers.
- Config is loaded from environment variables at startup and validated; the app fails fast if required vars are missing.
- `Makefile` wraps common commands: `make migrate/up`, `make sqlc`, `make test`.
