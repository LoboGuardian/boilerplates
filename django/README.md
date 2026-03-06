# django

Django + Django REST Framework + uv + PostgreSQL

## Idea

A batteries-included REST API using Django's ecosystem. Best when you need Django's admin, ORM, auth system, and the breadth of its third-party packages. Managed with `uv`.

## Stack

- **Django 5** — web framework
- **Django REST Framework (DRF)** — REST API layer
- **uv** — package and project manager
- **PostgreSQL** — primary database (via psycopg3)
- **Simple JWT** — JWT authentication
- **dj-database-url** — 12-factor DB config
- **Ruff** — linting and formatting
- **pytest-django** — testing

## Structure

```
config/
  settings/
    base.py       # Shared settings
    local.py      # Dev overrides
    production.py # Prod overrides
  urls.py
  wsgi.py / asgi.py
apps/
  users/          # Custom user model (always extend AbstractUser)
  core/           # Shared models, mixins, permissions
api/
  v1/
    urls.py       # API router
    views/        # DRF ViewSets and APIViews
    serializers/  # DRF serializers
.env.example
pyproject.toml
manage.py
```

## Decisions

- Always use a custom user model from day one — impossible to swap later.
- Split settings per environment; use `DJANGO_SETTINGS_MODULE` env var.
- DRF ViewSets for CRUD-heavy resources; APIView for custom logic.
- All secrets via environment variables — `django-environ` or `pydantic-settings`.
- `asgi.py` wired up for async views and WebSocket support via Channels if needed.
