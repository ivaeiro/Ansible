
# 📜 Playbooks en Ansible

Un playbook en Ansible es un archivo en formato YAML que define un conjunto de tareas para ejecutar en los nodos gestionados. Permiten la automatización de configuraciones, despliegues y otras tareas administrativas.

## Estructura básica de un Playbook

Un playbook típico se ve así:

```bash
---
- name: Configurar servidores
  hosts: managed_nodes
  become: true
  tasks:
    - name: Instalar paquetes esenciales
      apt:
        name:
          - curl
          - git
          - vim
        state: present
        update_cache: yes
    
    - name: Crear un archivo de prueba
      copy:
        dest: /home/usuario/testfile.txt
        content: "Este es un archivo de prueba creado por Ansible."
```
### Cómo ejecutar un Playbook

Para ejecutar un playbook, usa el siguiente comando en el nodo de control:

```bash
ansible-playbook nombre_del_playbook.yml
```
Ejemplo:

```bash
ansible-playbook setup.yml
```

### Verificar qué hará un Playbook sin ejecutarlo

Puedes hacer una ejecución en modo de prueba con:

```bash
ansible-playbook nombre_del_playbook.yml --check
```

### Ejecución con privilegios de superusuario

```bash
ansible-playbook nombre_del_playbook.yml --ask-become-pass
```
