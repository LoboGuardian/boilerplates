# winforms-net48

.NET Framework 4.8 + Windows Forms + C# — Windows 7/8/10/11

## Idea

Windows Forms en .NET Framework 4.8 para máxima compatibilidad con Windows legacy. El más sencillo de los stacks Windows — sin XAML, sin MVVM obligatorio. Ideal para herramientas internas, utilidades de sistema, o ports de apps VB6/VB.NET.

## Stack

- **.NET Framework 4.8** — runtime compatible con Windows 7 SP1+
- **C# 7.3** — lenguaje
- **Windows Forms** — framework de UI
- **NUnit o MSTest** — testing
- **Dapper** — acceso a datos simple (opcional)

## Compatibility

| OS | Soporte |
|---|---|
| Windows 7 SP1 | Si (con .NET 4.8 instalado) |
| Windows 8.1 | Si |
| Windows 10/11 | Si |

## Structure

```
src/
  MyApp/
    Forms/
      MainForm.cs
      MainForm.Designer.cs
      MainForm.resx
    Controls/           # UserControls
    Business/           # Lógica de negocio
    Data/               # Acceso a datos (Dapper, ADO.NET)
    Models/
    Helpers/
    Program.cs
    app.manifest        # DPI awareness
    app.config          # Connection strings, app settings
tests/
```

## Decisions

- `app.config` para connection strings y configuración — no hardcoded.
- `app.manifest` con DPI awareness para que no se vea borroso en pantallas de alta resolución.
- `BackgroundWorker` para operaciones largas — es el patrón más compatible con .NET 4.8.
- Distribuir con instalador WiX o Inno Setup — genera `.msi` o `.exe` que instala .NET 4.8 si no está presente.
- Evitar características de C# 8+ — usar solo hasta C# 7.3.
