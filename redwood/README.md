# redwood

RedwoodJS + React + GraphQL + Prisma + TypeScript

## Idea

Full-stack framework opinionated para startups. Une React en el frontend con GraphQL (Apollo) y Prisma en el backend. Todo en un monorepo con generadores de código para máxima velocidad de desarrollo.

## Stack

- **RedwoodJS** — full-stack framework
- **React** — frontend
- **GraphQL + Apollo** — API layer
- **Prisma** — ORM
- **PostgreSQL** — base de datos
- **TypeScript** — generado automáticamente desde el schema GraphQL
- **Tailwind CSS** — styling
- **Jest + Storybook** — testing y component development

## Structure

```
api/
  src/
    graphql/          # SDL files (schema GraphQL)
      users.sdl.ts
    services/         # Resolvers y lógica de negocio
      users/
        users.ts
        users.scenarios.ts  # Test fixtures
        users.test.ts
    lib/
      db.ts           # Prisma client
      auth.ts         # Auth decoder
  db/
    schema.prisma
web/
  src/
    components/       # Componentes React
    layouts/          # Layouts de página
    pages/            # Páginas (filesystem routing)
```

## Decisions

- Monorepo: `api/` y `web/` en el mismo repo con Yarn workspaces.
- Redwood genera types TypeScript del schema SDL automáticamente.
- Services son los resolvers GraphQL — contienen toda la lógica de negocio.
- Cells: patrón de Redwood para data fetching (QUERY + Loading/Empty/Failure/Success states).
- `yarn rw generate scaffold <model>` crea CRUD completo (SDL, service, pages, components).
