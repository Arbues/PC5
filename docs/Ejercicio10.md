# Documentación Ejercicio 10: Implementación CI con Pytest y Docker

## Descripción General

Este ejercicio implementa un pipeline completo de Integración Continua (CI) utilizando GitHub Actions, Pytest y Docker, integrándose con la infraestructura Ansible existente.

## Componentes Principales

### 1. Pipeline CI (.github/workflows/ci.yml)

- **Propósito**: Automatiza pruebas y despliegue
- **Triggers**: Push a main y Pull Requests
- **Jobs**:
    - Test: Ejecuta pruebas unitarias
    - Build: Construye y publica imagen Docker

### 2. Pruebas Automatizadas (templates/test_flask_app.py.j2)

- **Funcionalidad**: Test unitarios para la aplicación Flask
- **Cobertura**:
    - Verificación de página principal
    - Validación de configuración de puertos
    - Fixture de cliente de prueba

### 3. Dependencias (templates/requirements.txt.j2)

- **Nuevas inclusiones**:
    - pytest para pruebas automatizadas
    - Versiones específicas de Flask y Gunicorn

### 4. Tareas Ansible (ansible/ejercicio10/main.yml)

**Flujo de tareas**:

1. Copia archivos de prueba
2. Actualiza requirements
3. Instala dependencias
4. Ejecuta pruebas
5. Construye imagen Docker
6. Despliega contenedores

### 5. Handlers (handlers/main.yml)

- **Notificación**: Resultados del pipeline CI
- **Condiciones**: Ejecución basada en resultados de pruebas

## Verificación y Comandos

### Verificar Estado de Tareas

``` bash 
vagrant ssh cd /opt/docker_app ansible-playbook -i inventory [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) --tags "ejercicio10" --check 
```

### Comprobar Pruebas

```bash 
cd /opt/docker_app pytest test_flask_app.py -v 
```

### Verificar Contenedores

```bash 
docker ps | grep flask-app docker images | grep flask-app 
```

### Validar Puertos

```bash 
netstat -tulpn | grep 500 curl localhost:5000 curl localhost:5001 curl localhost:5002 
```

### Logs y Diagnóstico

```bash 
docker logs flask-app-5000 ansible-playbook [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) --tags "ejercicio10" -v 
```

## Dependencias y Prerrequisitos

### Software Requerido

- Python 3.8+
- Docker
- Pytest
- Ansible
- GitHub Actions configurado

### Variables de Entorno

- DOCKER_HUB_USERNAME
- DOCKER_HUB_TOKEN

### Permisos Necesarios

- Acceso a Docker Hub
- Permisos de escritura en /opt/docker_app
- Acceso a GitHub Actions

## Monitoreo y Mantenimiento

### Logs

- Logs de Docker: `/var/log/docker`
- Logs de Ansible: `/var/log/ansible.log`
- Logs de aplicación: Dentro de cada contenedor

### Métricas Importantes

- Tiempo de ejecución de pruebas
- Estado de contenedores
- Uso de recursos
- Tiempo de construcción de imagen

## Resolución de Problemas

### Problemas Comunes

1. Fallos en pruebas ```bash pytest -v --tb=short ```
    
2. Problemas de Docker ```bash docker system df docker system prune ```
    
3. Problemas de red ```bash sudo systemctl status nginx netstat -tulpn ```
    

### Verificación de Salud

```bash ansible-playbook [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) --tags "ejercicio10" --list-tasks docker-compose ps ```

## Notas Adicionales

- Las pruebas deben pasar antes del despliegue
- Backup recomendado antes de actualizaciones
- Monitorear uso de recursos
- Revisar logs periódicamente