# spring-boot

Java + Spring Boot 3 + Spring Data JPA + PostgreSQL

## Idea

El framework enterprise Java por excelencia. Ecosistema maduro, con soluciones para todo: seguridad, mensajería, batch, microservicios. Ideal para organizaciones con experiencia Java o requisitos enterprise.

## Stack

- **Java 21** — LTS con virtual threads (Project Loom)
- **Spring Boot 3.3** — framework con autoconfiguration
- **Spring Data JPA + Hibernate** — ORM
- **PostgreSQL** — base de datos
- **Spring Security + JWT** — autenticación y autorización
- **Flyway** — migraciones de base de datos
- **MapStruct** — mapeo entre DTOs y entidades
- **JUnit 5 + Mockito** — testing
- **Maven** — build tool

## Structure

```
src/
  main/
    java/com/example/app/
      config/           # Spring configs (Security, CORS, Swagger)
      controller/       # REST Controllers
      service/          # Lógica de negocio (interfaces + implementaciones)
      repository/       # Spring Data JPA repositories
      entity/           # JPA entities
      dto/              # Request/Response DTOs
        request/
        response/
      mapper/           # MapStruct mappers
      exception/        # Custom exceptions + GlobalExceptionHandler
      security/         # JWT filter, UserDetailsService
    resources/
      application.yml
      application-dev.yml
      application-prod.yml
      db/migration/     # Flyway SQL migrations
  test/
pom.xml
```

## Decisions

- Virtual threads (Java 21) habilitados — máximo throughput sin código reactivo complejo.
- DTOs siempre: nunca exponer entidades JPA en la API.
- MapStruct para mapeo entity↔DTO en compile time (sin reflection en runtime).
- `GlobalExceptionHandler` con `@ControllerAdvice` para manejo centralizado de errores.
- Perfiles de Spring (`dev`, `prod`) para configuración por entorno.
