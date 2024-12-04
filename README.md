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

git clone https://github.com/Arbues/PC5.git 
cd PC5/vagrant 
```

## Configuración y Ejecución

Nota: Al principio todos los ejercicios van a estar comentados, si requiere ejecutar el ejercicio 6, debera descomentar tambien los anteriores, esto debido a que algunos ejercicios posteriores toman por echo configuraciones previas :D 

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

ansible-playbook site.yml

# Ejecutar ejercicio específico

ansible-playbook site.yml --tags "ejercicioN"

# Modo prueba

ansible-playbook site.yml --check 
```

## Estructura de Ejercicios

### 1. Configuración Base

- Sistema base
- Usuarios y grupos
- [Ver documentación](https://github.com/Arbues/PC5/blob/main/docs/Ejercicio1.md)

### 2. Servicios Web Seguros

- Nginx + SSL
- Firewall UFW
- [Ver documentación](https://github.com/Arbues/PC5/blob/main/docs/Ejercicio2.md)

[Ejercicios 3-10...]

## Notas Importantes

### Dependencias

- Los ejercicios son incrementales
- Descomentar ejercicios previos en [site.yml](https://github.com/Arbues/PC5/blob/main/site.yml)
- Revisar docs antes de ejecutar (ya que el ejercicio 9 y 10 no se logro solucionar los bugs)

### Troubleshooting

```bash

# Logs de Ansible

tail -f /var/log/ansible.log

# Estado de servicios

systemctl status <servicio>

# Reiniciar desde cero

vagrant destroy -f vagrant up 
```


## Contribución

1. Fork del repositorio
2. Crear rama feature
3. Commit cambios
4. Push a la rama
5. Crear Pull Request
