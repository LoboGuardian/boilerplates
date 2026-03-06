# vue-ts

Vue 3 + TypeScript + Vite + Tailwind CSS

## Idea

A clean Vue 3 SPA using the Composition API throughout. Equivalent in scope to `react-ts` but for teams that prefer Vue's conventions and template syntax.

## Stack

- **Vue 3** — Composition API, `<script setup>` syntax
- **TypeScript** — strict mode
- **Vite** — dev server and bundler
- **Tailwind CSS v4** — utility-first styling
- **Vue Router 4** — client-side routing
- **Pinia** — state management (Vue's official store)
- **TanStack Query for Vue** — server state management
- **Axios** — HTTP client
- **ESLint + Prettier** — linting and formatting (vue-tsc for type checking)

## Structure

```
src/
  components/     # Shared UI components
  composables/    # Reusable Composition API logic (like React hooks)
  features/       # Feature-based modules
  lib/            # Third-party setup (axios, queryClient)
  pages/          # Route-level views
  router/         # Vue Router config
  stores/         # Pinia stores
  types/          # Global TypeScript types
  utils/          # Pure utilities
```

## Decisions

- Always use `<script setup lang="ts">` — no Options API.
- Pinia for global/client state; TanStack Query for server state.
- Composables mirror the pattern of React custom hooks.
- `defineProps` and `defineEmits` with full TypeScript types.
