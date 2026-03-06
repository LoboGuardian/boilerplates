# qt6-python

Python + PySide6 (Qt6) — app de escritorio Qt con Python

## Idea

Qt6 con Python usando PySide6 (el binding oficial de Qt). La productividad de Python con el poder y la madurez de Qt. Ideal para herramientas internas, dashboards científicos, y apps donde el prototipado rápido importa.

## Stack

- **Python 3.12+** — lenguaje
- **PySide6** — binding oficial de Qt6 para Python (LGPL)
- **Qt6** — framework de UI (Widgets + QML opcional)
- **uv** — package manager
- **Qt Designer** — diseñador visual de UI
- **Ruff** — linting y formatting
- **pytest-qt** — testing de widgets Qt

## Structure

```
src/
  app_name/
    __init__.py
    main.py               # QApplication entry point
    main_window.py        # QMainWindow subclass
    widgets/              # QWidget subclasses
    models/               # QAbstractItemModel subclasses
    services/             # Lógica de negocio (sin Qt)
    ui/                   # Archivos .ui de Qt Designer
      main_window.ui
resources/
  resources.qrc
  icons/
tests/
pyproject.toml
```

## Decisions

- PySide6 sobre PyQt6: licencia LGPL (PyQt6 es GPL para uso comercial).
- `uic.loadUiType()` para cargar archivos `.ui` en runtime — o compilar con `pyside6-uic`.
- QThread o `QRunnable` para operaciones en background — nunca bloquear el main thread.
- `QSettings` para persistencia de preferencias (integrado con el SO).
- `pytest-qt` con `qtbot` fixture para testing de interacciones de UI.
- `pyside6-deploy` para crear ejecutables distribuibles.
