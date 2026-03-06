# rails

Ruby on Rails 8 + PostgreSQL

## Idea

El framework que popularizó "convention over configuration". Máxima productividad con mínima configuración. Rails 8 incluye Solid Queue, Solid Cache y Kamal para deploy — sin dependencias externas de infraestructura.

## Stack

- **Ruby on Rails 8** — full-stack web framework
- **Ruby 3.3** — lenguaje
- **PostgreSQL** — base de datos
- **Active Record** — ORM de Rails
- **Devise** — autenticación (o Rails 8 Authentication Generator)
- **Active Job + Solid Queue** — background jobs sin Redis
- **Hotwire (Turbo + Stimulus)** — frontend reactivo sin escribir mucho JS
- **Tailwind CSS** — styling via `tailwindcss-rails`
- **RSpec** — testing
- **RuboCop** — linting y formatting

## Structure

```
app/
  controllers/
    api/v1/         # API controllers (si hay API)
    concerns/       # Módulos compartidos entre controllers
  models/
    concerns/       # Módulos compartidos entre models
  services/         # Plain Ruby Objects para lógica de negocio
  serializers/      # Serialización de respuestas API (jbuilder o blueprinter)
  views/            # ERB templates (para apps web)
  jobs/             # Active Job jobs
  mailers/
config/
  routes.rb
db/
  migrate/
  seeds.rb
spec/               # RSpec tests
```

## Decisions

- Skinny controllers, fat models — pero la lógica compleja va a Services (POROs).
- Rails 8 Authentication Generator para auth simple; Devise para necesidades avanzadas.
- Hotwire para interactividad: evitar una SPA separada cuando Turbo es suficiente.
- API-only mode (`--api`) si el frontend es externo.
- Kamal para deploy: Docker-based, sin necesidad de Heroku o plataformas externas.
