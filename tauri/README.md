# tauri

Tauri 2 + React + TypeScript + Rust

## Idea

Apps de escritorio cross-platform (Windows, macOS, Linux) con frontend web y backend Rust. Mucho más liviano que Electron: usa el WebView del sistema operativo en vez de empacar Chromium. El backend Rust maneja las operaciones nativas.

## Stack

- **Tauri 2** — framework desktop
- **Rust** — backend nativo (commands, filesystem, OS integration)
- **React 19 + TypeScript** — frontend (en WebView)
- **Vite** — bundler del frontend
- **Tailwind CSS v4** — styling
- **Zustand** — client state
- **TanStack Query** — server/async state
- **@tauri-apps/api** — bindings TypeScript para las APIs de Rust

## Structure

```
src/                  # Frontend React
  components/
  pages/
  hooks/
    useTauri.ts       # Wrapper para invoke() calls
  store/
  lib/
    tauri.ts          # Typed wrappers para tauri commands
  App.tsx
src-tauri/            # Backend Rust
  src/
    commands/         # Tauri commands (@tauri_command)
      fs.rs
      system.rs
    lib.rs            # Command registration
    main.rs
  tauri.conf.json     # Config: ventana, permisos, bundle
  Cargo.toml
```

## Decisions

- Commands de Tauri como bridge entre frontend y backend — no llamadas directas a APIs del SO desde JS.
- Typed wrappers en `lib/tauri.ts` sobre `invoke()` — el frontend tiene types del backend.
- Sistema de permisos de Tauri 2 en `tauri.conf.json` — allowlist explícita de capacidades.
- El estado de la app vive en el frontend; Rust solo ejecuta operaciones nativas.
- `tauri-plugin-store` para persistencia de configuración local.
