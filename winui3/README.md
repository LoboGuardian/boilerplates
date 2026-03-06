# winui3

WinUI 3 + C# + Windows App SDK — Windows 10/11 moderno

## Idea

El framework de UI más moderno de Microsoft para Windows. WinUI 3 con Windows App SDK desacopla la UI del OS — se actualiza independientemente de Windows. Fluent Design System nativo, soporte para dark/light mode automático.

## Stack

- **Windows App SDK 1.6** — SDK desacoplado del OS
- **WinUI 3** — framework UI moderno de Microsoft
- **C# 13 / .NET 9** — lenguaje y runtime
- **XAML** — declaración de UI
- **MVVM Community Toolkit** — MVVM sin boilerplate
- **Windows Community Toolkit** — controles adicionales
- **Microsoft.Extensions.DependencyInjection** — DI

## Structure

```
src/
  MyApp/
    App.xaml
    App.xaml.cs           # DI setup, ventana principal
    Views/
      MainWindow.xaml     # ShellWindow con NavigationView
      MainWindow.xaml.cs
      Pages/              # Páginas de contenido
        HomePage.xaml
    ViewModels/
      MainViewModel.cs
      Pages/
    Services/
      INavigationService.cs
      NavigationService.cs
    Models/
    Helpers/              # Converters, extensions
    Assets/               # Iconos y recursos
Package.appxmanifest      # Manifiesto de la app (capacidades, permisos)
```

## Decisions

- `NavigationView` como shell principal — patrón estándar en apps WinUI modernas.
- MVVM Toolkit con `[ObservableProperty]` y `[RelayCommand]` — source generators en build time.
- `DispatcherQueue` para actualizaciones de UI desde otros threads (reemplaza `Dispatcher` de WPF).
- Tema automático: `Application.RequestedTheme` desde configuración del sistema.
- MSIX packaging para distribución: firma, actualizaciones, y Microsoft Store.
