# flutter-desktop

Flutter + Dart — app de escritorio cross-platform

## Idea

Flutter para desktop: Windows, macOS, y Linux desde un solo codebase. El mismo framework que para mobile pero con widgets adaptados para pantallas grandes, mouse, y teclado. Ideal si ya tienes una app Flutter mobile y quieres expandirla a desktop.

## Stack

- **Flutter 3.27+** — framework UI
- **Dart 3** — lenguaje
- **Riverpod 2** — state management
- **go_router** — routing (con soporte deep link en desktop)
- **drift** — base de datos local SQLite (generación de código)
- **window_manager** — control de la ventana (tamaño, título, decoración)
- **very_good_analysis** — linting estricto

## Structure

```
lib/
  core/
    router/
    theme/              # ThemeData adaptado para desktop
    database/           # Drift database
  features/
    home/
      presentation/
        screens/
          home_screen.dart     # Layout de dos paneles para desktop
        widgets/
      data/
      domain/
  shared/
    widgets/
      responsive/       # Widgets que adaptan layout a tamaño de pantalla
  main.dart
  app.dart
linux/                  # Configuración específica de Linux
windows/                # Configuración específica de Windows
macos/                  # Configuración específica de macOS
```

## Decisions

- Layouts responsivos: `LayoutBuilder` para adaptar UI de mobile a desktop (sidebar en pantalla grande).
- `window_manager` para control de la ventana: tamaño mínimo, título dinámico, cerrar minimizado al tray.
- `drift` sobre `sqflite` para desktop — soporte completo en las tres plataformas.
- Keyboard shortcuts con `Shortcuts` y `Actions` widgets — esenciales en desktop.
- `ContextMenu` para menús contextuales con click derecho.
- Distribuir con MSIX (Windows), DMG (macOS), AppImage/Snap/Flatpak (Linux).
