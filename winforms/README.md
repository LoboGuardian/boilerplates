# winforms

.NET 9 + Windows Forms + C# — Windows 10/11

## Idea

El framework de UI más simple y maduro de Microsoft. Drag & drop en el diseñador, sin XAML. Ideal para herramientas internas, utilidades de sistema, o cuando se necesita velocidad de desarrollo sobre riqueza visual.

## Stack

- **.NET 9** — runtime
- **C# 13** — lenguaje
- **Windows Forms** — framework de UI (solo Windows)
- **xUnit** — testing
- **Dapper** — micro-ORM para acceso a datos (si se necesita BD)

## Structure

```
src/
  MyApp/
    Forms/
      MainForm.cs         # Formulario principal
      MainForm.Designer.cs # Código generado por el diseñador
      MainForm.resx       # Recursos del formulario
      Dialogs/            # Formularios de diálogo
    Controls/             # UserControls personalizados
    Services/             # Lógica de negocio
    Models/               # Entidades de datos
    Helpers/              # Utilidades
    Program.cs            # Entry point
    app.manifest          # Manifest (DPI awareness, etc.)
tests/
  MyApp.Tests/
```

## Decisions

- Separar lógica de negocio en `Services/` — no mezclar con event handlers del Form.
- `Program.cs` configura DPI awareness y crea el formulario principal.
- Evitar lógica en `Form.Designer.cs` — solo código generado por el diseñador.
- `BackgroundWorker` o `Task` + `Invoke()` para operaciones async sin congelar la UI.
- `ApplicationSettings` para persistir preferencias del usuario.
- High DPI support: `Application.SetHighDpiMode(HighDpiMode.PerMonitorV2)`.
