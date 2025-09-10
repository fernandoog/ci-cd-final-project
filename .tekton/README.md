# OpenShift Pipeline Configuration

Este directorio contiene la configuración completa para el pipeline de CI/CD en OpenShift.

## Archivos de Configuración

### 1. `tasks.yml`
Contiene las tareas de Tekton:
- **cleanup**: Limpia el workspace
- **nose**: Ejecuta tests con nose

### 2. `pipeline.yml`
Define el pipeline completo con los siguientes pasos:
1. cleanup
2. git-clone
3. flake8-linting
4. nose-tests
5. buildah-build
6. deploy-app

### 3. `pvc.yml`
Configuración del Persistent Volume Claim para el workspace.

## Instrucciones de Despliegue

### Paso 1: Crear el Namespace
```bash
oc create namespace ci-cd-project
```

### Paso 2: Crear el PVC
```bash
oc apply -f .tekton/pvc.yml
```

### Paso 3: Instalar las Tareas
```bash
oc apply -f .tekton/tasks.yml
```

### Paso 4: Crear el Pipeline
```bash
oc apply -f .tekton/pipeline.yml
```

### Paso 5: Ejecutar el Pipeline
```bash
oc create -f - <<EOF
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: ci-cd-pipeline-run-001
spec:
  pipelineRef:
    name: ci-cd-pipeline
  params:
    - name: app-name
      value: counter-service
    - name: build-image
      value: counter-service:latest
    - name: namespace
      value: ci-cd-project
  workspaces:
    - name: source
      persistentVolumeClaim:
        claimName: oc-lab-pvc
EOF
```

### Paso 6: Monitorear el Pipeline
```bash
# Ver el estado del pipeline
oc get pipelinerun ci-cd-pipeline-run-001

# Ver los logs
oc logs -f pipelinerun/ci-cd-pipeline-run-001

# Ver los pods
oc get pods
```

### Paso 7: Verificar la Aplicación
```bash
# Ver el deployment
oc get deployment counter-service

# Ver el servicio
oc get service counter-service

# Obtener la URL de la aplicación
oc get route counter-service
```

## Parámetros del Pipeline

- **app-name**: Nombre de la aplicación (default: counter-service)
- **build-image**: Imagen Docker a construir (default: counter-service:latest)
- **namespace**: Namespace de OpenShift (default: ci-cd-project)

## Workspace

El pipeline utiliza un PVC llamado `oc-lab-pvc` con:
- Storage Class: `skills-network-learner`
- Tamaño: 1Gi
- Access Mode: ReadWriteOnce

## Tareas Requeridas

El pipeline asume que las siguientes tareas están disponibles en el cluster:
- `git-clone` (tarea estándar de Tekton)
- `flake8` (tarea personalizada para linting)
- `buildah` (tarea estándar de Tekton)
- `openshift-client` (tarea estándar de Tekton)

## Troubleshooting

### Verificar el estado del PVC
```bash
oc describe pvc oc-lab-pvc
```

### Ver logs de tareas específicas
```bash
oc logs -f taskrun/<task-run-name>
```

### Verificar recursos creados
```bash
oc get all -l app=counter-service
```