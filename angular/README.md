# angular

Angular 19 + TypeScript + Tailwind CSS

## Idea

Framework enterprise de Google. Opinionated, con todo incluido: DI, routing, forms, HTTP client, testing. Ideal para equipos grandes donde la consistencia importa más que la flexibilidad.

## Stack

- **Angular 19** — framework SPA completo (signals-based)
- **TypeScript** — strict mode (Angular lo requiere)
- **Tailwind CSS v4** — styling
- **Angular Router** — routing con lazy loading
- **Angular HttpClient** — HTTP con interceptors
- **RxJS** — programación reactiva
- **Signals** — state management moderno (reemplaza NgRx para casos simples)
- **NgRx** — state management complejo (opcional)
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  app/
    core/           # Singleton services, guards, interceptors
      services/
      guards/
      interceptors/
    features/       # Feature modules con lazy loading
      dashboard/
        dashboard.component.ts
        dashboard.routes.ts
        dashboard.service.ts
      auth/
    shared/         # Componentes, pipes y directivas reutilizables
      components/
      pipes/
      directives/
    app.routes.ts   # Root routes
    app.config.ts   # App config (standalone components)
  environments/
```

## Decisions

- Standalone components (sin NgModules) — Angular 19 los prefiere.
- Signals para estado local y compartido simple; NgRx solo para estado global complejo.
- Lazy loading en todas las feature routes — `loadChildren` con dynamic import.
- Interceptors para auth headers y error handling global.
- Smart/dumb component pattern: smart components obtienen datos, dumb solo reciben `@Input`.
