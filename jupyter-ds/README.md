# jupyter-ds

Jupyter + Python — análisis de datos y ciencia de datos

## Idea

Entorno de análisis de datos reproducible. Notebooks para exploración, scripts Python para pipelines reutilizables, y estructura clara para separar datos, análisis y reportes. Gestionado con `uv` para entornos reproducibles.

## Stack

- **Python 3.12+** — lenguaje
- **uv** — package manager y entornos virtuales
- **JupyterLab** — IDE de notebooks
- **pandas** — manipulación de datos tabulares
- **polars** — alternativa rápida a pandas (Rust-based)
- **numpy** — cálculo numérico
- **matplotlib / seaborn** — visualización estática
- **plotly** — visualización interactiva
- **scikit-learn** — ML clásico
- **duckdb** — SQL sobre DataFrames y archivos Parquet

## Structure

```
notebooks/
  01_exploration.ipynb      # EDA inicial
  02_cleaning.ipynb         # Limpieza de datos
  03_analysis.ipynb         # Análisis principal
  04_modeling.ipynb         # Modelado ML
  05_reporting.ipynb        # Notebook limpio para presentar
src/
  data/
    loaders.py              # Funciones para cargar datasets
    cleaners.py             # Transformaciones reproducibles
  features/
    engineering.py          # Feature engineering reutilizable
  models/
    train.py
    evaluate.py
  visualization/
    plots.py                # Funciones de plotting reutilizables
data/
  raw/                      # Datos originales (nunca modificar)
  processed/                # Datos limpios
  external/                 # Datos de fuentes externas
reports/
  figures/                  # Gráficos exportados
pyproject.toml
.env.example                # API keys para fuentes de datos
```

## Decisions

- Datos `raw/` son inmutables — todos los cambios se guardan en `processed/`.
- Notebooks numerados por orden de ejecución — reproducibles de principio a fin.
- Lógica reutilizable en `src/` importada desde los notebooks — no duplicar código.
- DuckDB para queries SQL sobre archivos CSV/Parquet sin levantar una BD.
- `nbstripout` en git hooks — no commitear outputs de notebooks (reducen diff y peso del repo).
