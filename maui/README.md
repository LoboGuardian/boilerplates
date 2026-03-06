# maui

.NET MAUI + C# — cross-platform mobile y desktop

## Idea

Multi-platform App UI de Microsoft. Un solo proyecto para Android, iOS, macOS (Mac Catalyst) y Windows. Evolución de Xamarin.Forms con mejor rendimiento y la madurez de .NET moderno.

## Stack

- **.NET 9** — runtime
- **C# 13** — lenguaje
- **.NET MAUI** — framework cross-platform
- **XAML** — declaración de UI
- **MVVM Community Toolkit** — MVVM con source generators
- **CommunityToolkit.Maui** — controles y behaviors adicionales
- **SQLite-net** — base de datos local
- **Microsoft.Extensions.DependencyInjection** — DI container

## Structure

```
src/
  MyApp/
    Platforms/          # Código específico por plataforma
      Android/
      iOS/
      MacCatalyst/
      Windows/
    Resources/
      Fonts/
      Images/           # Imágenes escaladas automáticamente por MAUI
      AppIcon/
      Splash/
    Views/              # XAML Pages y ContentViews
      MainPage.xaml
      MainPage.xaml.cs
    ViewModels/
      MainViewModel.cs
    Models/
    Services/
      Interfaces/
    MauiProgram.cs      # DI setup, app configuration
    AppShell.xaml       # Navigation Shell
    AppShell.xaml.cs
```

## Decisions

- `AppShell` con `Shell` routing para navegación — URL-based, simple.
- MVVM Toolkit con `[ObservableProperty]` y `[RelayCommand]` — source generators.
- `MauiProgram.cs` centraliza toda la DI — servicios, ViewModels, handlers de plataforma.
- Imágenes en `Resources/Images/` — MAUI las escala automáticamente por densidad de pantalla.
- `Preferences` para settings simples, SQLite para datos estructurados.
- Handlers para customizar la apariencia de controles por plataforma.
