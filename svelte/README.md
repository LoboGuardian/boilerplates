# svelte

SvelteKit + TypeScript + Tailwind CSS

## Idea

A full-stack SvelteKit starter that leverages its filesystem routing, form actions, and load functions. Svelte's compile-time approach means minimal runtime overhead — great for performance-sensitive apps.

## Stack

- **SvelteKit** — full-stack framework with filesystem routing
- **TypeScript** — svelte-check for type safety in templates
- **Tailwind CSS v4** — utility-first styling
- **Zod** — schema validation for form actions
- **Superforms** — form handling with validation
- **ESLint + Prettier (svelte plugin)** — linting and formatting

## Structure

```
src/
  lib/
    components/   # Reusable Svelte components
    server/       # Server-only utilities (DB, auth)
    utils/        # Shared utilities
  routes/
    (app)/        # Protected app routes
    (auth)/       # Auth pages
    api/          # API endpoints (+server.ts files)
```

## Decisions

- Use `+page.server.ts` load functions for data fetching — not client-side fetching on mount.
- Form actions (`+page.server.ts` actions) for mutations instead of separate API routes.
- Keep `$lib/server/` strictly server-side; SvelteKit enforces this boundary.
- Stores only for truly global UI state (theme, toasts).
