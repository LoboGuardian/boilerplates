# bevy

Rust + Bevy — game engine ECS

## Idea

Motor de juegos data-driven en Rust puro con arquitectura ECS (Entity Component System). Bevy es el motor más activo del ecosistema Rust. ECS favorece la composición sobre la herencia y escala mejor que los árboles de objetos tradicionales.

## Stack

- **Rust** — lenguaje (edition 2021)
- **Bevy 0.15** — game engine ECS
- **bevy_asset_loader** — carga de assets con estados
- **bevy_rapier2d / bevy_rapier3d** — física (Rapier)
- **bevy_egui** — UI de debug / herramientas in-game
- **bevy_kira_audio** — audio

## ECS Concepts

- **Entity** — ID único (sin datos propios)
- **Component** — datos puros (`struct Position(Vec2)`)
- **System** — funciones que operan sobre queries de componentes
- **Resource** — datos globales singleton (`ResMut<Score>`)
- **Event** — comunicación entre sistemas

## Structure

```
src/
  main.rs             # App::new() + plugins
  plugins/            # Cada sistema de juego como Plugin
    player/
      mod.rs          # Plugin definition
      systems.rs      # Systems del player
      components.rs   # Components del player
    enemy/
    physics/
    ui/
  states.rs           # GameState enum (Menu, Playing, Paused)
  assets.rs           # AssetCollection con bevy_asset_loader
assets/
  sprites/
  audio/
  fonts/
```

## Decisions

- Todo es un Plugin — `App::add_plugins(PlayerPlugin)`. Mantiene `main.rs` limpio.
- Systems agrupados en `SystemSet` con orden explícito cuando hay dependencias.
- `GameState` como `States` enum para separar lógica de menú, gameplay, pausa.
- `bevy_asset_loader` para cargar assets antes de entrar al estado de juego.
- Componentes son structs simples — sin lógica, solo datos.
- `Event` para comunicación entre plugins — nunca acceder al state de otro plugin directamente.
