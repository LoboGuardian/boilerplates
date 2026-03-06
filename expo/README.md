# expo

React Native + Expo + TypeScript

## Idea

Desarrollo mobile cross-platform (iOS + Android) con React Native gestionado por Expo. El SDK de Expo provee acceso a APIs nativas sin configurar Xcode ni Android Studio. Expo Router para navegación basada en archivos.

## Stack

- **Expo SDK 52** — plataforma managed para React Native
- **React Native** — framework mobile
- **TypeScript** — strict mode
- **Expo Router** — filesystem routing (como Next.js para mobile)
- **NativeWind v4** — Tailwind CSS para React Native
- **TanStack Query** — server state management
- **Zustand** — client state
- **Expo SecureStore** — almacenamiento seguro de tokens
- **React Hook Form + Zod** — formularios con validación

## Structure

```
app/
  (auth)/           # Grupo de rutas de autenticación
    login.tsx
    register.tsx
  (tabs)/           # Navegación por tabs
    index.tsx       # Home
    profile.tsx
  _layout.tsx       # Root layout
components/
  ui/               # Componentes base
  features/         # Componentes por feature
hooks/              # Custom hooks
lib/
  api.ts            # Cliente HTTP (axios o fetch con interceptors)
  queryClient.ts
store/              # Zustand stores
constants/          # Colores, tamaños, strings
assets/             # Imágenes, fonts, iconos
```

## Decisions

- Expo Managed Workflow: sin tocar código nativo a menos que sea necesario.
- Expo Router para navegación — type-safe con TypeScript.
- NativeWind para estilos — reutilizar conocimiento de Tailwind.
- SecureStore para tokens JWT — nunca AsyncStorage para datos sensibles.
- EAS Build para generar APK/IPA en la nube sin configurar entornos locales.
