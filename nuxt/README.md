# nuxt

Nuxt 3 + TypeScript + Tailwind CSS

## Idea

A full-stack Vue framework starter. Nuxt handles SSR, SSG, and API routes in one codebase. Great for Vue teams that want the same DX as Next.js but with Vue's syntax and conventions.

## Stack

- **Nuxt 3** — full-stack Vue framework
- **TypeScript** — strict mode, Nuxt auto-imports typed
- **Tailwind CSS v4** — styling via `@nuxtjs/tailwindcss`
- **Pinia** — state management (`@pinia/nuxt`)
- **Nuxt Auth Utils** — session-based auth (or `nuxt-auth` for Auth.js)
- **Prisma / Drizzle** — ORM (Drizzle for edge, Prisma for standard Node)
- **Zod** — validation for server routes and forms
- **ESLint + Prettier** — linting

## Structure

```
app/
  components/     # Auto-imported components
  composables/    # Auto-imported composables (like React hooks)
  layouts/        # Page layouts (default, auth, dashboard)
  pages/          # Filesystem-based routing
  stores/         # Pinia stores
server/
  api/            # API routes (nitro handlers)
  middleware/     # Server middleware (auth guards)
  utils/          # Server-only utilities
shared/
  types/          # Types shared between client and server
.env.example
nuxt.config.ts
```

## Decisions

- Nuxt auto-imports components, composables, and utils — no explicit imports needed in most files.
- Server routes in `server/api/` are Nitro handlers — they run in a separate context from Vue.
- `useAsyncData` and `useFetch` are the idiomatic way to fetch data in pages and components.
- Pinia stores are auto-imported; use them for global client state only.
- `shared/types/` for types needed on both client and server side.
