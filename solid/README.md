# solid

SolidJS + TypeScript + Vite + Tailwind CSS

## Idea

Framework reactivo con señales reales — sin Virtual DOM. Las actualizaciones van directo al DOM, lo que lo hace uno de los frameworks más rápidos disponibles. Sintaxis similar a React pero con un modelo mental más simple y predecible.

## Stack

- **SolidJS** — framework reactivo sin VDOM
- **TypeScript** — strict mode
- **Vite** — bundler
- **Tailwind CSS v4** — styling
- **SolidJS Router** — routing basado en señales
- **TanStack Query para Solid** — server state
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  components/       # Componentes reutilizables (.tsx)
  pages/            # Componentes de página (rutas)
  stores/           # createStore / createSignal globales
  hooks/            # Primitivas reutilizables (como custom hooks de React)
  lib/              # Setup de clientes externos
  types/            # TypeScript types globales
  utils/
  App.tsx
  index.tsx
```

## Decisions

- Sin VDOM: los componentes se ejecutan UNA sola vez — no hay re-renders del componente completo.
- `createSignal` para estado local, `createStore` para objetos/arrays anidados.
- `createMemo` para valores derivados (equivalente a `useMemo` pero automático).
- `createEffect` para side effects — se ejecuta cuando sus señales dependientes cambian.
- JSX en SolidJS compila diferente que React — no usar patrones de React directamente.
