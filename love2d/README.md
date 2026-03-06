# love2d

Lua + LÖVE 2D — juego 2D ligero

## Idea

Framework 2D minimalista en Lua. LÖVE provee el loop de juego, renderizado, audio y física — el desarrollador construye todo lo demás. Lua es simple, rápido de aprender y perfecto para prototipos. Popular en game jams.

## Stack

- **LÖVE 11.5** — framework 2D
- **Lua 5.1** — lenguaje (versión de LuaJIT incluida en LÖVE)
- **hump** — librería de utilidades (gamestate, vector, timer)
- **bump.lua** — detección de colisiones AABB simple
- **busted** — testing framework para Lua (opcional)

## Structure

```
main.lua              # love.load, love.update, love.draw callbacks
conf.lua              # Configuración de la ventana (love.conf)
src/
  states/             # Game states con hump.gamestate
    menu.lua
    game.lua
    gameover.lua
  entities/           # Entidades del juego (tablas Lua con metatables)
    player.lua
    enemy.lua
  systems/
    collision.lua
  ui/
    hud.lua
assets/
  sprites/
  audio/
  fonts/
libs/                 # Librerías externas (hump, bump, etc.)
```

## main.lua (estructura)

```lua
local Gamestate = require 'libs.hump.gamestate'
local menu = require 'src.states.menu'

function love.load()
  Gamestate.registerEvents()
  Gamestate.switch(menu)
end
```

## Decisions

- `hump.gamestate` para manejo de estados — `Gamestate.switch(game)`, `Gamestate.push(pause)`.
- Entidades como tablas Lua con metatables — OOP simple sin framework pesado.
- `bump.lua` para colisiones — AABB tile-based, simple y efectivo para juegos 2D.
- `conf.lua` para configurar resolución, título y módulos activos al inicio.
- Distribuir con `love game.love` (archivo zip) — funciona en Windows, macOS y Linux.
