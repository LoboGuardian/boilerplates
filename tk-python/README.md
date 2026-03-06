# tk-python

Python + Tkinter — GUI sin dependencias externas

## Idea

Tkinter está incluido en Python — cero dependencias adicionales, funciona en Windows, macOS y Linux sin instalar nada. Ideal para herramientas internas, scripts con interfaz gráfica, o cuando el entorno no permite instalar paquetes externos.

## Stack

- **Python 3.12+** — lenguaje
- **Tkinter** — binding de Tk incluido en Python stdlib
- **customtkinter** — widgets modernos sobre Tkinter (opcional, requiere pip)
- **Pillow** — para mostrar imágenes (PNG, JPG en Tkinter)
- **uv** — package manager (solo si se usan dependencias opcionales)

## Structure

```
src/
  main.py             # Entry point: Tk() root window
  app.py              # Clase App principal (Tk o CTk)
  views/              # Frames/ventanas como clases
    main_view.py
    settings_view.py
  widgets/            # Custom widgets reutilizables
  controllers/        # Lógica que conecta views con models
  models/             # Lógica de negocio (sin Tkinter)
  utils/
    config.py         # Leer/escribir configuración (configparser)
```

## Decisions

- Clases que heredan de `tk.Frame` o `tk.Tk` como unidades de UI.
- MVC simple: Views muestran datos, Controllers manejan eventos, Models procesan datos.
- `customtkinter` para una apariencia más moderna si se puede instalar — misma API que Tkinter.
- `configparser` para persistir configuración en un archivo `.ini` — sin dependencias externas.
- `tk.StringVar`, `tk.IntVar` para binding bidireccional entre widgets y datos.
- Sin Tkinter en el hilo de background — toda la UI en el hilo principal, lógica pesada en `threading.Thread`.
