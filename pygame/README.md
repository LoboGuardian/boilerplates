# pygame

Python + Pygame — juego 2D simple

## Idea

La librería de juegos 2D más popular de Python. Sin motor complejo — control total del game loop, renderizado y física. Ideal para juegos simples, game jams, o aprender desarrollo de videojuegos desde cero.

## Stack

- **Python 3.12+** — lenguaje
- **Pygame-CE** — fork comunitario de Pygame con mejoras activas
- **uv** — package manager
- **pytest** — testing de lógica de juego

## Structure

```
src/
  main.py             # Entry point: init, game loop
  game.py             # Clase Game (game loop principal)
  states/             # Estados del juego (State pattern)
    base_state.py
    menu_state.py
    play_state.py
    game_over_state.py
  entities/           # Sprites y entidades del juego
    player.py
    enemy.py
    projectile.py
  systems/            # Lógica desacoplada (colisiones, física)
    collision.py
  ui/                 # Elementos de UI (HUD, texto, botones)
  assets/             # Loader de assets centralizado
    asset_manager.py
resources/
  sprites/
  audio/
  fonts/
pyproject.toml
```

## Decisions

- State machine para gestionar pantallas: `MenuState`, `PlayState`, `GameOverState`.
- `pygame.sprite.Group` para gestionar colecciones de sprites con detección de colisiones.
- Game loop con `clock.tick(FPS)` y delta time para movimiento independiente del framerate.
- Assets cargados una sola vez al inicio con `AssetManager` — sin carga repetida en el loop.
- Separar lógica de juego de la lógica de renderizado — facilita el testing.
