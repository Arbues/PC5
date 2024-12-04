# # PC5 - Desarrollo de Software

## Descripción

Proyecto de automatización y despliegue usando Ansible, Docker y herramientas DevOps para la PC5.

## Requisitos Previos

### Software Necesario

```bash

# Verificar versiones instaladas

virtualbox --help vagrant --version ansible --version git --version 
```

### Instalación en Linux

```bash

# Actualizar repositorios

sudo apt update

# Instalar VirtualBox

sudo apt install virtualbox

# Instalar Vagrant

sudo apt install vagrant

# Instalar Ansible

sudo apt install ansible

# Clonar repositorio

git clone <URL-repo> cd PC5 
```

## Configuración y Ejecución

### Iniciar Entorno

```bash

# Crear y provisionar VM

vagrant up

# Verificar estado

vagrant status

# Acceder a la VM

vagrant ssh 
```

### Ejecutar Ejercicios

```bash

# Ejecutar todos los ejercicios

ansible-playbook [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

# Ejecutar ejercicio específico

ansible-playbook [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) --tags "ejercicioN"

# Modo prueba

ansible-playbook [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) --check 
```

## Estructura de Ejercicios

### 1. Configuración Base

- Sistema base
- Usuarios y grupos
- [Ver documentación](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

### 2. Servicios Web Seguros

- Nginx + SSL
- Firewall UFW
- [Ver documentación](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

[Ejercicios 3-10...]

## Notas Importantes

### Dependencias

- Los ejercicios son incrementales
- Descomentar ejercicios previos en [site.yml](vscode-file://vscode-app/c:/Users/kikhe/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)
- Revisar docs antes de ejecutar

### Troubleshooting

```bash

# Logs de Ansible

tail -f /var/log/ansible.log

# Estado de servicios

systemctl status <servicio>

# Reiniciar desde cero

vagrant destroy -f vagrant up 
```

### Mantenimiento

- Backups regulares recomendados
- Monitorear recursos
- Actualizar dependencias

## Contribución

1. Fork del repositorio
2. Crear rama feature
3. Commit cambios
4. Push a la rama
5. Crear Pull Request

### Estándares

- Seguir convenciones Ansible
- Documentar cambios
- Agregar pruebas