# wxwidgets

C++ + wxWidgets — app desktop cross-platform con controles nativos

## Idea

Framework C++ que usa los controles nativos del sistema operativo — en Windows usa Win32, en macOS usa Cocoa, en Linux usa GTK. Las apps se ven y se sienten nativas en cada plataforma. Usado por Audacity, FileZilla, y Code::Blocks.

## Stack

- **C++17** — lenguaje
- **wxWidgets 3.2** — framework cross-platform con controles nativos
- **CMake** — build system
- **wxFormBuilder** — diseñador visual de UI (genera código C++)

## Structure

```
src/
  main.cpp            # wxApp subclass — entry point
  MainFrame.h
  MainFrame.cpp       # wxFrame principal
  dialogs/            # wxDialog subclasses
  panels/             # wxPanel subclasses (contenido de la ventana)
  models/             # Lógica de negocio (sin dependencia de wx)
  resources/
    app.xrc           # XML Resource — UI declarativa (alternativa a código)
    icons/
CMakeLists.txt
```

## Decisions

- `wxApp::OnInit()` es el entry point — crea el frame principal y lo muestra.
- XRC (XML Resources) para definir UI en XML — separación de UI y lógica.
- Eventos con `Bind()` en lugar de macros de event tables — más type-safe.
- Lógica de negocio en clases sin dependencia de wxWidgets — testeable de forma aislada.
- `wxConfig` para persistir preferencias — usa el registro en Windows, `.plist` en macOS, archivos en Linux.
- CMake con `find_package(wxWidgets REQUIRED)` — funciona en las tres plataformas.
