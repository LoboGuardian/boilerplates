# t3

T3 Stack — Next.js + tRPC + Prisma + Tailwind + Auth.js

## Idea

The T3 Stack's philosophy: only add complexity when it's justified. TypeScript everywhere, end-to-end type safety from the database to the React component via tRPC, with no code generation or schema syncing required.

## Stack

- **Next.js 15** — App Router
- **TypeScript** — strict mode
- **tRPC v11** — end-to-end type-safe API layer
- **Prisma** — ORM
- **PostgreSQL** — primary database
- **Auth.js v5** — authentication
- **Tailwind CSS v4** — styling
- **TanStack Query** — server state management (used under the hood by tRPC)
- **Zod** — input validation for tRPC procedures
- **ESLint + Prettier** — linting and formatting

## Structure

```
src/
  app/            # Next.js App Router pages and layouts
  components/     # Shared UI components
  server/
    api/
      routers/    # tRPC routers (one per domain)
      root.ts     # Root router
      trpc.ts     # tRPC initialization, context, middleware
    auth.ts       # Auth.js config
    db.ts         # Prisma client
  trpc/
    react.tsx     # Client-side tRPC provider + hooks
    server.ts     # Server-side caller (for RSC)
prisma/
  schema.prisma
```

## Decisions

- tRPC replaces REST/GraphQL: types flow from procedure definition to React hook automatically.
- Procedures are organized by domain (users, posts) not by HTTP verb.
- Protected procedures use tRPC middleware — no manual auth checks per route.
- Use tRPC server caller in Server Components for initial data, client hooks for interactive updates.
- Prisma schema is the single source of truth for data shape.
