# Documentación Ejercicio 6: Seguridad Avanzada y Cumplimiento

## 1. Descripción General

El ejercicio implementa medidas de seguridad avanzada utilizando Ansible para fortalecer un sistema Linux, incluyendo:

- Instalación de herramientas de seguridad
- Configuración de políticas
- Endurecimiento de servicios
- Escaneo de vulnerabilidades

## 2. Estructura del Ejercicio

### 2.1 Archivos Principales

- [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html): Archivo principal que importa las tareas del ejercicio 6
- [main.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html): Contiene las tareas principales
- [main.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html): Manejadores específicos para reinicio de servicios

### 2.2 Templates Utilizados

1. **jail.local.j2**
    
    - Configura Fail2ban para protección contra ataques de fuerza bruta
    - Define tiempos de baneo y reglas para SSH
2. **pwquality.conf.j2**
    
    - Establece políticas de contraseñas
    - Define requisitos mínimos de complejidad
3. **sshd_config.j2**
    
    - Configuración endurecida para SSH
    - Restricciones de acceso root y autenticación
4. **nginx_hardened.conf.j2**
    
    - Headers de seguridad para Nginx
    - Configuración SSL/TLS
5. **nginx_apparmor.j2**
    
    - Perfil AppArmor para Nginx
    - Restricciones de acceso a archivos

## 3. Tareas Principales

### 3.1 Instalación de Herramientas

- Lynis: Auditoría de seguridad
- AppArmor: Control de acceso obligatorio
- RKHunter: Detección de rootkits
- Fail2ban: Prevención de intrusiones

### 3.2 Configuraciones de Seguridad

- Endurecimiento de SSH
- Políticas de contraseñas
- Configuración de Nginx
- Perfiles AppArmor

### 3.3 Escaneo y Reportes

- Ejecución de auditorías Lynis
- Generación de reportes de vulnerabilidades

## 4. Handlers Utilizados

- Reinicio de SSH
- Reinicio de Fail2ban
- Actualización de PAM
- Reinicio de AppArmor
- Reinicio de Nginx

## 5. Comandos de Verificación

### 5.1 Estado de Servicios

``` bash
sudo systemctl status fail2ban sudo systemctl status apparmor sudo systemctl status nginx sudo systemctl status ssh 
```

### 5.2 Verificación de Configuraciones

``` bash 
sudo nginx -t 
sudo sshd -T 
sudo apparmor_status 
sudo fail2ban-client status 
```

### 5.3 Verificación de Permisos

``` bash 
ls -l /etc/shadow ls -l /etc/gshadow ls -l /etc/passwd- ls -l /etc/group- 
```

## 6. Notas Importantes

- Asegurarse de tener permisos sudo
- Hacer backup antes de modificar configuraciones
- Verificar la sintaxis antes de aplicar cambios
- Monitorear logs después de cambios
- Realizar pruebas en entorno controlado primero

## 7. Solución de Problemas

- Verificar sintaxis de configuraciones
- Revisar logs del sistema
- Comprobar permisos de archivos
- Validar estado de servicios
- Monitorear recursos del sistema