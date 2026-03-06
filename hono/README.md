# hono

Hono + TypeScript — edge-ready API

## Idea

An ultra-lightweight API built with Hono. Runs on Node.js, Deno, Bun, Cloudflare Workers, or any WinterCG-compatible runtime. Ideal for APIs that need to run at the edge or in serverless environments.

## Stack

- **Hono** — web framework for the edge
- **TypeScript** — strict mode
- **Zod + @hono/zod-validator** — request validation
- **Hono RPC** — type-safe client (optional, full-stack use)
- **Drizzle ORM** — lightweight, edge-compatible ORM
- **PostgreSQL / D1 / Turso** — database (runtime-dependent)
- **Biome** — fast linting and formatting

## Structure

```
src/
  routes/         # One file per resource, using Hono's chained API
  middleware/     # Auth (JWT), logger, CORS
  db/             # Drizzle client and schema
  validators/     # Zod schemas for requests
  lib/            # Shared utilities
  index.ts        # App entry point
```

## Decisions

- Use Hono's built-in RPC mode to share types between server and client without tRPC overhead.
- Drizzle chosen over Prisma for edge compatibility (no native binaries).
- All middleware is Hono-native — no Express-style compatibility layers.
- Target runtime is set in `package.json` scripts (Node by default, easy to swap to Bun or Workers).
