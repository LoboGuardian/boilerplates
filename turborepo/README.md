# turborepo

Turborepo + pnpm workspaces + TypeScript

## Idea

Monorepo para múltiples apps y paquetes compartidos. Turborepo cachea resultados de build/test/lint — solo re-ejecuta lo que cambió. Ideal cuando tienes una app web, una mobile, y una librería compartida en el mismo repo.

## Stack

- **Turborepo** — build system con caché incremental
- **pnpm workspaces** — gestión de paquetes en monorepo
- **TypeScript** — compartido via paquete `@repo/typescript-config`
- **ESLint** — compartido via paquete `@repo/eslint-config`
- **Changesets** — versionado y changelogs para paquetes publicables

## Structure

```
apps/
  web/              # Next.js app principal
  docs/             # Documentación (Astro o Next.js)
  mobile/           # Expo app (opcional)
packages/
  ui/               # Librería de componentes React compartida
  api-client/       # Cliente HTTP tipado compartido
  utils/            # Utilidades puras compartidas
  typescript-config/# tsconfig.json base compartido
  eslint-config/    # ESLint config compartida
turbo.json          # Pipeline de tareas (build, test, lint)
pnpm-workspace.yaml
package.json
```

## Decisions

- Cada workspace tiene su propio `package.json` — son paquetes independientes.
- `turbo.json` define el pipeline: qué tareas dependen de cuáles, qué se cachea.
- Paquetes internos se importan como `@repo/ui` — pnpm resuelve el workspace.
- `packages/ui` usa `tsup` para compilar — las apps consumen el código compilado.
- Caché remota de Turborepo (Vercel) para compartir caché entre CI y desarrolladores.
