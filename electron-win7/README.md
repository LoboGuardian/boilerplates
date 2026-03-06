# electron-win7

Electron 22 + TypeScript + Vite — Windows 7 compatible

## Idea

Electron 22 es la última versión que soporta Windows 7/8/8.1. A partir de Electron 23 se requiere Windows 10+. Usa el mismo stack que el template `electron` pero fijado en versiones compatibles con Windows legacy.

## Stack

- **Electron 22** — última versión con soporte Windows 7 (Chromium 108)
- **TypeScript** — en main y renderer
- **Vite** — bundler del frontend
- **React 18** — UI en el renderer
- **electron-builder** — packaging y distribución
- **electron-store** — persistencia local

## Compatibility

| OS | Soporte |
|---|---|
| Windows 7 SP1 | Si (requiere KB2533623) |
| Windows 8/8.1 | Si |
| Windows 10/11 | Si |
| macOS 10.13+ | Si |
| Linux | Si |

## Structure

```
src/
  main/
    index.ts          # BrowserWindow, app lifecycle
    ipc/              # IPC handlers
  preload/
    index.ts          # contextBridge API
  renderer/
    src/
      App.tsx
      components/
electron-builder.yml  # Config de packaging
package.json          # electron fijado a ^22.x
```

## Decisions

- Fijar `"electron": "^22.3.25"` en `package.json` — no actualizar a 23+.
- Fijar `"electron-builder": "^24.x"` — compatible con Electron 22.
- No usar APIs de Windows 10+ en el proceso main (notificaciones nativas modernas, etc.).
- `squirrel.windows` target en electron-builder para instalador compatible con Windows 7.
- Context Isolation + contextBridge — igual que en el template moderno, es compatible con Windows 7.
