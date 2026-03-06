# gradio

Python + Gradio — demo de modelo ML / AI

## Idea

La forma más rápida de crear demos interactivas para modelos de ML y AI. Interfaces web con inputs/outputs configurables en pocas líneas. Se puede compartir con un link público via Gradio Share o desplegar en Hugging Face Spaces.

## Stack

- **Python 3.12+** — lenguaje
- **Gradio 5** — framework de demos ML
- **uv** — package manager
- **PyTorch / transformers / scikit-learn** — según el modelo
- **Hugging Face Hub** — para descargar modelos y desplegar en Spaces

## Structure

```
app/
  app.py              # Entry point: gr.Interface o gr.Blocks
  inference/
    model.py          # Carga del modelo y función de predicción
    pipeline.py       # Pipeline de preprocesamiento
  components/         # Bloques de UI reutilizables (con gr.Blocks)
    input_panel.py
    output_panel.py
  utils/
    preprocessing.py
models/               # Modelos locales (gitignored si son grandes)
examples/             # Inputs de ejemplo para la interfaz
.env                  # HF_TOKEN, etc.
pyproject.toml
README.md             # Metadatos para Hugging Face Spaces (con front matter YAML)
```

## Decisions

- `gr.Interface` para demos simples (una función, inputs/outputs directos).
- `gr.Blocks` para layouts complejos con múltiples componentes y lógica.
- Modelos cargados una sola vez fuera de la función de inferencia — sin recarga por request.
- `gr.Examples` para mostrar casos de uso y facilitar la exploración.
- `share=True` en `demo.launch()` para link público temporal (Gradio Share).
- Para producción: desplegar en Hugging Face Spaces con el `README.md` correcto.
