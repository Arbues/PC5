# Documentación Ejercicio 5: Alta Disponibilidad y Recuperación de Desastres

## Descripción General

Este ejercicio implementa una solución de alta disponibilidad y recuperación ante desastres utilizando PostgreSQL 12 con replicación, backups automatizados y failover mediante Keepalived.

## Estructura y Componentes

### 1. Archivo Principal (`site.yml`)

- Importa las tareas del ejercicio 5
- Configura la ejecución de Ansible
- Utiliza handlers específicos para PostgreSQL y Keepalived

### 2. Tareas Principales (`ansible/ejercicio5/main.yml`)

#### Instalación y Configuración Base

- Instala PostgreSQL 12 y dependencias necesarias
- Crea y configura el cluster PostgreSQL
- Configura la replicación y autenticación

#### Configuración de Usuario y Replicación

- Establece contraseña del usuario postgres
- Crea usuario replicador con permisos específicos
- Implementa espera para asegurar disponibilidad del servicio

#### Sistema de Backup

- Crea directorio para backups
- Implementa script de backup automatizado
- Configura tarea cron para ejecución nocturna

#### Alta Disponibilidad

- Configura Keepalived para failover automático
- Implementa verificación de estado de PostgreSQL
- Gestiona IP virtual para alta disponibilidad

### 3. Archivos de Configuración

#### PostgreSQL (`postgresql.conf.j2`)

- Define configuración base de PostgreSQL
- Habilita replicación y streaming
- Configura parámetros de rendimiento

#### Autenticación (`pg_hba.conf.j2`)

- Define métodos de autenticación
- Configura acceso para replicación
- Establece seguridad de conexiones

#### Alta Disponibilidad (`keepalived.conf.j2`)

- Define configuración de Keepalived
- Implementa verificación de estado
- Gestiona IP virtual

#### Script de Backup (`backup_script.sh.j2`)

- Automatiza proceso de backup
- Implementa retención de 7 días
- Incluye verificación de éxito

### 4. Handlers Relevantes (`handlers/main.yml`)

- Reinicio de PostgreSQL
- Reinicio de Keepalived

## Comandos de Verificación

### PostgreSQL y Replicación

```bash

sudo su
# Estado del servicio PostgreSQL

systemctl status postgresql

# Verificar logs de PostgreSQL

tail -f /var/log/postgresql/postgresql-12-main.log

# Verificar configuración

sudo -u postgres psql -c "SHOW max_wal_senders;" sudo -u postgres psql -c "SHOW wal_level;"

# Listar roles y permisos

sudo -u postgres psql -c "\du" 
```

### Sistema de Backup

```bash

# Verificar directorio de backups

ls -l /opt/backups/

# Verificar permisos del script

ls -l /opt/backups/backup_script.sh

# Comprobar tarea cron

sudo crontab -l -u postgres

```

### Alta Disponibilidad

```bash

# Estado de Keepalived

systemctl status keepalived

# Verificar IP virtual

ip addr show

# Ver configuración de Keepalived

cat /etc/keepalived/keepalived.conf

# Verificar script de chequeo

pgrep postgres 
```

## Puntos de Verificación

1. **PostgreSQL**
    
    - Servicio activo y escuchando
    - Configuración de replicación correcta
    - Usuario replicador creado con permisos adecuados
2. **Sistema de Backup**
    
    - Script de backup presente y ejecutable
    - Tarea cron configurada
    - Backups generándose correctamente
    - Rotación de backups funcionando
3. **Alta Disponibilidad**
    
    - Keepalived activo y monitoreando
    - IP virtual accesible
    - Failover funcionando correctamente
    - Scripts de verificación ejecutándose

## Extra

- La replicación está configurada en modo streaming
- Los backups se ejecutan diariamente a las 3 AM
- El sistema mantiene los últimos 7 días de backups
- Keepalived verifica el estado de PostgreSQL cada 2 segundos