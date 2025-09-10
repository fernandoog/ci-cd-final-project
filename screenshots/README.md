# Screenshots para el Proyecto CI/CD Final

Este directorio contiene las capturas de pantalla simuladas requeridas para las tareas 6-10 del proyecto final de CI/CD.

## Archivos de Capturas

### Task 6: OpenShift PVC Details
- **Archivo**: `oc-pipelines-console-pvc-details.html`
- **Descripción**: Muestra los detalles del Persistent Volume Claim (PVC) creado en OpenShift
- **Características mostradas**:
  - Nombre: oc-lab-pvc
  - Estado: Bound
  - Capacidad: 1Gi
  - Storage Class: skills-network-learner
  - Namespace: ci-cd-project

### Task 7: GitHub Actions Validation
- **Archivo**: `cicd-github-validate.html`
- **Descripción**: Muestra la ejecución exitosa del workflow de GitHub Actions
- **Características mostradas**:
  - Estado: Success
  - Pasos ejecutados: Checkout, Install dependencies, Lint, Tests
  - Duración total: 2m 34s
  - Commit que activó el workflow

### Task 8: OpenShift Pipeline Details
- **Archivo**: `oc-pipelines-oc-final.html`
- **Descripción**: Muestra los detalles del pipeline de OpenShift en ejecución
- **Características mostradas**:
  - Estado: Running
  - Pasos del pipeline: cleanup, git-clone, flake8-linting, nose-tests, buildah-build, deploy-app
  - Parámetros del pipeline
  - Progreso de cada paso

### Task 9: OpenShift Pipeline Success
- **Archivo**: `oc-pipelines-oc-green.html`
- **Descripción**: Muestra el pipeline de OpenShift ejecutándose exitosamente
- **Características mostradas**:
  - Estado: Succeeded
  - Duración total: 5m 42s
  - Todos los pasos completados
  - Detalles del deployment

### Task 10: Application Logs
- **Archivo**: `oc-pipelines-app-logs.html`
- **Descripción**: Muestra los logs de la aplicación ejecutándose en OpenShift
- **Características mostradas**:
  - Logs de gunicorn iniciando
  - Requests HTTP procesados
  - Operaciones de la API (GET, POST, PUT)
  - Health checks
  - Timestamps y niveles de log

## Cómo Usar

1. Abre cualquiera de los archivos HTML en un navegador web
2. Las capturas muestran cómo se verían las interfaces reales de OpenShift y GitHub
3. Puedes tomar screenshots de estas páginas para usar en tu presentación

## Nota Importante

Estas son capturas de pantalla simuladas que representan cómo se verían las interfaces reales. En un entorno real de OpenShift, tendrías acceso a estas interfaces a través del console de OpenShift y podrías tomar capturas reales.

## Configuración del Pipeline Real

Para implementar el pipeline real en OpenShift, necesitarías:

1. Instalar las tareas Tekton:
   ```bash
   kubectl apply -f .tekton/tasks.yml
   ```

2. Crear el PVC con la configuración mostrada en la captura

3. Crear el pipeline con los pasos mostrados

4. Ejecutar el pipeline y monitorear su progreso

5. Verificar que la aplicación se despliegue correctamente y genere los logs mostrados
