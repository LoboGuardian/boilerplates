# avalonia

Avalonia UI + C# + .NET — cross-platform desktop

## Idea

WPF para todas las plataformas. Avalonia es un framework de UI cross-platform para .NET — misma experiencia que WPF pero en Windows, macOS, y Linux. XAML, MVVM, data binding. Ideal para equipos .NET que necesitan salir de Windows.

## Stack

- **Avalonia UI 11** — framework UI cross-platform
- **.NET 9** — runtime
- **C# 13** — lenguaje
- **AXAML** — XAML extendido de Avalonia
- **MVVM Community Toolkit** — MVVM con source generators
- **ReactiveUI** (opcional) — MVVM reactivo (popular en la comunidad Avalonia)
- **Avalonia.Themes.Fluent** — tema Fluent Design

## Structure

```
src/
  MyApp/
    App.axaml               # Application resources
    App.axaml.cs
    Views/
      MainWindow.axaml      # Ventana principal
      MainWindow.axaml.cs
      Pages/                # UserControls como páginas
    ViewModels/
      MainWindowViewModel.cs
      Pages/
    Models/
    Services/
    Converters/             # IValueConverter para bindings
    Assets/                 # Iconos, fuentes
tests/
  MyApp.Tests/              # Con Avalonia.Headless para tests de UI
```

## Decisions

- `UserControl` como unidad de navegación — inyectados como contenido de la ventana principal.
- MVVM Toolkit o ReactiveUI — elige uno y úsalo consistentemente.
- `Avalonia.Headless` para tests de UI sin display — funciona en CI.
- Theming: `Avalonia.Themes.Fluent` o `Avalonia.Themes.Simple` como base.
- Para Linux: asegurarse que funciona con X11 y Wayland (Avalonia soporta ambos).
- Publicar como self-contained para evitar dependencia del runtime .NET instalado.
