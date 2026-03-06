# chrome-extension

Chrome/Firefox Extension — TypeScript + React + Vite

## Idea

Extensión de navegador compatible con Chrome, Edge y Firefox (Manifest V3). React para la UI del popup y las páginas de opciones. Vite para el build. Manifest V3 es el estándar actual — Manifest V2 está siendo deprecado en Chrome.

## Stack

- **TypeScript** — strict mode
- **React 19** — UI del popup y páginas de opciones
- **Vite + CRXJS** — bundler con HMR para extensiones
- **Tailwind CSS v4** — styling
- **Zod** — validación de mensajes entre contexts
- **@webext-core/messaging** — comunicación tipada entre contextos

## Structure

```
src/
  background/
    index.ts          # Service Worker (background script MV3)
  content/
    index.ts          # Content script (se inyecta en páginas)
  popup/
    index.html
    index.tsx         # React app del popup
    App.tsx
  options/
    index.html
    index.tsx         # React app de la página de opciones
  components/         # Componentes React compartidos
  lib/
    storage.ts        # chrome.storage wrapper tipado
    messaging.ts      # Mensajes tipados entre contextos
public/
  icons/
    16.png
    48.png
    128.png
manifest.json         # Manifest V3
vite.config.ts
```

## Decisions

- Manifest V3: background script es un Service Worker (sin DOM, sin estado persistente en memoria).
- Mensajes tipados con `@webext-core/messaging` — no `chrome.runtime.sendMessage` crudo.
- `chrome.storage.local` para persistencia — no `localStorage` (no funciona en Service Workers).
- CRXJS Vite plugin: HMR en popup y options sin rebuild manual.
- Content scripts son JS puro o con React montado en un Shadow DOM para evitar conflictos de estilos.
- Compatible con Firefox cambiando `chrome.*` por `browser.*` (usando `webextension-polyfill`).
