# nextjs

Next.js 15 App Router + TypeScript + Tailwind CSS

## Idea

A lean Next.js starter using the App Router. Focused on server components by default, with client components only where interactivity is needed. Good for content-heavy sites, marketing pages, and apps that benefit from SSR/SSG.

## Stack

- **Next.js 15** — App Router, Server Components, Server Actions
- **TypeScript** — strict mode
- **Tailwind CSS v4** — utility-first styling
- **next-auth v5** — authentication (optional, pre-wired)
- **Zod** — schema validation for forms and API routes
- **ESLint + Prettier** — linting and formatting

## Structure

```
app/
  (auth)/         # Auth route group (login, register)
  (main)/         # Main app route group
  api/            # API route handlers
  layout.tsx      # Root layout
  page.tsx        # Home page
components/
  ui/             # Base UI primitives
  layout/         # Header, footer, sidebar
lib/
  auth.ts         # next-auth config
  db.ts           # DB client (if used)
  validations/    # Zod schemas
types/            # Global types
```

## Decisions

- Server Components are the default; use `"use client"` only when necessary.
- Server Actions replace most API routes for mutations.
- Route groups `(name)` keep layouts isolated without affecting the URL.
- Metadata API used for SEO on all pages.
