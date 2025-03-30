
# Infrastructura Ansible

Este repositorio documenta la infraestructura configurada para la automatización con Ansible. La arquitectura consta de una máquina de control que orquesta las configuraciones y despliegues en varias máquinas gestionadas.

## ¿Que es Ansible?

Ansible es un motor open source que automatiza una gran cantidad de procesos informáticos, como la preparación de la infraestructura, la gestión de la configuración, la implementación de las aplicaciones y la organización de los sistemas.

## Arquitectura

La infraestructura está compuesta por:

- 🖥️ Control Node: Una máquina virtual con Ubuntu, encargada de ejecutar Ansible y gestionar las configuraciones.

- 📡 Managed Nodes: Tres máquinas virtuales con Ubuntu, que reciben y ejecutan las órdenes enviadas desde el nodo de control.

## Esquema de la Infraestructura

                       +----------------+
                       | Control Node   |
                       | (Ubuntu VM)    |
                       | 192.168.1.31   |
                       +----------------+
                                |
                                |
            --------------------|------------------
            |                   |                 |
    +----------------+ +----------------+ +----------------+
    | Managed Node 1 | | Managed Node 2 | | Managed Node 3 |
    |   (Ubuntu1)    | |   (Ubuntu2)    | |   (Ubuntu3)    |
    | 192.168.1.31   | | 192.168.1.33   | | 192.168.1.34   |
    +----------------+ +----------------+ +----------------+


## Configuración

 1. Instalar Ansible en el Control Node

 ```bash
 sudo apt update && sudo apt install -y ansible
 ```
 2. Configurar el archivo de inventario (/etc/ansible/hosts)

 ```bash
[servidores]
ubuntu1 ansible_host=192.168.1.32 ansible_user=ubuntu1 ansible_password=ubuntu1 ansible_become_pass=ubuntu1
ubuntu2 ansible_host=192.168.1.33 ansible_user=ubuntu2 ansible_password=ubuntu2 ansible_become_pass=ubuntu2
ubuntu3 ansible_host=192.168.1.34 ansible_user=ubuntu3 ansible_password=ubuntu3 ansible_become_pass=ubuntu3
```

El siguiente comando define un host en el archivo de inventory de Ansible y especifica cómo conectarse a él:

Descripción de cada parámetro:

- ubuntu1 → Nombre del host en el inventory. Puede ser cualquier alias que el usuario quiera asignarle.

- ansible_host=192.168.1.32 → Dirección IP o nombre de dominio del host al que Ansible se conectará.

- ansible_user=ubuntu1 → Usuario con el que Ansible se conectará al host remoto.

- ansible_password=ubuntu1 → Contraseña del usuario especificado para autenticarse en la máquina remota.

- ansible_become_pass=ubuntu1 → Contraseña para elevar privilegios con sudo cuando se necesiten permisos administrativos.

3. Verificar conectividad

```bash
ansible-playbook playbook.yml
```

## 📌 Notas

- Asegúrate de que todas las máquinas tienen Python instalado.
- Puedes ampliar esta infraestructura agregando más nodos en el inventario.
- Para ejecutar comandos en todos los nodos:

```bash
ansible all -a "comando_a_ejecutar"
```
