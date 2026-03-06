# xfce-plugin

C + GTK3 + libxfce4ui — plugin para el panel de XFCE

## Idea

Plugin para el panel de XFCE4. Los plugins aparecen en la barra de tareas de XFCE y pueden mostrar información, controles, o menús. Escritos en C usando la API de XFCE y GTK3.

## Stack

- **C (C11)** — lenguaje
- **GTK3** — toolkit (XFCE usa GTK3)
- **libxfce4panel** — API para plugins del panel
- **libxfce4ui** — widgets y diálogos de XFCE
- **libxfconf** — sistema de configuración de XFCE (Xfconf)
- **Autotools o CMake** — build system

## Structure

```
panel-plugin/
  plugin-name.c         # Plugin principal (XfcePanelPlugin)
  plugin-name.h
  plugin-name-dialogs.c # Diálogo de configuración
  plugin-name-dialogs.h
  plugin-name.desktop.in # Metadata del plugin
m4/                     # Macros de Autotools
configure.ac            # Script de configuración
Makefile.am
```

## plugin-name.c (estructura básica)

```c
// Registrar el plugin con XFCE
XFCE_PANEL_PLUGIN_REGISTER(plugin_construct);

static void plugin_construct(XfcePanelPlugin *plugin) {
    // Crear widgets, conectar señales
    // Registrar callbacks del panel (orientación, tamaño, etc.)
}
```

## Decisions

- Un `.c/.h` por componente: plugin principal, diálogos, configuración.
- Xfconf para persistir configuración — `xfconf_channel_new(PLUGIN_NAME)`.
- El plugin debe responder a cambios de orientación del panel (horizontal/vertical).
- `xfce_panel_plugin_menu_insert_item()` para agregar opciones al menú contextual.
- Instalación en `$(libdir)/xfce4/panel/plugins/` y el `.desktop` en `$(datadir)/xfce4/panel/plugins/`.
