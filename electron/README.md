# electron

Electron + TypeScript + Vite + React

## Idea

Apps de escritorio con tecnologías web. Empaca Chromium + Node.js — mayor compatibilidad pero binarios más grandes que Tauri. Ideal cuando se necesita acceso completo a Node.js en el proceso principal o se migra una app web existente a desktop.

## Stack

- **Electron 33** — framework desktop
- **TypeScript** — strict mode en main y renderer
- **Vite + electron-vite** — bundler unificado para ambos procesos
- **React 19** — UI en el renderer
- **Tailwind CSS v4** — styling
- **electron-store** — persistencia de configuración
- **Vitest** — testing

## Structure

```
src/
  main/               # Proceso principal (Node.js + Electron APIs)
    index.ts          # Entry point, crea BrowserWindow
    ipc/              # IPC handlers (responden llamadas del renderer)
    services/         # Servicios nativos (fs, notifications, tray)
  preload/            # Script de preload (puente seguro main↔renderer)
    index.ts          # Expone API via contextBridge
  renderer/           # Proceso renderer (React app)
    src/
      components/
      pages/
      hooks/
        useElectron.ts  # Hook para llamar la API expuesta por preload
      App.tsx
electron-builder.yml    # Config de empaquetado y distribución
```

## Decisions

- Context Isolation + contextBridge: el renderer nunca importa módulos de Node directamente.
- IPC tipado: preload expone funciones nombradas, no `ipcRenderer.invoke` crudo.
- `electron-vite` reemplaza webpack — HMR en renderer, watch en main/preload.
- `electron-builder` para distribución: instaladores para Windows, macOS, Linux.
- Actualizaciones automáticas con `electron-updater`.
