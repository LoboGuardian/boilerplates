# nextjs-fullstack

Next.js 15 + Prisma + PostgreSQL + Tailwind CSS + Auth.js

## Idea

A full-stack Next.js app where the frontend and backend live in the same codebase. Server Actions handle mutations, server components handle data fetching, and Prisma provides a type-safe DB layer. No separate API service needed.

## Stack

- **Next.js 15** — App Router, Server Components, Server Actions
- **TypeScript** — strict mode
- **Tailwind CSS v4** — styling
- **Prisma** — ORM with migrations
- **PostgreSQL** — primary database
- **Auth.js v5** — authentication (OAuth + credentials)
- **Zod** — server action input validation
- **Resend** — transactional email (optional)
- **ESLint + Prettier** — linting and formatting

## Structure

```
app/
  (auth)/         # Login, register, verify pages
  (dashboard)/    # Protected app pages
  api/            # Webhooks and external API routes only
actions/          # Server Actions (one file per domain)
components/
  ui/             # Primitive components (Button, Input, etc.)
  features/       # Feature-specific components
lib/
  auth.ts         # Auth.js config
  db.ts           # Prisma client singleton
  validations/    # Zod schemas used in actions
prisma/
  schema.prisma
.env.example
```

## Decisions

- Server Actions replace API routes for all user-initiated mutations.
- `lib/db.ts` exports a single Prisma client instance (avoids connection pool exhaustion in dev).
- Auth middleware in `middleware.ts` protects routes at the edge.
- Avoid `useEffect` for data fetching — use async server components or `use` hook.
