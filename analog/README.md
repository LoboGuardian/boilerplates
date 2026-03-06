# analog

Analog.js + Angular 19 + TypeScript + Tailwind CSS

## Idea

Meta-framework para Angular — lo que Next.js es para React. SSR, SSG, filesystem routing y API routes sobre Angular. Para equipos Angular que quieren las ventajas de un meta-framework sin abandonar su stack.

## Stack

- **Analog.js** — meta-framework Angular
- **Angular 19** — framework base con Signals
- **TypeScript** — strict mode
- **Vite** — dev server y bundler (reemplaza webpack en Angular)
- **Tailwind CSS v4** — styling
- **Nitro** — server engine para API routes (mismo que Nuxt)
- **Prisma** — ORM (opcional)
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  app/
    pages/          # Filesystem routing (.page.ts, .page.analog)
      index.page.ts
      blog/
        [slug].page.ts
    components/     # Componentes Angular reutilizables
    layouts/        # Layout components
  server/
    routes/         # API routes (Nitro handlers)
      api/
        users.get.ts
        users.post.ts
  content/          # Markdown content (blog posts, docs)
public/
vite.config.ts
```

## Decisions

- Archivo `.page.ts` es un componente Angular standalone — es la ruta.
- API routes en `server/routes/` son Nitro handlers — corren en el servidor.
- Signals de Angular 19 como sistema reactivo principal — sin RxJS donde no sea necesario.
- SSG para contenido estático (blog, docs); SSR para páginas dinámicas.
- Vite reemplaza el Angular CLI webpack builder — arranque y HMR mucho más rápido.
