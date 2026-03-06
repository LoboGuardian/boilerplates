# python-lib

Python library/package + uv + pytest + ruff

## Idea

A starter for building and publishing a Python library to PyPI. Follows modern Python packaging standards (PEP 621, `pyproject.toml`-only) and uses `uv` for fast dependency management.

## Stack

- **uv** — package manager, virtual environment, build tool
- **Ruff** — linting and formatting (replaces flake8, black, isort)
- **mypy** — static type checking
- **pytest** — testing framework
- **pytest-cov** — test coverage
- **GitHub Actions** — CI for test, lint, and publish

## Structure

```
src/
  mylib/          # Library source (src-layout prevents import confusion)
    __init__.py   # Public API exports
    _internal/    # Private implementation details
    py.typed      # Marker file — declares the package is typed
tests/
  unit/
  integration/
docs/             # Optional: MkDocs or Sphinx
pyproject.toml    # Single config file for everything
.github/
  workflows/
    ci.yml        # Run tests and lint on every push
    publish.yml   # Publish to PyPI on release tag
```

## Decisions

- **src layout**: `src/mylib/` prevents accidentally importing from the project root instead of the installed package.
- `py.typed` marker tells type checkers that the library ships with type annotations.
- Public API is explicitly defined in `__init__.py` — anything not exported there is considered private.
- `pyproject.toml` is the single source of truth: no `setup.py`, `setup.cfg`, or `requirements.txt`.
- Version is set once in `pyproject.toml` and read at runtime via `importlib.metadata`.
