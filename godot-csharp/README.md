# godot-csharp

Godot 4 + C# (.NET) — juego 2D/3D

## Idea

Godot con C# como lenguaje de scripting. Mismo motor que `godot-gdscript` pero con tipado estático, mejor rendimiento en lógica compleja, y acceso al ecosistema NuGet. Ideal para equipos con background en Unity o .NET.

## Stack

- **Godot 4.3 (.NET)** — versión de Godot con soporte C#
- **C# 12 / .NET 8** — lenguaje y runtime
- **Godot C# API** — bindings de Godot para C#
- **xUnit** — testing de lógica de juego (fuera de Godot)

## Structure

```
project.godot
scenes/
  Main/
    Main.tscn
    Main.cs
  Player/
    Player.tscn
    Player.cs
  UI/
    HUD.tscn
    HUD.cs
scripts/
  Autoloads/          # Singletons globales
    GameManager.cs
    EventBus.cs
  Data/               # Recursos y ScriptableObjects equivalentes
    CharacterStats.cs
assets/
  Sprites/
  Audio/
  Fonts/
tests/                # Lógica de negocio testeable sin el motor
  GameLogic.Tests/
```

## Decisions

- C# en Godot usa el mismo Node system que GDScript — `[Export]` en lugar de `export var`.
- `partial class` — Godot genera parte de la clase; el developer escribe la otra parte.
- Separar lógica de juego pura (sin dependencia de Godot) en clases C# testables con xUnit.
- Autoloads como singletons C# — accesibles desde cualquier nodo.
- Evitar `GetNode<T>()` excesivo — preferir `[Export]` y asignar desde el editor.
- C# es más rápido que GDScript para cálculos pesados (pathfinding, física customizada).
