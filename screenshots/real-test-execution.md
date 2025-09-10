
# CAPTURA DE PANTALLA REAL - EJECUCIÓN DE TESTS
# Generado el: 2025-09-10 19:29:06
# Proyecto: CI/CD Final Project

## FLAKE8 LINTING - ERRORES CRÍTICOS
```bash
python -m flake8 service --count --select=E9,F63,F7,F82 --show-source --statistics
```
Return code: 1

C:\Users\ferna\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe: No module named flake8


## FLAKE8 LINTING - COMPLEJIDAD
```bash
python -m flake8 service --count --max-complexity=10 --max-line-length=127 --statistics
```
Return code: 1

C:\Users\ferna\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe: No module named flake8


## TESTS UNITARIOS
```bash
python -m unittest tests.test_routes -v
```
Return code: 1

test_routes (unittest.loader._FailedTest.test_routes) ... ERROR

======================================================================
ERROR: test_routes (unittest.loader._FailedTest.test_routes)
----------------------------------------------------------------------
ImportError: Failed to import test module: test_routes
Traceback (most recent call last):
  File "C:\Program Files\WindowsApps\PythonSoftwareFoundation.Python.3.12_3.12.2800.0_x64__qbz5n2kfra8p0\Lib\unittest\loader.py", line 137, in loadTestsFromName
    module = __import__(module_name)
             ^^^^^^^^^^^^^^^^^^^^^^^
  File "C:\Dv\Repo\ci-cd-final-project\tests\test_routes.py", line 9, in <module>
    from service.common import status  # HTTP Status Codes
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "C:\Dv\Repo\ci-cd-final-project\service\__init__.py", line 4, in <module>
    from flask import Flask
ModuleNotFoundError: No module named 'flask'


----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (errors=1)


## RESUMEN
- Linting crítico: ❌ FAILED
- Linting complejidad: ❌ FAILED
- Tests unitarios: ❌ FAILED
