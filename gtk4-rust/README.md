# gtk4-rust

Rust + GTK4 + libadwaita — GNOME app con máximo rendimiento

## Idea

Apps GNOME en Rust usando gtk4-rs. Combina la seguridad de memoria de Rust con los widgets nativos de GTK4. Ideal para herramientas de sistema, apps con operaciones intensivas, o cuando Python no es suficientemente rápido.

## Stack

- **Rust** — lenguaje (edition 2021)
- **gtk4-rs** — bindings GTK4 para Rust
- **libadwaita-rs** — bindings libadwaita para Rust
- **glib-rs** — bindings GLib (tipos base, signals, properties)
- **Meson + Ninja** — build system
- **Blueprint** — UI files `.blp`
- **cargo-test** — testing

## Structure

```
src/
  application.rs    # GApplication subclass
  window/
    mod.rs          # AdwApplicationWindow subclass
    imp.rs          # Implementación interna (GObject boilerplate)
  widgets/          # Custom widget subclasses
    widget_name/
      mod.rs
      imp.rs
  main.rs           # Entry point
data/
  ui/               # Blueprint UI files
    window.blp
  resources.gresource.xml
  app.name.desktop
  app.name.appdata.xml
  app.name.gschema.xml
build.rs            # Compila resources GNOME
Cargo.toml
meson.build
```

## Decisions

- Pattern `mod.rs` + `imp.rs` para cada GObject subclass — la separación es idiomática en gtk4-rs.
- GObject subclassing con `#[derive(CompositeTemplate)]` para conectar UI files a structs Rust.
- `build.rs` compila los GResources en tiempo de compilación.
- GSettings wrapeado en un servicio para preferencias persistentes.
- Operaciones bloqueantes en threads separados con `gio::spawn_blocking` o Tokio.
