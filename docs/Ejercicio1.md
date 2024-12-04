# Documentación Ejercicio de Configuración Básica del Sistema

### Plan de Implementación

1. Configuración de paquetes del sistema
2. Configuración de zona horaria
3. Gestión de usuarios y grupos

### Archivos Necesarios
### Detalles de Implementación

1. **Actualización del Sistema**
    
    - Actualiza el caché de paquetes
    - Realiza una actualización completa del sistema
2. **Configuración de Zona Horaria**
    
    - Establece la zona horaria a América/Lima
    - Asegura la consistencia horaria en el sistema
3. **Gestión de Usuarios**
    
    - Crea grupo 'admin'
    - Crea usuario 'devuser' con acceso administrativo
    - Implementa contraseña cifrada por seguridad

### Verificacion
``` bash
# Verificar usuario creado
id devuser

# Verificar zona horaria
timedatectl

# Verificar grupo admin
getent group admin
```

### Notas Importantes

- La contraseña está pre-cifrada por limitaciones de passlib
- El usuario devuser tiene privilegios administrativos
- La zona horaria está configurada específicamente para Perú