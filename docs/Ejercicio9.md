# Documentación Ejercicio 9: Orquestación con Docker Compose (Aun hay presencia de errores)

## 1. Componentes Principales

### 1.1 Configuración de Docker Compose (templates/docker-compose.yml.j2)

- **Servicios definidos**:
    - 3 instancias de aplicación Flask (puertos 5000, 5001, 5002)
    - Balanceador de carga Nginx (puerto 80)
- **Características**:
    - Red bridge personalizada para comunicación entre servicios
    - Volúmenes para persistencia
    - Reinicio automático de contenedores
    - Gestión de dependencias entre servicios

### 1.2 Tareas Principales (ansible/ejercicio9/main.yml)

- **Instalación**: Descarga e instalación de Docker Compose
- **Configuración**: Creación de directorios y copia de archivos
- **Despliegue**: Gestión del ciclo de vida de contenedores
- **Verificación**: Comprobación de disponibilidad de servicios

### 1.3 Archivos de Soporte

- **Plantillas en templates/**:
    - `Dockerfile.j2`: Construcción de imagen Flask
    - `requirements.txt.j2`: Dependencias de la aplicación
    - `flask_app.py.j2`: Código fuente de la aplicación
    - `nginx_load_balancer.conf.j2`: Configuración del balanceo

### 1.4 Handlers (handlers/main.yml)

- Handler específico para reiniciar servicios Docker Compose

## 2. Verificación y Comprobación

### 2.1 Comandos Esenciales
```bash
# Verificar estado del despliegue
docker-compose ps

# Revisar logs
docker-compose logs

# Verificar balanceador
curl localhost:80

# Comprobar aplicaciones Flask
curl localhost:5000
```

### 2.2 Mantenimiento Básico
```bash
# Reiniciar servicios
docker-compose restart

# Detener servicios
docker-compose down

# Monitorear en tiempo real
docker-compose logs -f
```

## 3. Solución de Problemas

- Verificar permisos de archivos en `/opt/docker_compose_app`
- Comprobar conectividad entre contenedores
- Revisar logs de aplicaciones y Nginx
- Verificar configuración de puertos y redes
- Aun no se soluciona los bugs :c