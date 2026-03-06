# godot-gdscript

Godot 4 + GDScript — juego 2D/3D

## Idea

El motor de juegos open source más popular. GDScript es el lenguaje nativo de Godot — sintaxis tipo Python, diseñado específicamente para juegos. Sin necesidad de compilación: iteración rápida, ideal para prototipos y juegos indie.

## Stack

- **Godot 4.3** — motor de juegos (2D y 3D)
- **GDScript** — lenguaje de scripting nativo
- **Godot Editor** — IDE integrado
- **GDUnit4** — framework de testing para GDScript (opcional)

## Structure

```
project.godot             # Config del proyecto
scenes/                   # Escenas (.tscn) — unidad básica de Godot
  main/
    Main.tscn
    Main.gd
  player/
    Player.tscn
    Player.gd
  ui/
    HUD.tscn
    HUD.gd
    MainMenu.tscn
scripts/                  # Scripts sin escena asociada
  autoloads/              # Singletons globales (GameManager, AudioManager)
    GameManager.gd
    EventBus.gd
  resources/              # Recursos personalizados (.tres)
assets/
  sprites/
  audio/
    sfx/
    music/
  fonts/
addons/                   # Plugins de la Asset Library
```

## Decisions

- Escenas como unidad fundamental — cada entidad del juego es una escena reutilizable.
- Autoloads (singletons) solo para estado verdaderamente global: GameManager, AudioManager, EventBus.
- Señales para comunicación entre nodos — evitar referencias directas entre escenas no relacionadas.
- `EventBus.gd` como autoload: señales globales para desacoplar sistemas.
- Recursos personalizados (`Resource`) para datos de juego (stats de personajes, niveles).
- Grupos de Godot para identificar nodos por rol: `add_to_group("enemies")`.
