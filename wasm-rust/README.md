# wasm-rust

Rust + WebAssembly — módulo WASM para el browser

## Idea

Compila Rust a WebAssembly para ejecutar código de alto rendimiento en el browser. Ideal para procesamiento de imágenes, criptografía, parsers, simulaciones físicas, o cualquier tarea CPU-intensive que JavaScript no puede manejar eficientemente.

## Stack

- **Rust** — lenguaje (edition 2021)
- **wasm-pack** — toolchain para compilar Rust a WASM + bindings JS
- **wasm-bindgen** — bridge entre Rust y JavaScript
- **web-sys** — bindings a APIs del browser (DOM, Canvas, WebGL, fetch)
- **js-sys** — bindings a objetos JavaScript nativos
- **Vite + vite-plugin-wasm** — integración del módulo WASM en un proyecto web

## Structure

```
src/
  lib.rs              # Exports principales con #[wasm_bindgen]
  core/               # Lógica Rust pura (sin dependencias WASM)
    processor.rs
    math.rs
  bindings/           # Wrappers #[wasm_bindgen] sobre la lógica core
    mod.rs
Cargo.toml
web/                  # Frontend que consume el módulo WASM
  src/
    main.ts
    worker.ts         # Web Worker para ejecutar WASM sin bloquear el UI
  index.html
  vite.config.ts
pkg/                  # Output de wasm-pack (gitignored)
```

## Decisions

- Lógica core en Rust puro sin `#[wasm_bindgen]` — testeable con `cargo test` normal.
- Bindings son wrappers delgados sobre el core — separación de responsabilidades.
- Ejecutar WASM en un Web Worker — no bloquea el hilo principal del browser.
- `wasm-pack build --target web` para uso con bundlers modernos (Vite, webpack).
- Transferir datos con TypedArrays (`Uint8Array`, `Float32Array`) — sin copias innecesarias.
- `console_error_panic_hook` en dev — los panics de Rust aparecen en la consola del browser.
