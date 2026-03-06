# gtk3-python

Python + GTK3 — compatible con XFCE, MATE, LXDE, Cinnamon

## Idea

Apps GTK3 para entornos de escritorio que no han migrado a GTK4: XFCE, MATE, LXDE, Cinnamon. También útil cuando las dependencias del sistema son más antiguas (Ubuntu LTS, Debian Stable).

## Stack

- **Python 3.10+** — lenguaje
- **GTK3** — toolkit gráfico (ampliamente disponible en distros)
- **PyGObject** — bindings Python para GTK3
- **Glade** — diseñador de UI visual (genera XML .glade / .ui)
- **GLib / GIO** — tipos base y async
- **Autotools o Meson** — build system

## Structure

```
src/
  app_name/
    __init__.py
    main.py           # Gtk.Application entry point
    window.py         # Gtk.ApplicationWindow principal
    widgets/          # Widgets personalizados
data/
  ui/
    window.ui         # Glade/XML UI file
  icons/
  app.name.desktop
  app.name.gschema.xml
po/                   # Traducciones (gettext)
meson.build
```

## Decisions

- `Gtk.Application` como base — maneja instancia única y ciclo de vida.
- Archivos `.ui` XML cargados con `Gtk.Builder` — UI separada del código.
- GSettings para preferencias persistentes.
- `GObject.GObject` subclassing donde se necesiten signals personalizadas.
- Compatible con Python 3.6+ para mayor soporte en distros LTS.
- Sin dependencia de libadwaita — usa GTK3 puro para máxima compatibilidad.
