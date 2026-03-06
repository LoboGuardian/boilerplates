# fastapi-ml

Python + FastAPI + Model Serving — API de inferencia ML

## Idea

API REST para servir modelos de ML en producción. FastAPI maneja las requests async, los modelos se cargan al iniciar el servidor, y las predicciones se ejecutan en background si son lentas. Preparado para escalar con múltiples workers.

## Stack

- **FastAPI** — API framework async
- **uv** — package manager
- **PyTorch / scikit-learn / transformers** — según el modelo
- **Pydantic** — validación de inputs/outputs del modelo
- **Celery + Redis** — tareas async para inferencia lenta (opcional)
- **Prometheus + prometheus-fastapi-instrumentator** — métricas
- **Docker** — contenedor para deployment
- **Ruff** — linting y formatting

## Structure

```
app/
  main.py             # FastAPI app, lifespan para cargar modelos
  api/
    v1/
      predict.py      # Endpoint de predicción
      health.py       # Health check
  models/
    loader.py         # Carga y cacheo de modelos al startup
    schemas.py        # Pydantic schemas (PredictionRequest, PredictionResponse)
  inference/
    pipeline.py       # Preprocesamiento + modelo + postprocesamiento
    model_name.py     # Lógica específica del modelo
  core/
    config.py         # Settings (model path, device, batch size)
    metrics.py        # Setup de Prometheus
artifacts/            # Modelos serializados (.pt, .pkl, .onnx) — gitignored
Dockerfile
pyproject.toml
.env.example
```

## Decisions

- Modelos cargados en el `lifespan` de FastAPI — disponibles en `app.state.model`.
- `asyncio.get_event_loop().run_in_executor()` para inferencia CPU-bound — sin bloquear el event loop.
- ONNX Runtime sobre PyTorch en producción cuando es posible — 2-5x más rápido en CPU.
- Pydantic valida inputs del modelo — requests inválidas fallan antes de llegar al modelo.
- `/health` endpoint con estado del modelo cargado — para readiness probe en Kubernetes.
- Batching: agrupar requests concurrentes en un solo forward pass si el modelo lo soporta.
