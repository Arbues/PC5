# Documentación Ejercicio 3: Balanceador de Carga con Nginx

## Descripción General

Este ejercicio implementa un balanceador de carga utilizando Nginx para distribuir el tráfico entre tres instancias de una aplicación Flask.

## Estructura y Componentes

### 1. Archivo Principal (`site.yml`)

- Punto de entrada que importa las tareas del ejercicio 3
- Define la configuración base para Ansible
- Utiliza handlers específicos para el reinicio de servicios

### 2. Tareas Principales (`ansible/ejercicio3/main.yml`)

1. **Instalación de Dependencias**
    
    - Instala python3-pip
    - Configura Flask y Gunicorn vía pip
2. **Configuración de la Aplicación Flask**
    
    - Crea directorio `/opt/flask_app`
    - Despliega múltiples instancias de la aplicación Flask
    - Crea servicios systemd para cada instancia
3. **Configuración del Balanceador**
    
    - Configura Nginx como balanceador de carga
    - Distribuye tráfico entre puertos 5000, 5001 y 5002

### 3. Archivos de Plantilla

#### [flask_app.py.j2](https://github.com/Arbues/PC5/blob/main/templates/flask_app.py.j2)

- Define una aplicación Flask básica
- Configura el puerto dinámicamente usando variables

#### [flask_app.service.j2](https://github.com/Arbues/PC5/blob/main/templates/flask_app.service.j2)

- Define servicios systemd para cada instancia Flask
- Configura Gunicorn como servidor WSGI
- Establece parámetros de ejecución

#### [nginx_load_balancer.conf.j2](https://github.com/Arbues/PC5/blob/main/templates/nginx_load_balancer.conf.j2)

- Define configuración del balanceador de carga
- Establece upstream servers
- Configura proxy settings

### 4. Handlers (`handlers/main.yml`)

- **Recargar systemd**: Actualiza configuración de servicios
- **Reiniciar Flask app**: Reinicia las instancias de Flask
- **Reiniciar Nginx**: Aplica nueva configuración del balanceador

## Comandos de Verificación

```bash

# Verificar estado de servicios Flask

systemctl status flask_app_5000 systemctl status flask_app_5001 systemctl status flask_app_5002

# Verificar estado de Nginx

systemctl status nginx

# Comprobar puertos en uso

ss -tulpn | grep '500[0-2]'

# Permisos para proceder

sudo su

# Verificar configuración de Nginx

nginx -t

# Probar balanceo de carga

for i in {1..6}; do curl http://localhost; done

# Verificar logs

tail -f /var/log/nginx/access.log 
```

## Puntos de Verificación

1. **Servicios Flask**:
    
    - Tres instancias ejecutándose en puertos 5000-5002
    - Servicios systemd activos y habilitados
2. **Balanceador Nginx**:
    
    - Configuración sin errores
    - Distribución efectiva del tráfico
    - Logs mostrando rotación entre servidores
3. **Conectividad**:
    
    - Acceso web funcional
    - Respuestas correctas de la aplicación
    - Balanceo de carga efectivo

## Extra

- El balanceador utiliza el método round-robin por defecto
- Cada instancia Flask maneja su propio proceso Gunicorn
- La configuración permite escalar horizontalmente añadiendo más instancias

## Comprobacion de los resultados

![](https://i.imgur.com/yi8oygS.png)
![](https://i.imgur.com/oCTamNg.png)
![](https://i.imgur.com/4XIUUdi.png)
![](https://i.imgur.com/gIoJWs9.png)
![](https://i.imgur.com/tk8cfRr.png)
