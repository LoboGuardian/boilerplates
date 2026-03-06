# gtk4-python

Python + GTK4 + libadwaita — GNOME app moderna

## Idea

App de escritorio nativa para GNOME usando GTK4 y libadwaita. Libadwaita provee los widgets y estilos de diseño de GNOME HIG (Human Interface Guidelines). Python con PyGObject es el binding oficial y el más productivo.

## Stack

- **Python 3.12+** — lenguaje
- **GTK4** — toolkit gráfico
- **libadwaita 1** — widgets GNOME modernos (AdwWindow, AdwHeaderBar, etc.)
- **PyGObject** — bindings Python para GTK/GLib/Gio
- **Meson + Ninja** — build system (estándar en el ecosistema GNOME)
- **Blueprint** — lenguaje de UI para archivos `.blp` (compilados a XML)
- **pytest** — testing

## Structure

```
src/
  app_name/
    __init__.py
    main.py           # GApplication entry point
    window.py         # Ventana principal (AdwApplicationWindow)
    widgets/          # Widgets personalizados
    data/
      app_name.gresource.xml  # Bundle de resources
      ui/             # Archivos .blp (Blueprint UI files)
        window.blp
      icons/
data/
  app.name.appdata.xml    # Metadatos para GNOME Software
  app.name.desktop        # .desktop file para lanzador
  app.name.gschema.xml    # GSettings schema
meson.build
pyproject.toml
```

## Decisions

- `GApplication` como base — maneja instancia única, DBus, activación.
- Blueprint para UI: sintaxis legible en vez de XML puro.
- GSettings para persistir preferencias — integrado con dconf.
- GResources para empaquetar assets (iconos, UI files) en el binario.
- Meson porque es el build system de GNOME — integración con `gnome.compile_resources()`.
