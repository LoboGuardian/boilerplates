# gnome-extension

GNOME Shell Extension — JavaScript + GJS

## Idea

Extensión para personalizar y extender GNOME Shell. Las extensiones se escriben en JavaScript con GJS (GNOME JavaScript). Pueden agregar indicadores al panel, modificar el comportamiento del escritorio, añadir funcionalidad al menú de sistema.

## Stack

- **GJS** — JavaScript runtime de GNOME (SpiderMonkey + GObject introspection)
- **JavaScript (ES6+)** — lenguaje
- **GNOME Shell API** — APIs de extensión (St, Shell, Clutter, Gio)
- **GNOME Extensions Tool** — CLI para desarrollo y testing

## Structure

```
extension.js          # Entry point (init, enable, disable exports)
prefs.js              # Preferencias de la extensión (UI de configuración)
metadata.json         # Nombre, UUID, versiones de GNOME compatibles
stylesheet.css        # Estilos para widgets de la extensión
schemas/
  org.gnome.shell.extensions.myext.gschema.xml  # GSettings schema
po/                   # Traducciones
icons/                # Iconos de la extensión
Makefile              # install, package, lint
```

## metadata.json

```json
{
  "name": "My Extension",
  "uuid": "my-extension@username.github.com",
  "description": "...",
  "shell-version": ["45", "46", "47"],
  "version": 1
}
```

## Decisions

- UUID en formato `name@domain` — debe ser único en extensions.gnome.org.
- Limpiar todo en `disable()` — signals desconectadas, timeouts cancelados, widgets destruidos.
- GSettings para persistir configuración — accesible desde `extension.js` y `prefs.js`.
- `Main.panel` para agregar indicadores al panel superior.
- Probar con `gnome-extensions enable <uuid>` y `journalctl -f -o cat /usr/bin/gnome-shell` para logs.
