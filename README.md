# Calculator App - Monorepo DevOps

Monorepo del proyecto API Calculadora, estructurado siguiendo la Guia de Integracion y Despliegue DevOps para soportar CI/CD, contenedorizacion y despliegue en AWS EKS.

## Estructura del proyecto

```
calculator-app/
├── backend/                  # API REST (FastAPI + Python 3.12)
│   ├── main.py               # Aplicacion con prefijo /api
│   ├── requirements.txt      # Deps con versiones pinneadas
│   ├── Dockerfile            # Non-root, cache optimizado
│   ├── .dockerignore
│   ├── .env.example
│   └── README.md
├── frontend/                 # UI (HTML/CSS/JS + Nginx)
│   ├── index.html
│   ├── app.js                # URL base relativa (/api)
│   ├── app.css
│   ├── nginx.conf.template   # Proxy /api → backend
│   ├── Dockerfile
│   └── .dockerignore
├── .github/
│   ├── workflows/            # CI/CD pipelines
│   └── CODEOWNERS
├── docker-compose.yml        # Desarrollo local (front + back)
└── .gitignore
```

## Inicio rapido

```bash
# Levantar todo en local
docker compose up --build

# Acceder
# Frontend: http://localhost
# API docs: http://localhost/api/docs
# Health:   http://localhost/api/health
```

## Endpoints del backend

| Metodo | Ruta                | Descripcion                  |
|--------|---------------------|------------------------------|
| GET    | `/api/health`       | Health check                 |
| GET    | `/api/sumar`        | Suma `?a=2&b=3`             |
| GET    | `/api/restar`       | Resta `?a=10&b=4`           |
| POST   | `/api/multiplicar`  | `{"a": 3, "b": 4}`          |
| POST   | `/api/dividir`      | `{"a": 10, "b": 2}`         |

## Despliegue en Kubernetes

```bash
# Dev
kubectl apply -k k8s/overlays/dev

# Staging
kubectl apply -k k8s/overlays/staging

# Prod
kubectl apply -k k8s/overlays/prod
```

## Equipo y CODEOWNERS

- **Global:** @jluisquf
- **Backend:** @eeloc37, @Bxtto
- **Frontend:** @mau-m
- **Infraestructura:** @MMCJUAREZ, @hernandev96

