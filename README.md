# CI/CD Final Project

Este proyecto implementa un pipeline completo de CI/CD para una aplicación Flask de contadores.

## Estructura del Proyecto

```
├── .github/workflows/workflow.yml    # GitHub Actions CI Pipeline
├── .tekton/                          # OpenShift CD Pipeline
│   ├── tasks.yml                     # Tekton Tasks
│   ├── pipeline.yml                  # OpenShift Pipeline
│   └── pvc.yml                       # Persistent Volume Claim
├── service/                          # Aplicación Flask
│   ├── __init__.py
│   ├── routes.py                     # API Endpoints
│   └── common/                       # Utilidades comunes
├── tests/                            # Tests unitarios
│   └── test_routes.py
├── screenshots/                      # Capturas de pantalla (Tareas 6-10)
│   ├── cicd-github-validate.jpg
│   ├── oc-pipelines-console-pvc-details.jpg
│   ├── oc-pipelines-oc-final.jpg
│   ├── oc-pipelines-oc-green.jpg
│   └── oc-pipelines-app-logs.jpg
├── requirements.txt                  # Dependencias Python
├── Dockerfile                        # Imagen Docker
└── README.md
```

## URLs para Evaluación

### Task 1: GitHub Repository
- **URL**: https://github.com/fernandoog/ci-cd-final-project.git

### Task 2: GitHub Actions Linting Step
- **URL**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L29-L32

### Task 3: GitHub Actions Test Step
- **URL**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L34-L36

### Task 4: Tekton Cleanup Task
- **URL**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L30

### Task 5: Tekton Nose Test Task
- **URL**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.tekton/tasks.yml#L32-50

### Tasks 6-10: Screenshots
- **Ubicación**: Directorio `screenshots/`
- **Formato**: Archivos JPG de alta calidad
- **Contenido**: Capturas de pantalla reales de OpenShift y GitHub Actions

## Pipeline CI/CD

### GitHub Actions (CI)
- **Trigger**: Push y Pull Request en main
- **Container**: python:3.9-slim
- **Steps**: checkout, install, lint, test

### OpenShift Pipeline (CD)
- **Steps**: cleanup, git-clone, flake8, nose, buildah, deploy
- **Workspace**: PVC con storage class `skills-network-learner`
- **Deployment**: Aplicación Flask en OpenShift

## Aplicación

La aplicación es una API REST de contadores con los siguientes endpoints:
- `GET /` - Información del servicio
- `GET /health` - Health check
- `GET /counters` - Listar contadores
- `POST /counters/<name>` - Crear contador
- `GET /counters/<name>` - Leer contador
- `PUT /counters/<name>` - Actualizar contador
- `DELETE /counters/<name>` - Eliminar contador

## Instalación y Uso

```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar tests
python -m unittest tests.test_routes -v

# Ejecutar aplicación
python -m flask run
```

## Autor

Proyecto final del curso CI/CD Tools and Practices