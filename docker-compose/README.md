# docker-compose

Docker + Docker Compose — entorno multi-servicio

## Idea

Base de infraestructura local con Docker Compose. Define el stack completo de servicios (app, base de datos, cache, proxy) para que cualquier desarrollador levante el entorno con un solo comando. Agnóstico del lenguaje de la aplicación.

## Stack

- **Docker** — contenedores
- **Docker Compose** — orquestación local
- **Nginx** — reverse proxy (termina SSL, sirve archivos estáticos)
- **PostgreSQL** — base de datos principal
- **Redis** — cache y message broker
- **Adminer** — UI web para la BD (solo en dev)

## Structure

```
docker/
  nginx/
    nginx.conf        # Config del reverse proxy
    conf.d/
      app.conf        # Virtual host de la app
  postgres/
    init.sql          # Scripts de inicialización
  redis/
    redis.conf
docker-compose.yml        # Stack completo (prod-like)
docker-compose.override.yml  # Overrides para desarrollo local
docker-compose.test.yml   # Stack mínimo para tests CI
.env.example
Makefile              # make up, make down, make logs, make shell
```

## docker-compose.yml (servicios tipo)

```yaml
services:
  app:       # La aplicación principal
  db:        # PostgreSQL
  redis:     # Redis
  nginx:     # Reverse proxy
  adminer:   # BD UI (solo dev, comentado en prod)
```

## Decisions

- `docker-compose.override.yml` extiende el base automáticamente en dev (volumes para hot reload, puertos expuestos, Adminer).
- Variables de entorno desde `.env` — nunca hardcodeadas en el compose.
- Healthchecks en todos los servicios — `depends_on: condition: service_healthy`.
- Named volumes para datos persistentes (no bind mounts para BD).
- `Makefile` como interfaz: `make up`, `make down`, `make logs app`, `make shell app`.
