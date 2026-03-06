# capacitor

Capacitor + Ionic + React/Vue/Angular — web app empaquetada como mobile

## Idea

Convierte una web app en app móvil nativa (iOS + Android) con acceso a APIs del dispositivo. Capacitor es el bridge entre el WebView y las APIs nativas. Ideal cuando ya tienes una web app y quieres publicarla en las tiendas con funcionalidades nativas.

## Stack

- **Capacitor 6** — bridge nativo (iOS + Android + PWA)
- **Ionic Framework 8** — componentes UI adaptados a mobile
- **React / Vue / Angular** — framework web (elige uno)
- **TypeScript** — strict mode
- **Capacitor Plugins** — Camera, Filesystem, Geolocation, Push Notifications, etc.
- **Vite** — bundler

## Structure

```
src/
  components/       # Componentes Ionic + framework elegido
  pages/            # Páginas de la app
  hooks/            # Custom hooks
  services/         # Lógica y llamadas a plugins de Capacitor
    camera.service.ts
    storage.service.ts
  theme/            # variables.css — colores y tema Ionic
  App.tsx           # Ionic + IonRouterOutlet
android/            # Proyecto Android nativo (Gradle)
ios/                # Proyecto iOS nativo (Xcode)
capacitor.config.ts # Config de Capacitor (appId, appName, server)
```

## Decisions

- Ionic para UI: sus componentes se adaptan automáticamente al look de iOS o Android.
- Capacitor Plugins sobre Cordova — API más limpia y moderna.
- `@capacitor/preferences` para persistencia local — reemplaza localStorage con almacenamiento nativo.
- Live reload en dispositivo: `npx ionic cap run android --livereload`.
- Para plugins nativos personalizados: crear un plugin de Capacitor en Swift/Kotlin.
