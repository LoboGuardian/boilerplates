# gtk4-c

C + GTK4 — app GNOME tradicional

## Idea

El lenguaje nativo de GTK. Apps escritas en C con GTK4 son lo que usa GNOME internamente (Nautilus, GNOME Terminal, etc.). Máximo control, mínimas dependencias, integración perfecta con el ecosistema GNOME.

## Stack

- **C (C11/C17)** — lenguaje
- **GTK4** — toolkit gráfico
- **libadwaita** — widgets GNOME modernos
- **GLib / GIO** — tipos base, async, filesystem
- **Meson + Ninja** — build system oficial de GNOME
- **Blueprint** — UI files `.blp`
- **GTest** — testing (parte de GLib)

## Structure

```
src/
  main.c
  app-name-application.c    # GApplication subclass
  app-name-application.h
  app-name-window.c         # AdwApplicationWindow subclass
  app-name-window.h
  widgets/                  # Custom GObject widgets
data/
  ui/
    app-name-window.blp     # Blueprint UI file
  org.gnome.AppName.gresource.xml
  org.gnome.AppName.desktop
  org.gnome.AppName.appdata.xml
  org.gnome.AppName.gschema.xml
tests/
meson.build
meson_options.txt
```

## Decisions

- Un par `.c/.h` por clase GObject — convención del proyecto GNOME.
- Naming en snake_case con prefijo del namespace: `app_name_window_new()`.
- GObject type system para herencia y signals — `G_DECLARE_FINAL_TYPE` macro.
- Blueprint para UI: evita XML repetitivo, tiene autocompletado en GNOME Builder.
- `meson.build` usa `gnome.compile_resources()` y `gnome.compile_schemas()`.
