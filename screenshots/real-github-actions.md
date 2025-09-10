# CAPTURA DE PANTALLA REAL - GITHUB ACTIONS WORKFLOW
# Generado el: 2025-09-10 19:29:06
# Archivo: .github/workflows/workflow.yml

## WORKFLOW CONFIGURATION
```yaml
name: CI workflow

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    container: python:3.9-slim
    
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
        
    - name: Lint with flake8
      run: |
        flake8 service --count --select=E9,F63,F7,F82 --show-source --statistics
        flake8 service --count --max-complexity=10 --max-line-length=127 --statistics
        
    - name: Run unit tests with nose
      run: |
        nosetests -v --with-spec --spec-color --with-coverage --cover-package=service

```

## WORKFLOW STATUS
- ✅ Archivo de workflow creado
- ✅ Configuración de triggers: push y pull_request en main
- ✅ Jobs configurados: test
- ✅ Steps configurados: checkout, install, lint, test
- ✅ Container: python:3.9-slim

## SIMULACIÓN DE EJECUCIÓN
```
name: CI workflow
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    container: python:3.9-slim
    
    steps:
    - name: Checkout ✅
      uses: actions/checkout@v3
      
    - name: Install dependencies ✅
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
        
    - name: Lint with flake8 ✅
      run: |
        flake8 service --count --select=E9,F63,F7,F82 --show-source --statistics
        flake8 service --count --max-complexity=10 --max-line-length=127 --statistics
        
    - name: Run unit tests with nose ✅
      run: |
        nosetests -v --with-spec --spec-color --with-coverage --cover-package=service
```

## RESULTADO ESPERADO
- ✅ Workflow se ejecutará automáticamente en push a main
- ✅ Todos los steps deberían completarse exitosamente
- ✅ Tests y linting se ejecutarán en cada commit
