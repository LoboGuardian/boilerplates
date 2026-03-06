# laravel

Laravel 11 + PHP 8.3 + PostgreSQL

## Idea

El framework PHP más popular. Batteries-included: ORM Eloquent, migraciones, autenticación, queues, scheduling, y más. Ideal para aplicaciones web completas o APIs con el ecosistema PHP.

## Stack

- **Laravel 11** — framework PHP full-stack
- **PHP 8.3** — lenguaje con tipos modernos
- **PostgreSQL** — base de datos principal
- **Eloquent** — ORM de Laravel
- **Laravel Sanctum** — autenticación API (tokens)
- **Laravel Horizon** — gestión de queues con Redis
- **Pest** — testing moderno para PHP
- **Laravel Pint** — code formatter (basado en PHP-CS-Fixer)

## Structure

```
app/
  Http/
    Controllers/    # Controllers por recurso
    Middleware/     # Auth, throttle, etc.
    Requests/       # Form Requests (validación)
    Resources/      # API Resources (serialización)
  Models/           # Eloquent models
  Services/         # Lógica de negocio
  Actions/          # Single-purpose action classes
  Exceptions/       # Custom exceptions
database/
  migrations/
  factories/
  seeders/
routes/
  api.php           # API routes
  web.php           # Web routes
tests/
  Feature/
  Unit/
.env.example
```

## Decisions

- Form Requests para validación — no validar en controllers.
- API Resources para serialización — no devolver modelos Eloquent directamente.
- Services para lógica de negocio compleja; Actions para operaciones únicas.
- `php artisan make:` para todo — scaffolding consistente.
- Sanctum para auth API (stateless con tokens); Breeze/Jetstream para web auth.
