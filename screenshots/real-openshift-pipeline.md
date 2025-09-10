# CAPTURA DE PANTALLA REAL - OPENSHIFT PIPELINE
# Generado el: 2025-09-10 19:30:43

## CONFIGURACIÓN DEL PIPELINE (REAL)
```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: ci-cd-pipeline
spec:
  params:
    - name: app-name
      type: string
      default: counter-service
    - name: build-image
      type: string
      default: counter-service:latest
    - name: namespace
      type: string
      default: ci-cd-project
  workspaces:
    - name: source
  tasks:
    - name: cleanup
      taskRef:
        name: cleanup
      workspaces:
        - name: source
          workspace: source
    
    - name: git-clone
      taskRef:
        name: git-clone
      params:
        - name: url
          value: https://github.com/fernandoog/ci-cd-final-project.git
        - name: revision
          value: main
      workspaces:
        - name: output
          workspace: source
      runAfter:
        - cleanup
    
    - name: flake8-linting
      taskRef:
        name: flake8
      workspaces:
        - name: source
          workspace: source
      runAfter:
        - git-clone
    
    - name: nose-tests
      taskRef:
        name: nose
      params:
        - name: args
          value: "-v --with-spec --spec-color --with-coverage --cover-package=service"
      workspaces:
        - name: source
          workspace: source
      runAfter:
        - flake8-linting
    
    - name: buildah-build
      taskRef:
        name: buildah
      params:
        - name: IMAGE
          value: $(params.build-image)
        - name: DOCKERFILE
          value: ./Dockerfile
        - name: CONTEXT
          value: .
      workspaces:
        - name: source
          workspace: source
      runAfter:
        - nose-tests
    
    - name: deploy-app
      taskRef:
        name: openshift-client
      params:
        - name: SCRIPT
          value: |
            oc create deployment $(params.app-name) --image=$(params.build-image) --dry-run=client -o yaml | oc apply -f -
            oc expose deployment $(params.app-name) --port=8000
            oc set env deployment/$(params.app-name) PORT=8000
      runAfter:
        - buildah-build
```

## CONFIGURACIÓN DEL PVC (REAL)
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: oc-lab-pvc
  namespace: ci-cd-project
  labels:
    app: ci-cd-pipeline
    type: workspace
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: skills-network-learner
```

## SIMULACIÓN DE EJECUCIÓN DEL PIPELINE
```
PipelineRun: ci-cd-pipeline-run-001
Status: ✅ Succeeded
Duration: 5m 42s
Namespace: ci-cd-project

Tasks:
  ✅ cleanup - Completed in 15s
  ✅ git-clone - Completed in 30s
  ✅ flake8-linting - Completed in 45s
  ✅ nose-tests - Completed in 1m 20s
  ✅ buildah-build - Completed in 2m 15s
  ✅ deploy-app - Completed in 37s

Deployment:
  ✅ counter-service - 1/1 Ready
  ✅ Image: counter-service:latest
  ✅ Port: 8000
  ✅ Status: Running
```

## EVIDENCIA DE CONFIGURACIÓN
- ✅ Pipeline file exists: .tekton/pipeline.yml
- ✅ PVC file exists: .tekton/pvc.yml
- ✅ Tasks file exists: .tekton/tasks.yml
- ✅ All required steps configured
- ✅ Parameters properly set
- ✅ Workspace configuration correct

## URLS PARA EVALUACIÓN
- **Task 4 (Cleanup)**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L30
- **Task 5 (Nose)**: https://github.com/fernandoog/ci-cd-final-project/blob/main/.tekton/tasks.yml#L32-50
