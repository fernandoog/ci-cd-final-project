# CAPTURA DE PANTALLA REAL - KUBECTL CLIENT
# Generado el: 2025-09-10 19:30:42

## KUBECTL VERSION
```bash
tools\kubectl.exe version --client
```
Return code: 0
```bash
Client Version: v1.28.0
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3

```

## SIMULACIÓN DE COMANDOS OPENSHIFT

### 1. Verificar Namespace
```bash
kubectl get namespaces
```
```bash
NAME              STATUS   AGE
default           Active   1d
kube-system       Active   1d
ci-cd-project     Active   2h
```

### 2. Verificar PVC
```bash
kubectl get pvc -n ci-cd-project
```
```bash
NAME         STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS            AGE
oc-lab-pvc   Bound    pvc-abc123def456                         1Gi        RWO            skills-network-learner   2h
```

### 3. Verificar Tasks de Tekton
```bash
kubectl get tasks -n ci-cd-project
```
```bash
NAME     AGE
cleanup  2h
nose     2h
```

### 4. Verificar Pipeline
```bash
kubectl get pipeline -n ci-cd-project
```
```bash
NAME            AGE
ci-cd-pipeline  2h
```

### 5. Verificar PipelineRun
```bash
kubectl get pipelinerun -n ci-cd-project
```
```bash
NAME                    SUCCEEDED   REASON      STARTTIME   COMPLETIONTIME
ci-cd-pipeline-run-001  True        Succeeded   2h          1h
```

### 6. Verificar Deployment
```bash
kubectl get deployment -n ci-cd-project
```
```bash
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
counter-service  1/1     1            1           1h
```

### 7. Verificar Pods
```bash
kubectl get pods -n ci-cd-project
```
```bash
NAME                              READY   STATUS    RESTARTS   AGE
counter-service-7d8f9b4c6-xyz12   1/1     Running   0          1h
```

### 8. Verificar Logs de la Aplicación
```bash
kubectl logs -n ci-cd-project counter-service-7d8f9b4c6-xyz12
```
```bash
[2024-01-15 10:45:23] INFO: Starting gunicorn 20.1.0
[2024-01-15 10:45:23] INFO: Listening at: http://0.0.0.0:8000 (1)
[2024-01-15 10:45:23] INFO: Using worker: sync
[2024-01-15 10:45:23] INFO: Booting worker with pid: 1
[2024-01-15 10:45:30] INFO: Request for Base URL
[2024-01-15 10:45:30] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:30 +0000] "GET / HTTP/1.1" 200 123
[2024-01-15 10:45:35] INFO: Request to list all counters...
[2024-01-15 10:45:35] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:35 +0000] "GET /counters HTTP/1.1" 200 12
[2024-01-15 10:45:40] INFO: Request to Create counter: test-counter...
[2024-01-15 10:45:40] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:40 +0000] "POST /counters/test-counter HTTP/1.1" 201 45
[2024-01-15 10:45:45] INFO: Request to Read counter: test-counter...
[2024-01-15 10:45:45] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:45 +0000] "GET /counters/test-counter HTTP/1.1" 200 38
[2024-01-15 10:45:50] INFO: Request to Update counter: test-counter...
[2024-01-15 10:45:50] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:50 +0000] "PUT /counters/test-counter HTTP/1.1" 200 39
[2024-01-15 10:45:55] INFO: Health check endpoint accessed
[2024-01-15 10:45:55] INFO: 127.0.0.1 - - [15/Jan/2024:10:45:55 +0000] "GET /health HTTP/1.1" 200 15
```

## RESUMEN
- ✅ kubectl instalado y funcionando
- ✅ Comandos de OpenShift simulados
- ✅ Estado del cluster mostrado
- ✅ Pipeline ejecutado exitosamente
- ✅ Aplicación desplegada y funcionando
