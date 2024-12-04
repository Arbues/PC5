# Documentación Ejercicio 4: Monitoreo y Alertas

## Descripción General

Este ejercicio implementa un sistema de monitoreo utilizando Prometheus y Grafana para recolectar y visualizar métricas de las aplicaciones Flask, además de configurar alertas básicas.

## Estructura y Componentes

### 1. Archivo Principal (`site.yml`)

- Punto de entrada que importa las tareas del ejercicio 4
- Mantiene la configuración base de Ansible
- Integra los handlers necesarios para el reinicio de servicios

### 2. Tareas Principales (`ansible/ejercicio4/main.yml`)

1. **Instalación de Dependencias**
    - Instala Prometheus, Node Exporter y Python3-pip
    - Instala Grafana 10.0.3 desde paquete .deb
    - Actualiza caché de paquetes

2. **Instalación de Bibliotecas Python**
    - prometheus_client para métricas
    - flask-prometheus-metrics para integración

3. **Configuración de Prometheus y Grafana**
    - Crea directorio de configuración
    - Implementa configuración y reglas de alertas
    - Configura puertos UFW (9090, 3000, 9100)
    - Asegura servicios en ejecución
    - Configura Prometheus como fuente de datos en Grafana

4. **Configuración de Aplicaciones Flask**
    - Actualiza aplicaciones con soporte de métricas
    - Despliega en puertos 5000, 5001, 5002
    - Implementa monitoreo y endpoints de métricas

### 3. Archivos de Plantilla

#### prometheus.yml.j2
- Define intervalos de scraping (15s)
- Configura jobs para Prometheus, Node y Flask
- Incluye reglas de alertas

#### alert_rules.yml.j2
- Define alertas para latencia alta (>0.5s)
- Monitorea tasa de errores (>10%)
- Configura severidades y anotaciones

#### flask_app_metrics.py.j2
- Implementa contadores de requests
- Añade histogramas de latencia
- Expone endpoint /metrics

### 4. Handlers Relevantes

- Reinicio de Prometheus
- Reinicio de aplicaciones Flask
- Recarga de UFW
- Recarga de systemd

## Verificación

```bash
# Verificar servicios
systemctl status prometheus
systemctl status grafana-server
systemctl status flask_app_5000

# Verificar métricas
curl localhost:9090/metrics  # Prometheus
curl localhost:9100/metrics  # Node Exporter

```

## Puntos de Control

1. **Servicios Base**:
    - Prometheus activo y recolectando
    - Grafana accesible
    - Node Exporter funcionando

2. **Métricas de Aplicación**:
    - Endpoints /metrics accesibles
    - Métricas registrándose
    - Monitoreo funcionando

3. **Alertas**:
    - Reglas cargadas
    - Umbrales configurados
    - Notificaciones activas

## Accesos Web

- Prometheus: http://192.168.56.12:9090
- Grafana: http://192.168.56.12:3000

## Pruebas en la web del host local

![](https://i.imgur.com/Mui5bUY.png)

![](https://i.imgur.com/0K2gDmf.png)

![](https://i.imgur.com/7gMgras.png)
