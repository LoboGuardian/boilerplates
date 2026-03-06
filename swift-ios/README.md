# swift-ios

Swift + SwiftUI + iOS nativo

## Idea

App iOS nativa con SwiftUI — el framework declarativo de Apple. Mismo código funciona en iOS, iPadOS, macOS (Mac Catalyst) y watchOS con adaptaciones mínimas. El stack que Apple recomienda para nuevas apps.

## Stack

- **Swift 6** — lenguaje con concurrencia estricta (strict concurrency)
- **SwiftUI** — UI declarativa de Apple
- **Swift Concurrency** — async/await, actors, TaskGroup
- **Combine** — streams reactivos (o AsyncStream/AsyncSequence)
- **SwiftData** — ORM local de Apple (reemplaza CoreData)
- **URLSession** — HTTP client nativo
- **XCTest** — testing (unit + UI)
- **Xcode** — IDE requerido (solo macOS)

## Structure

```
MyApp/
  App/
    MyApp.swift         # @main entry point
    AppDelegate.swift   # (si se necesita)
  Features/
    Home/
      HomeView.swift
      HomeViewModel.swift   # @Observable class
      HomeModel.swift
    Auth/
    Settings/
  Core/
    Network/
      APIClient.swift
      Endpoints.swift
    Database/
      SwiftDataManager.swift
    Extensions/
  Components/           # Views reutilizables
  Resources/
    Assets.xcassets
    Localizable.strings
MyAppTests/
MyAppUITests/
```

## Decisions

- `@Observable` (Swift 5.9+) para ViewModels — reemplaza `ObservableObject` + `@Published`.
- Swift Concurrency (async/await + actors) en lugar de callbacks o Combine para networking.
- SwiftData para persistencia local — sin XML de CoreData.
- Feature-based folder structure — cada feature tiene su View, ViewModel y Model.
- Preview providers en cada View para desarrollo sin correr el simulador.
- Swift 6 strict concurrency: todo thread-safe por el compilador.
