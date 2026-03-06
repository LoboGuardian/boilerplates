# nestjs

NestJS + TypeScript + Prisma + PostgreSQL

## Idea

Framework Node.js de grado enterprise con arquitectura Angular-like: módulos, decoradores, DI. Ideal para APIs complejas donde la estructura y testabilidad son prioridad.

## Stack

- **NestJS 10** — framework Node.js con decoradores
- **TypeScript** — strict mode
- **Prisma** — ORM
- **PostgreSQL** — base de datos
- **Passport + JWT** — autenticación
- **class-validator + class-transformer** — validación de DTOs
- **Swagger (OpenAPI)** — documentación automática
- **Jest** — testing (unit + e2e)
- **ESLint + Prettier** — linting y formatting

## Structure

```
src/
  auth/             # Módulo de autenticación
    auth.module.ts
    auth.controller.ts
    auth.service.ts
    strategies/     # Passport strategies (jwt, local)
    guards/
    dto/
  users/            # Módulo de usuarios
    users.module.ts
    users.controller.ts
    users.service.ts
    dto/
  common/           # Decoradores, filtros, interceptors, pipes globales
    filters/        # Exception filters
    interceptors/
    decorators/
  prisma/           # PrismaService (módulo global)
  app.module.ts     # Root module
  main.ts           # Bootstrap
test/
  app.e2e-spec.ts
```

## Decisions

- Un módulo por dominio — cada uno es autocontenido con su controller, service y DTOs.
- DTOs con `class-validator` para validación automática vía `ValidationPipe` global.
- `PrismaModule` global para no importarlo en cada módulo.
- Swagger habilitado en dev — decoradores `@ApiProperty` en todos los DTOs.
- Guards a nivel de controller o route, no hardcodeados en services.
