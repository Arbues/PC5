# Documentación Ejercicio 9: Orquestación con Docker Compose

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

### 2.1 Comandos de Verificación
``` bash
# Verificar instalación de Docker Compose
docker-compose --version

# Verificar servicios en ejecución
docker-compose ps

# Comprobar logs de servicios
docker-compose logs

# Verificar estado de contenedores
docker ps -a

# Comprobar red creada
docker network ls

# Verificar puertos en escucha
netstat -tulpn | grep -E '5000|5001|5002|80'

# Probar balanceador de carga
curl localhost:80
```
### 2.2 Comprobación de Recursos
``` bash
# Estado de los servicios
systemctl status docker

# Verificar configuración Nginx
curl -I localhost:80

# Comprobar respuesta de aplicaciones Flask
for port in 5000 5001 5002; do curl localhost:$port; done
```
## 3. Mantenimiento y Gestión

### 3.1 Operaciones Comunes
``` bash
# Reiniciar servicios
cd /opt/docker_compose_app && docker-compose restart

# Actualizar servicios
cd /opt/docker_compose_app && docker-compose up -d --build

# Detener servicios
cd /opt/docker_compose_app && docker-compose down
```
### 3.2 Monitoreo
``` bash
# Ver estadísticas de contenedores
docker stats

# Monitorear logs en tiempo real
docker-compose logs -f

# Verificar uso de recursos
docker-compose top
```
## 4. Solución de Problemas

- Verificar permisos de archivos en `/opt/docker_compose_app`
- Comprobar conectividad entre contenedores
- Revisar logs de aplicaciones y Nginx
- Verificar configuración de puertos y redes