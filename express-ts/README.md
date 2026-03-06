# express-ts

Node.js + Express + TypeScript + Zod + Prisma

## Idea

A classic but modern Express API starter. TypeScript end-to-end, with Zod for runtime validation and Prisma as the ORM. Suitable when you want full control over the HTTP layer without a heavier framework.

## Stack

- **Express 5** — HTTP framework
- **TypeScript** — strict mode, `tsx` for dev
- **Zod** — request validation and schema inference
- **Prisma** — ORM with type-safe queries
- **PostgreSQL** — primary database
- **JWT (jose)** — authentication
- **Pino** — structured JSON logging
- **Vitest** — unit and integration testing
- **ESLint + Prettier** — linting and formatting

## Structure

```
src/
  config/         # Environment config (validated with Zod)
  db/             # Prisma client singleton
  middleware/     # Auth, error handler, request logger
  modules/        # Feature modules (users/, posts/, etc.)
    users/
      users.router.ts
      users.controller.ts
      users.service.ts
      users.schema.ts   # Zod schemas
  lib/            # Utilities (jwt, bcrypt wrappers)
  app.ts          # Express app setup
  server.ts       # Entry point (starts HTTP server)
prisma/
  schema.prisma
.env.example
```

## Decisions

- Module-based structure: each resource owns its router, controller, service, and schema.
- Controller handles HTTP concerns only; business logic lives in services.
- Zod schemas are the single source of truth for input types — infer TypeScript types from them.
- Centralized error handler middleware catches all thrown errors.
- No `any` — Prisma and Zod provide full type coverage.
