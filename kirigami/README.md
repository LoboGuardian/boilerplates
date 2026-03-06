# kirigami

KDE Kirigami + QML + C++ — app KDE adaptable

## Idea

Framework UI de KDE sobre Qt6 + QML. Kirigami está diseñado para apps que se adaptan a desktop y mobile desde el mismo código. Es el framework de KDE para apps modernas (Discover, KDE Connect usan Kirigami).

## Stack

- **KDE Kirigami2** — framework UI adaptable de KDE
- **QML** — lenguaje declarativo para UI
- **C++** — backend (lógica, modelos)
- **Qt6** — base del framework
- **CMake + extra-cmake-modules (ECM)** — build system de KDE
- **KConfig** — sistema de configuración de KDE
- **KDE CI Pipeline** — CI estándar de KDE

## Structure

```
src/
  main.cpp              # QApplication + QQmlApplicationEngine
  backend/              # C++ QObject subclasses expuestos a QML
    AppController.h
    AppController.cpp
  models/               # QAbstractListModel para listas en QML
qml/
  Main.qml              # Ventana Kirigami principal
  pages/                # Páginas de la app (Kirigami.Page)
    HomePage.qml
    SettingsPage.qml
  components/           # Componentes QML reutilizables
resources.qrc
CMakeLists.txt
org.kde.AppName.desktop
org.kde.AppName.appdata.xml
```

## Decisions

- QML para toda la UI — C++ solo para lógica y modelos.
- `Kirigami.ApplicationWindow` como ventana base — maneja navigation stack.
- `Kirigami.Page` como unidad de navegación — push/pop en el page stack.
- C++ QObjects registrados en QML con `qmlRegisterType` o `QML_ELEMENT`.
- KConfig para preferencias — integrado con el sistema de temas de KDE.
- `KAboutData` para información de la app (se usa en el diálogo "Acerca de").
