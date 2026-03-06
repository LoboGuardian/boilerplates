# elysia

Elysia + Bun + TypeScript

## Idea

Framework web nativo de Bun. El más rápido en benchmarks Node/Bun. Type safety end-to-end sin código generado — los tipos fluyen del schema de la ruta al cliente automáticamente via Eden Treaty.

## Stack

- **Elysia** — framework web para Bun
- **Bun** — runtime, bundler y test runner
- **TypeScript** — strict mode
- **Eden Treaty** — cliente HTTP type-safe (como tRPC pero para REST)
- **Drizzle ORM** — ORM edge-compatible
- **PostgreSQL** — base de datos (via `bun:sqlite` para proyectos pequeños)
- **Zod / TypeBox** — validación de schemas

## Structure

```
src/
  modules/          # Feature modules agrupados con Elysia plugins
    users/
      users.plugin.ts   # Elysia plugin con rutas del módulo
      users.service.ts
      users.schema.ts   # TypeBox o Zod schemas
    auth/
  middleware/         # Plugins globales (logger, cors, auth)
  db/
    schema.ts         # Drizzle schema
    index.ts          # Drizzle client
  lib/               # Utilidades compartidas
  index.ts           # Entry point
```

## Decisions

- Plugins de Elysia como unidad de modularización — cada feature es un plugin.
- TypeBox preferido sobre Zod (nativo en Elysia, mejor performance).
- Eden Treaty para clientes TypeScript: types del servidor disponibles en el cliente sin generación.
- Drizzle sobre Prisma: compatible con Bun sin binarios nativos.
- `Bun.serve()` bajo el capó — no necesita Express ni adaptadores.
