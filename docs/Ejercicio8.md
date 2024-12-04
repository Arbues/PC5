# Documentación Ejercicio 8: Contenerización con Docker

## Implementación Detallada

### 1. Archivo Principal (`ansible/ejercicio8/main.yml`)

- **Preparación del Sistema**
    
    - Instalación de dependencias Docker
    - Configuración de repositorios y claves GPG
    - Activación del servicio Docker
- **Gestión de Servicios Previos**
    
    - Detención de servicios Flask anteriores (puertos 5000-5002)
    - Limpieza de procesos en puertos específicos
- **Configuración Docker**
    
    - Construcción de imagen desde Dockerfile
    - Gestión de contenedores múltiples
    - Mapeo de puertos para cada instancia

### 2. Archivos de Soporte

#### Templates

1. **Dockerfile.j2**
    
    - Base Python 3.8-slim
    - Configuración de entorno de trabajo
    - Variables de entorno para puerto
    - Exposición de puerto dinámico
2. **flask_app.py.j2**
    
    - Adaptación para entorno containerizado
    - Configuración de puerto mediante variables de entorno
    - Endpoint principal con identificación de contenedor
3. **requirements.txt.j2**
    
    - Dependencias mínimas necesarias
    - Flask y Gunicorn especificados
4. **nginx_load_balancer.conf.j2**
    
    - Configuración de upstream servers
    - Balanceo entre tres contenedores
    - Configuración de proxy_pass y headers

#### Handlers (`handlers/main.yml`)

- Handler para reinicio de Docker
- Handler para recarga de Nginx

## Verificación de Funcionalidad

### Comandos de Comprobación

*Observacion*: antes de entrar al VM comenta desde la 14 asta la 21 del main.yml en la carpeta handlers

```bash

# Estado de los contenedores

sudo docker ps

# Pruebas de balanceo

for i in {1..6}; do curl localhost; done

# Logs de contenedores

sudo docker logs flask-app-5000 
sudo docker logs flask-app-5001 
sudo docker logs flask-app-5002

# Estado de servicios

sudo systemctl status nginx sudo systemctl status docker 
```

### Verificación de Configuración

```bash

# Configuración de Nginx

sudo nginx -t

# Puertos activos

sudo ss -tulpn | grep -E '5000|5001|5002|80'

# Estado de la imagen

sudo docker images | grep flask-app 
```

## Notas de Implementación

- Los contenedores utilizan la misma imagen base
- Cada contenedor mantiene su propio estado
- Nginx distribuye las peticiones equitativamente
- La configuración permite escalar horizontalmente
- Los contenedores se reconstruyen en cada despliegue

## Consideraciones de Seguridad

- Permisos Docker correctamente configurados
- Exposición mínima de puertos necesarios
- Limpieza automática de recursos no utilizados
- Configuración segura de Nginx como reverse proxy

## Pruebas del resultado

![](https://i.imgur.com/IXBzgxE.png)