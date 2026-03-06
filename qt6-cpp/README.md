# qt6-cpp

C++ + Qt6 + CMake — app de escritorio Qt clásica

## Idea

El framework de escritorio cross-platform más completo: Windows, macOS, Linux. Qt provee todo: widgets, red, base de datos, multimedia, testing. C++ con Qt es el stack para apps de escritorio profesionales (VLC, Wireshark, Autodesk usan Qt).

## Stack

- **C++17/20** — lenguaje
- **Qt6** — framework completo (Widgets, Core, Network, SQL)
- **CMake** — build system (oficial desde Qt6)
- **Qt Creator** — IDE recomendado
- **Qt Designer** — diseñador visual de UI (.ui files)
- **QTest** — framework de testing incluido en Qt

## Structure

```
src/
  main.cpp
  MainWindow/
    MainWindow.h
    MainWindow.cpp
    MainWindow.ui         # Qt Designer UI file
  widgets/                # Custom QWidget subclasses
  models/                 # QAbstractItemModel subclasses
  services/               # Lógica de negocio (sin dependencia de Qt Widgets)
resources/
  resources.qrc           # Resource file (iconos, traducciones)
  icons/
  translations/
    app_es.ts             # Qt Linguist translation files
tests/
  unit/
CMakeLists.txt
```

## Decisions

- Subclassing de QWidget/QMainWindow para la ventana principal.
- Signal & Slot mechanism para comunicación entre objetos — no callbacks directos.
- Qt Designer para UI: archivos `.ui` generan código C++ en build time.
- `QSettings` para persistir preferencias del usuario.
- Separar lógica de negocio de la UI — los services no deben depender de Qt Widgets.
- `Qt::QueuedConnection` para señales entre threads — thread safety garantizada.
