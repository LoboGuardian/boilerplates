# remix

Remix + TypeScript + Prisma + Tailwind CSS

## Idea

Full-stack React framework centrado en web fundamentals: forms, HTTP, y progressive enhancement. Los loaders y actions corren en el servidor — el cliente recibe HTML funcional antes de que cargue el JS.

## Stack

- **Remix 2** — full-stack React framework
- **TypeScript** — strict mode
- **Tailwind CSS v4** — styling
- **Prisma** — ORM
- **PostgreSQL** — base de datos
- **Zod** — validación en actions
- **ESLint + Prettier** — linting y formatting

## Structure

```
app/
  components/     # Componentes UI compartidos
  lib/
    db.server.ts  # Prisma client (sufijo .server.ts = solo servidor)
    session.server.ts # Session management
    auth.server.ts
  routes/         # Filesystem routing (loaders + actions + UI en un archivo)
    _index.tsx
    dashboard/
      _layout.tsx
      index.tsx
  root.tsx        # Root layout, ErrorBoundary global
prisma/
  schema.prisma
public/
.env.example
```

## Decisions

- Archivos `.server.ts` nunca se incluyen en el bundle del cliente — Remix lo enforcea.
- Cada route puede exportar `loader` (GET), `action` (POST/PUT/DELETE), y el componente React.
- Usar `<Form>` de Remix en vez de `fetch` manual — funciona sin JS y con JS.
- Nested routes para layouts compartidos — evitar duplicar headers/sidebars.
- Error boundaries por route — errores aislados, no pantalla blanca global.
