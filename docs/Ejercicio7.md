# Ejercicio 7: Integración de Pruebas Automatizadas con Pytest

## Descripción General

Este ejercicio implementa la integración de pruebas automatizadas utilizando Pytest para la aplicación Flask, asegurando la calidad del código a través de pruebas unitarias y de integración.

## Estructura del Proyecto

### 1. Archivos de Configuración

- **ansible/ejercicio7/main.yml**: Archivo principal que orquesta la instalación y ejecución de pruebas
- **templates/pytest.ini.j2**: Define la configuración de Pytest
- **templates/test_flask_app.py.j2**: Contiene las pruebas unitarias

## Componentes Principales

### 1. Configuración de Entorno

- Creación de directorios para pruebas y resultados
- Establecimiento de permisos adecuados
- Configuración del PYTHONPATH

### 2. Estructura de Pruebas

- **Fixture del Cliente**: Configura el entorno de pruebas aislado
- **Pruebas Implementadas**:
    - Validación de ruta principal
    - Manejo de rutas inválidas
    - Verificación de códigos de estado HTTP

### 3. Sistema de Reportes

- Generación de reportes XML en formato JUnit
- Almacenamiento en `/opt/flask_app/test-results/`
- Registro detallado de resultados de pruebas

## Verificación y Comandos

### Comandos de Verificación

```bash

# Verificar instalación de Pytest

pip list | grep pytest

# Comprobar estructura de directorios

ls -la /opt/flask_app/tests ls -la /opt/flask_app/test-results

# Verificar archivos de configuración

cat /opt/flask_app/pytest.ini

# Comprobar archivos de prueba

cat /opt/flask_app/tests/test_flask_app.py

# Verificar resultados de las pruebas

cat /opt/flask_app/test-results/junit.xml

# Comprobar estado del symlink

ls -l /opt/flask_app/app.py

# Verificar logs del servicio

sudo journalctl -u flask_app_5000 
```

## Puntos de Control

### 1. Instalación y Configuración

- Pytest y dependencias instaladas correctamente
- Estructura de directorios creada
- Archivos de configuración en su lugar
- Symlink configurado correctamente

### 2. Ejecución de Pruebas

- Las pruebas se ejecutan sin errores
- Se generan reportes XML
- El manejo de errores funciona según lo esperado


## Notas Importantes

1. El symlink es crucial para que las pruebas encuentren la aplicación
2. El PYTHONPATH se configura dinámicamente para asegurar imports correctos
3. Los resultados de las pruebas se conservan para análisis posterior
4. El proceso de CI/CD se detiene si las pruebas fallan

## Solución de Problemas

- Verificar permisos de directorios y archivos
- Comprobar la configuración del PYTHONPATH
- Revisar logs del sistema para errores
- Asegurar que el symlink apunta al archivo correcto
