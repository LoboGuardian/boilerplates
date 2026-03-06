# gtk4-vala

Vala + GTK4 + libadwaita — GNOME app con sintaxis moderna

## Idea

Vala es el lenguaje propio de GNOME: sintaxis similar a C# pero compila a C y luego a código nativo. Elimina el boilerplate de GObject en C manteniendo el rendimiento. Muchas apps GNOME están escritas en Vala (Gedit, Shotwell, GNOME Files).

## Stack

- **Vala** — lenguaje compilado a C (parte del proyecto GNOME)
- **GTK4** — toolkit gráfico
- **libadwaita** — widgets GNOME HIG
- **GLib / GIO** — tipos y async
- **Meson + Ninja** — build system
- **Blueprint** — UI files `.blp`

## Structure

```
src/
  Application.vala          # GApplication subclass
  MainWindow.vala           # AdwApplicationWindow subclass
  widgets/                  # Widgets personalizados
data/
  ui/
    MainWindow.blp
  org.example.AppName.gresource.xml
  org.example.AppName.desktop
  org.example.AppName.metainfo.xml
  org.example.AppName.gschema.xml
tests/
meson.build
meson_options.txt
```

## Decisions

- Clases Vala mapean 1:1 a GObject — el compilador genera el boilerplate C automáticamente.
- `async/await` en Vala para operaciones IO sin bloquear el UI thread.
- Properties de GObject con `{ get; set; }` — integradas con GSettings y bindings.
- Blueprint para UI: Vala + Blueprint es el stack moderno recomendado por GNOME.
- GNOME Builder es el IDE recomendado — soporte nativo para Vala + Meson + Blueprint.
