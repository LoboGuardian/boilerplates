# qwik

Qwik City + TypeScript + Tailwind CSS

## Idea

Framework con resumability — en vez de hidratar toda la app al cargar (como React/Vue), Qwik serializa el estado en el HTML y reanuda exactamente donde el servidor lo dejó. Tiempo de interactividad cercano a cero sin importar el tamaño de la app.

## Stack

- **Qwik + Qwik City** — framework con resumability
- **TypeScript** — strict mode
- **Vite** — bundler
- **Tailwind CSS v4** — styling
- **Zod** — validación de forms y actions
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  components/       # Componentes Qwik reutilizables
  routes/           # Filesystem routing (Qwik City)
    index.tsx       # Home page
    layout.tsx      # Root layout
    api/            # Server endpoints
  lib/              # Utilidades compartidas
  media/            # Imágenes y assets
public/             # Assets estáticos
vite.config.ts
```

## Decisions

- `component$()` — el `$` indica que el código puede ser lazy-loaded automáticamente.
- `useSignal()` y `useStore()` para estado reactivo local.
- `routeLoader$()` para cargar datos en el servidor antes de renderizar.
- `routeAction$()` para mutaciones — equivalente a Server Actions de Next.js.
- Evitar importar lógica pesada en el cliente: Qwik la lazy-carga, pero es mejor ser explícito.
