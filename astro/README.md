# astro

Astro + TypeScript + Tailwind CSS

## Idea

Static-first framework con islands architecture. Envía cero JavaScript por defecto — solo hidrata los componentes que realmente necesitan interactividad. Ideal para blogs, portfolios, documentación y landing pages.

## Stack

- **Astro 5** — static site generator con islands
- **TypeScript** — strict mode
- **Tailwind CSS v4** — styling
- **MDX** — contenido con componentes embebidos
- **React / Vue / Svelte** — para islands interactivas (elige uno)
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  components/     # Componentes Astro y de UI framework
    islands/      # Componentes con client: directives (interactivos)
  content/        # Content Collections (blog posts, docs)
    blog/
    docs/
  layouts/        # Layouts reutilizables
  pages/          # Filesystem routing (.astro, .md, .mdx)
  styles/         # CSS global
public/           # Assets estáticos (no procesados)
astro.config.mjs
```

## Decisions

- Componentes `.astro` por defecto — sin JS en el cliente.
- Islands solo cuando hay interactividad real: usar `client:visible` para lazy hydration.
- Content Collections tipadas con Zod para frontmatter validation.
- SSG por defecto; cambiar `output: 'server'` solo si se necesita SSR.
- Un solo UI framework para islands — no mezclar React + Vue en el mismo proyecto.
