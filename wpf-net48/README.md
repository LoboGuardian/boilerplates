# wpf-net48

.NET Framework 4.8 + WPF + C# — Windows 7/8/10/11

## Idea

WPF para aplicaciones que deben funcionar en Windows 7. .NET Framework 4.8 es el último que soporta Windows 7 SP1. Si el target es Windows 7, este es el stack recomendado para apps con UI rica.

## Stack

- **.NET Framework 4.8** — el último runtime compatible con Windows 7 SP1
- **C# 7.3** — máxima versión disponible en .NET Framework 4.8
- **WPF** — framework de UI
- **MVVM Light o Prism** — MVVM framework (MVVM Community Toolkit no soporta .NET Framework)
- **MSTest o NUnit** — testing

## Compatibility

| OS | Soporte |
|---|---|
| Windows 7 SP1 | Requiere KB2533623 + KB2999226 |
| Windows 8.1 | Si |
| Windows 10 | Si |
| Windows 11 | Si |

## Structure

```
src/
  MyApp/
    Views/
      MainWindow.xaml
      MainWindow.xaml.cs
    ViewModels/
      MainViewModel.cs    # Hereda de ViewModelBase (MVVM Light)
    Models/
    Services/
    Converters/
    Resources/
    App.xaml
    App.xaml.cs
tests/
```

## Decisions

- MVVM Light como framework MVVM — compatible con .NET Framework 4.8.
- No usar `async/await` con patrones modernos que requieren .NET 5+ — usar `Task` clásico.
- `ICommand` con `RelayCommand` de MVVM Light para binding de botones.
- Distribuir como instalador MSI o ClickOnce — compatible con Windows 7.
- Incluir VC++ Redistributable y .NET Framework 4.8 en el instalador.
- Evitar APIs de Windows 10+ — verificar compatibilidad antes de usar PInvoke.
