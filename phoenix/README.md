# phoenix

Elixir + Phoenix Framework + PostgreSQL

## Idea

Framework web funcional con concurrencia masiva. Basado en el modelo de actores de Erlang/OTP. Phoenix LiveView permite UIs reactivas en tiempo real sin escribir JavaScript. Ideal para apps con alta concurrencia, chat, dashboards en vivo.

## Stack

- **Elixir 1.17** — lenguaje funcional sobre la BEAM VM
- **Phoenix 1.7** — web framework
- **Phoenix LiveView** — UI reactiva server-side sin JS
- **Ecto** — ORM/query DSL para Elixir
- **PostgreSQL** — base de datos
- **Guardian** — autenticación JWT (para API)
- **Tailwind CSS** — styling
- **ExUnit** — testing (incluido en Elixir)

## Structure

```
lib/
  myapp/              # Contextos (bounded contexts de dominio)
    accounts/         # Contexto de usuarios/auth
      accounts.ex     # API pública del contexto
      user.ex         # Ecto schema
  myapp_web/          # Capa web
    controllers/      # Para API REST
    live/             # LiveView modules
    components/       # Componentes de función
    router.ex         # Rutas
    endpoint.ex
priv/
  repo/
    migrations/       # Ecto migrations
test/
config/
  config.exs
  dev.exs
  prod.exs
  test.exs
```

## Decisions

- Contextos como módulos Elixir — encapsulan la lógica de dominio y exponen una API pública.
- LiveView para UIs interactivas: el estado vive en el servidor, cambios via WebSocket.
- Ecto Changesets para validación — separados del schema, reutilizables.
- Pattern matching extensivamente en controllers y LiveView handlers.
- OTP: usar GenServer y Supervisors para procesos de larga vida (sessions, games, etc.).
