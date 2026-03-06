# flutter

Flutter + Dart + Riverpod

## Idea

Framework de Google para apps cross-platform: iOS, Android, Web, Desktop (Windows, macOS, Linux) desde un solo codebase. Renderiza sus propios widgets — no usa componentes nativos del SO, garantizando consistencia visual total.

## Stack

- **Flutter 3.27+** — framework UI cross-platform
- **Dart 3** — lenguaje (null safety, records, patterns)
- **Riverpod 2** — state management (code-gen based)
- **go_router** — routing declarativo
- **Dio** — HTTP client
- **Freezed** — data classes inmutables con code generation
- **flutter_secure_storage** — almacenamiento seguro
- **very_good_analysis** — linting estricto

## Structure

```
lib/
  core/
    router/         # go_router config y guards
    theme/          # ThemeData, colores, tipografía
    network/        # Dio client, interceptors
    error/          # Failure classes con Freezed
  features/
    auth/
      data/         # Datasources, models, repository impl
      domain/       # Entities, repository interfaces, use cases
      presentation/ # Providers (Riverpod), screens, widgets
    home/
  shared/
    widgets/        # Widgets reutilizables
  main.dart
  app.dart          # MaterialApp + ProviderScope
```

## Decisions

- Clean Architecture por feature: data → domain → presentation.
- Riverpod con code generation (`@riverpod`) — providers tipados sin boilerplate.
- Freezed para models y estados — immutability y pattern matching garantizados.
- go_router para routing declarativo con guards de autenticación.
- `flutter_gen` para references type-safe a assets (imágenes, fonts).
