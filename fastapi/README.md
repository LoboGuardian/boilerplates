# fastapi

Python FastAPI + uv + SQLModel + PostgreSQL

## Idea

A production-ready REST API starter. Async from the ground up, with typed models shared between the DB layer and the API schemas. Managed entirely with `uv` for fast dependency resolution.

## Stack

- **FastAPI** — async web framework with automatic OpenAPI docs
- **uv** — fast Python package and project manager
- **SQLModel** — combines SQLAlchemy + Pydantic (one model for DB and validation)
- **PostgreSQL** — primary database via asyncpg
- **Alembic** — database migrations
- **Ruff** — linting and formatting
- **pytest + httpx** — testing

## Structure

```
app/
  api/
    v1/
      routers/    # One file per resource (users.py, items.py)
      deps.py     # Shared dependencies (get_db, get_current_user)
  core/
    config.py     # Settings via pydantic-settings
    security.py   # JWT, password hashing
  db/
    session.py    # Async DB engine and session
    base.py       # SQLModel base
  models/         # SQLModel table models
  schemas/        # Pydantic models for request/response (when different from models)
  services/       # Business logic
  main.py         # App factory
tests/
.env.example
pyproject.toml
```

## Decisions

- All endpoints are async (`async def`).
- SQLModel reduces duplication: the same class defines the DB table and the API schema where possible.
- Settings loaded from environment via `pydantic-settings`; never hardcoded.
- JWT auth pre-wired with `python-jose`.
- One Alembic migration per feature; never edit existing migrations.
