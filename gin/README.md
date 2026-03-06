# gin

Go + Gin + GORM + PostgreSQL

## Idea

El framework Go más popular. Mayor ecosistema y más recursos que Chi. Ideal cuando se quiere un framework más completo con middleware integrado, binding automático y validación.

## Stack

- **Go 1.23+** — lenguaje
- **Gin** — framework HTTP (el más usado en Go)
- **GORM** — ORM para Go
- **PostgreSQL** — base de datos
- **golang-jwt/jwt** — autenticación JWT
- **go-playground/validator** — validación de structs
- **slog** — structured logging (stdlib)
- **testify** — assertions en tests
- **Air** — live reload en desarrollo
- **golang-migrate** — migraciones SQL

## Structure

```
cmd/
  api/
    main.go
internal/
  api/
    handlers/       # Gin handlers por recurso
    middleware/     # Auth JWT, logger, CORS, rate limit
    router.go       # Registro de rutas
  config/           # Config desde variables de entorno
  models/           # GORM models
  repository/       # Capa de acceso a datos
  service/          # Lógica de negocio
  dto/              # Request/Response structs con tags de validación
.env.example
Makefile
```

## Decisions

- Handlers delgados: reciben request, llaman al service, devuelven response.
- Repository pattern: services nunca llaman a GORM directamente.
- DTOs separados de los models: no exponer la estructura de BD en la API.
- Middleware de auth usando `gin.Context` para propagar el usuario actual.
- `Makefile` con targets: `run`, `build`, `test`, `migrate-up`, `migrate-down`.
