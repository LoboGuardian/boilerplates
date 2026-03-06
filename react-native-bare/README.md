# react-native-bare

React Native + TypeScript — bare workflow (sin Expo)

## Idea

React Native sin la capa de Expo. Control total sobre el código nativo (Android/iOS). Necesario cuando se usan módulos nativos que Expo no soporta, se integra con SDKs de terceros, o se necesita máxima optimización del bundle nativo.

## Stack

- **React Native 0.77** — framework mobile
- **TypeScript** — strict mode
- **React Navigation 7** — navegación (Stack, Tab, Drawer)
- **Zustand** — estado global
- **TanStack Query** — server state
- **Axios** — HTTP client
- **react-native-mmkv** — almacenamiento rápido (reemplaza AsyncStorage)
- **Reanimated 3** — animaciones de alta performance
- **Flashlist** — listas performantes (reemplaza FlatList)
- **Metro** — bundler de React Native

## Structure

```
src/
  api/              # Axios instance, endpoints
  components/       # Componentes reutilizables
  features/         # Feature-based modules
    auth/
      screens/
      hooks/
      types/
  navigation/
    RootNavigator.tsx
    types.ts        # Tipos de navegación (type-safe params)
  store/            # Zustand stores
  hooks/            # Custom hooks globales
  utils/
  theme/            # Colores, tipografía, spacing
android/            # Proyecto Android nativo
ios/                # Proyecto iOS nativo
```

## Decisions

- Bare workflow: acceso directo a `android/` e `ios/` — sin restricciones de Expo managed.
- MMKV sobre AsyncStorage: 10x más rápido, síncrono.
- Reanimated para animaciones — corren en el UI thread, nunca en el JS thread.
- Tipos de navegación centralizados en `navigation/types.ts` — params type-safe en todas las pantallas.
- Para módulos nativos: `yarn add lib && cd ios && pod install`.
