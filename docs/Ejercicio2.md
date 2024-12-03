# Documentación Ejercicio 2: Implementación de Servicios Web con Seguridad Básica

## Estructura y Componentes

### 1. Archivo Principal (`site.yml`)
- Punto de entrada principal que importa las tareas del ejercicio 2
- Establece la configuración base para la ejecución de Ansible
- Define el usuario y método de elevación de privilegios

### 2. Tareas Principales (`ansible/ejercicio2/main.yml`)
Contiene 5 tareas fundamentales:
1. **Instalación de Nginx**
   - Gestiona la instalación del servidor web
   - Asegura que Nginx esté presente en el sistema

2. **Generación de Certificados SSL**
   - Crea certificados autofirmados válidos por 365 días
   - Establece parámetros básicos de identidad del certificado
   - Almacena los certificados en `/etc/ssl/private/` y `/etc/ssl/certs/`

3. **Generación de Parámetros Diffie-Hellman**
   - Crea parámetros de seguridad adicionales
   - Mejora la seguridad de las conexiones SSL/TLS

4. **Configuración de Nginx con SSL**
   - Utiliza plantilla para configurar el servidor
   - Aplica los certificados generados
   - Activa el handler para reiniciar Nginx

5. **Configuración de UFW**
   - Habilita reglas de firewall específicas
   - Permite tráfico SSH y Nginx (HTTP/HTTPS)
   - Activa el handler para reiniciar UFW

### 3. Handlers (`handlers/main.yml`)
Contiene manejadores específicos:
- **Reinicio de Nginx**: Aplica cambios de configuración
- **Reinicio de UFW**: Actualiza reglas del firewall

### 4. Plantilla Nginx (`templates/nginx_ssl.conf.j2`)
- Define la configuración de escucha en puertos 80 y 443
- Establece rutas de certificados SSL
- Configura protocolos de seguridad y cifrado
- Establece proxy inverso para la aplicación Flask

## Comandos de Verificación

``` bash
# Verificar estado de Nginx
systemctl status nginx

# Comprobar certificados SSL
ls -l /etc/ssl/certs/nginx-selfsigned.crt
ls -l /etc/ssl/private/nginx-selfsigned.key

# Obtener mas permisos para ejecutar los comando posteriores
sudo su

# Verificar configuración de Nginx
nginx -t

# Comprobar puertos en escucha
ss -tulpn | grep nginx

# Verificar reglas UFW
ufw status

# Comprobar acceso HTTPS
curl -k https://localhost

# Verificar logs de Nginx
tail -f /var/log/nginx/access.log
```

## Puntos de Verificación Post-Implementación

1. **Servicio Nginx**:
   - Debe estar activo y ejecutándose
   - Sin errores en los logs

2. **Certificados SSL**:
   - Presentes en las ubicaciones correctas
   - Con permisos adecuados

3. **Firewall UFW**:
   - Reglas correctamente aplicadas
   - Puertos 22, 80 y 443 abiertos

4. **Acceso Web**:
   - HTTPS funcional (aunque con advertencia por certificado autofirmado)
   - Redirección correcta a la aplicación Flask

## Comprobacion de los resultados
![](https://i.imgur.com/8G9Fr0i.png)