# react-ts

React 19 + TypeScript + Vite + Tailwind CSS

## Idea

A minimal but production-ready SPA starter. No framework opinions beyond React itself — ideal for dashboards, tools, or apps that don't need SSR.

## Stack

- **React 19** — UI library with concurrent features
- **TypeScript** — strict mode enabled
- **Vite** — fast dev server and bundler
- **Tailwind CSS v4** — utility-first styling
- **React Router v7** — client-side routing
- **TanStack Query** — server state management
- **Zustand** — client state management
- **Axios** — HTTP client with typed responses
- **ESLint + Prettier** — linting and formatting

## Structure

```
src/
  components/     # Shared UI components
  features/       # Feature-based modules (each has its own components, hooks, types)
  hooks/          # Global custom hooks
  lib/            # Third-party client setup (axios instance, queryClient, etc.)
  pages/          # Route-level components
  store/          # Zustand stores
  types/          # Global TypeScript types
  utils/          # Pure utility functions
```

## Decisions

- Feature-based folder structure scales better than type-based.
- TanStack Query handles all async/server state; Zustand only for true client state.
- Strict TypeScript: no `any`, explicit return types on exported functions.
- `.env.example` included; all env vars prefixed with `VITE_`.
