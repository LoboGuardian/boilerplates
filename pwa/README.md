# pwa

Progressive Web App — React + TypeScript + Vite + PWA

## Idea

Web app instalable que funciona offline. Un Service Worker cachea los assets y las respuestas de red — la app carga sin conexión. Se puede instalar en el home screen de Android, iOS, Windows y macOS sin pasar por una tienda de apps.

## Stack

- **React 19 + TypeScript** — UI
- **Vite** — bundler
- **vite-plugin-pwa** — genera Service Worker y Web Manifest automáticamente
- **Workbox** — librería de Service Worker (bajo el capó de vite-plugin-pwa)
- **Tailwind CSS v4** — styling
- **TanStack Query** — server state con soporte de cache offline

## Structure

```
src/
  components/
  pages/
  hooks/
  lib/
    queryClient.ts    # TanStack Query con persistencia offline
  sw/
    sw.ts             # Service Worker personalizado (si se necesita)
  App.tsx
public/
  icons/              # Iconos en múltiples tamaños (512, 192, 144, 96, 72, 48)
  screenshots/        # Capturas para la ficha de instalación
vite.config.ts        # Config del plugin PWA (manifest, workbox strategies)
```

## Web Manifest (en vite.config.ts)

```ts
manifest: {
  name: 'My App',
  short_name: 'App',
  theme_color: '#ffffff',
  icons: [{ src: 'icons/512.png', sizes: '512x512', type: 'image/png' }]
}
```

## Decisions

- `vite-plugin-pwa` genera el SW y el manifest — sin escribir Service Worker manualmente.
- Estrategia `NetworkFirst` para API calls, `CacheFirst` para assets estáticos.
- `TanStack Query` con `persistQueryClient` para cache offline de datos del servidor.
- Íconos generados en todos los tamaños requeridos por los distintos SO.
- HTTPS obligatorio en producción — el Service Worker no funciona en HTTP.
