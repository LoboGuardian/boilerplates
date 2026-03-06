# gnome-app

GTK4 + libadwaita — GNOME app completa con estructura de proyecto GNOME Builder

## Idea

Proyecto GNOME completo listo para publicar en Flathub. Incluye el Flatpak manifest, integración con GNOME Builder, metadatos para GNOME Software, y todas las convenciones del ecosistema GNOME.

## Stack

- **Python / Rust / Vala / C** — elige el lenguaje (ver templates específicos)
- **GTK4** — toolkit
- **libadwaita** — widgets GNOME HIG
- **Meson** — build system
- **Flatpak** — empaquetado y distribución
- **GNOME Builder** — IDE recomendado

## Structure

```
src/                            # Código fuente de la app
data/
  icons/
    hicolor/
      scalable/apps/
        org.example.App.svg     # Icono principal
      symbolic/apps/
        org.example.App-symbolic.svg
  org.example.App.desktop       # Entrada en el lanzador
  org.example.App.metainfo.xml  # Metadatos para GNOME Software / Flathub
  org.example.App.gschema.xml   # GSettings schema
po/                             # Sistema de traducción (gettext)
  LINGUAS                       # Lista de idiomas soportados
flatpak/
  org.example.App.json          # Flatpak manifest
tests/
meson.build
meson_options.txt
README.md
CONTRIBUTING.md
```

## Decisions

- ID en formato DNS reverso: `org.example.AppName` — consistente en todos los archivos.
- Flatpak como formato de distribución: sandbox, actualizaciones, sin dependencias del sistema.
- `org.example.App.metainfo.xml` con screenshots y descripción — requerido por Flathub.
- Soporte de traducción con gettext desde el inicio — no es fácil agregar después.
- CI con GNOME CI templates en GitLab — build, test, y lint automáticos.
