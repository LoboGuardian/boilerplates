# fltk

C++ + FLTK — GUI ultraligera

## Idea

Fast Light Toolkit — el framework de UI más ligero para C++. Binarios de menos de 1MB, sin dependencias externas, arranca instantáneamente. Ideal para herramientas de sistema, apps embebidas, o cuando el tamaño y la velocidad de arranque son críticos.

## Stack

- **C++17** — lenguaje
- **FLTK 1.4** — toolkit gráfico ultraligero
- **CMake** — build system
- **FLUID** — diseñador visual de UI de FLTK (genera código C++)

## Structure

```
src/
  main.cpp            # Entry point: Fl::run()
  MainWindow.h
  MainWindow.cpp      # Fl_Window o Fl_Double_Window subclass
  widgets/            # Custom widgets (Fl_Widget subclasses)
  logic/              # Lógica de negocio sin dependencia de FLTK
ui/
  main.fl             # Archivo de FLUID (diseñador visual)
  main.cxx            # Código C++ generado por FLUID
  main.h
CMakeLists.txt
```

## Decisions

- FLTK dibuja sus propios widgets — no usa controles nativos del SO (similar a Qt en este aspecto).
- FLUID para diseñar la UI visualmente — genera `.cxx` y `.h` que se incluyen en el proyecto.
- Callbacks con punteros a función o lambdas: `btn->callback([](Fl_Widget* w, void* data){...}, this)`.
- Un solo thread para la UI — operaciones largas en threads separados con `Fl::lock()` / `Fl::unlock()`.
- Sin dependencias de sistema en Linux salvo X11/Wayland — binario portable.
- Ideal para distribución: binario estático de ~500KB-1MB.
