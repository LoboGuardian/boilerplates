# kotlin-android

Kotlin + Jetpack Compose + Android nativo

## Idea

App Android nativa con el stack moderno de Google. Jetpack Compose reemplaza XML para la UI — UI declarativa en Kotlin puro. Architecture Components para MVVM y navegación. El stack que Google recomienda para nuevas apps Android.

## Stack

- **Kotlin** — lenguaje oficial de Android
- **Jetpack Compose** — UI toolkit declarativo
- **Android SDK** — APIs nativas de Android
- **ViewModel + StateFlow** — MVVM y estado reactivo
- **Navigation Compose** — navegación type-safe
- **Hilt** — inyección de dependencias (Dagger simplificado)
- **Room** — base de datos local SQLite con corrutinas
- **Retrofit + OkHttp** — HTTP client
- **Coil** — carga de imágenes async
- **Kotlin Coroutines + Flow** — async y streams reactivos

## Structure

```
app/src/main/
  java/com/example/app/
    di/               # Módulos de Hilt
    data/
      local/          # Room DAOs, entities, database
      remote/         # Retrofit services, DTOs
      repository/     # Implementaciones de repositorios
    domain/
      model/          # Modelos de dominio
      repository/     # Interfaces de repositorios
      usecase/        # Use cases
    ui/
      navigation/     # NavGraph, Routes
      screens/        # Composables por pantalla
        home/
          HomeScreen.kt
          HomeViewModel.kt
      components/     # Composables reutilizables
      theme/          # MaterialTheme, colores, tipografía
    MainActivity.kt
  res/
    values/           # strings.xml, colors.xml
    drawable/
```

## Decisions

- Clean Architecture en capas: UI → Domain → Data.
- ViewModel expone `StateFlow<UiState>` — la UI solo observa y envía eventos.
- Hilt para DI — anotaciones simples, sin boilerplate de Dagger manual.
- Room con corrutinas — todas las operaciones de BD son suspend functions.
- `sealed class UiState` para representar Loading/Success/Error en cada pantalla.
