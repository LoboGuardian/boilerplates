# flask

Python Flask + uv + SQLAlchemy + PostgreSQL

## Idea

Micro-framework Python minimalista. Sin opiniones fuertes — construyes la arquitectura que necesitas. Ideal para APIs pequeñas/medianas, microservicios, o cuando Django es demasiado para el problema.

## Stack

- **Flask 3** — micro web framework
- **uv** — package manager
- **SQLAlchemy 2** — ORM async
- **Alembic** — migraciones de base de datos
- **PostgreSQL** — base de datos
- **Flask-JWT-Extended** — autenticación JWT
- **Marshmallow** — serialización y validación
- **Ruff** — linting y formatting
- **pytest** — testing

## Structure

```
app/
  __init__.py       # App factory (create_app())
  extensions.py     # Instancias de extensiones (db, jwt, ma)
  api/
    v1/
      users/
        routes.py
        service.py
        schemas.py  # Marshmallow schemas
      __init__.py   # Blueprint registration
  models/           # SQLAlchemy models
  core/
    config.py       # Config classes (Dev, Prod, Test)
    exceptions.py   # Custom exceptions + error handlers
migrations/         # Alembic migrations
tests/
.env.example
pyproject.toml
```

## Decisions

- App factory pattern (`create_app()`) — permite múltiples instancias para testing.
- Blueprints para organizar rutas por dominio.
- Extensions inicializadas sin la app, luego `init_app()` — evita circular imports.
- Marshmallow para serialización: separa la forma de la respuesta del modelo de BD.
- Config por clase: `DevelopmentConfig`, `ProductionConfig`, `TestingConfig`.
