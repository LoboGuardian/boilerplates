# wpf

.NET 9 + WPF + C# — Windows 10/11

## Idea

Windows Presentation Foundation — el framework de UI de Microsoft para Windows. XAML para declarar la UI, C# para la lógica. Rico en controles, data binding, animaciones y estilos. Ideal para apps de escritorio Windows con UI sofisticada.

## Stack

- **.NET 9** — runtime
- **C# 13** — lenguaje
- **WPF** — framework de UI (solo Windows)
- **MVVM Community Toolkit** — MVVM con source generators (sin boilerplate)
- **CommunityToolkit.Mvvm** — ViewModels, Commands, Messaging
- **Microsoft.Extensions.DependencyInjection** — DI container
- **Entity Framework Core** — ORM (si hay BD local con SQLite)
- **xUnit** — testing

## Structure

```
src/
  MyApp/
    App.xaml                  # Application resources y startup
    App.xaml.cs
    Views/                    # XAML Views (ventanas y páginas)
      MainWindow.xaml
      MainWindow.xaml.cs      # Code-behind mínimo
      Pages/
    ViewModels/               # ViewModels con ObservableObject
      MainViewModel.cs
      Pages/
    Models/                   # Modelos de dominio
    Services/                 # Lógica de negocio e interfaces
      Interfaces/
    Converters/               # IValueConverter para XAML bindings
    Controls/                 # Custom UserControls
    Resources/                # XAML ResourceDictionaries (estilos, temas)
tests/
  MyApp.Tests/
```

## Decisions

- MVVM estricto: Views solo tienen code-behind para lógica de UI pura.
- `[ObservableProperty]` y `[RelayCommand]` de MVVM Toolkit — sin boilerplate INotifyPropertyChanged.
- DI container configurado en `App.xaml.cs` — ViewModels y Services inyectados.
- ResourceDictionaries para estilos globales y temas (dark/light).
- `INavigationService` para navegar entre páginas sin acoplar ViewModels a Views.
