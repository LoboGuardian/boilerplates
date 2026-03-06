# streamlit

Python + Streamlit — data app interactiva

## Idea

Convierte scripts Python en web apps interactivas sin escribir HTML, CSS ni JavaScript. Ideal para dashboards de datos, demos de modelos ML, herramientas internas de análisis, y prototipos rápidos para científicos de datos.

## Stack

- **Python 3.12+** — lenguaje
- **Streamlit** — framework de data apps
- **uv** — package manager
- **pandas / polars** — manipulación de datos
- **plotly / altair** — visualizaciones interactivas
- **scikit-learn** — ML (si aplica)
- **SQLAlchemy** — acceso a BD (con `st.cache_resource`)

## Structure

```
app/
  main.py             # Entry point: st.title, layout principal
  pages/              # Multi-page app (Streamlit filesystem routing)
    01_dashboard.py
    02_analysis.py
    03_model.py
  components/         # Funciones que renderizan secciones de UI
    charts.py
    filters.py
    metrics.py
  data/
    loaders.py        # Funciones @st.cache_data para cargar datos
    processors.py     # Transformaciones de datos
  models/             # Carga y predicción de modelos ML
    predictor.py
.streamlit/
  config.toml         # Tema, puerto, opciones del servidor
  secrets.toml        # Secrets locales (no commitear)
pyproject.toml
```

## Decisions

- `@st.cache_data` para resultados de queries y procesamiento — solo se ejecutan cuando cambian los inputs.
- `@st.cache_resource` para conexiones a BD y modelos cargados — singleton por sesión.
- Multi-page apps con la carpeta `pages/` — Streamlit la detecta automáticamente.
- `st.session_state` para estado persistente entre rerenders.
- Secrets en `.streamlit/secrets.toml` — accesibles via `st.secrets["key"]`.
- `st.sidebar` para filtros globales que afectan toda la página.
