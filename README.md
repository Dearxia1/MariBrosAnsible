# Training Ansible: Docker Deployment

Este proyecto automatiza la instalación de Docker y el despliegue de un contenedor de Super Mario Bros en una VM de Azure utilizando Ansible.

## 🚀 Requisitos previos

- Ansible instalado (probado en WSL2 Ubuntu).
- Una máquina virtual con Ubuntu 22.04.
- El puerto **22** (SSH) y el puerto **8787** (App) deben estar abiertos en el Firewall/NSG de la infraestructura (Azure/AWS).

## 🛠️ Configuración

### 1. Inventario
Actualiza el archivo `inventory/hosts.ini` con la IP de tu servidor y las credenciales.
> [!IMPORTANT]
> Nunca subas credenciales reales al repositorio. Usa variables de entorno o Ansible Vault para producción.

```ini
[azure_vm]
<TU_IP_PUBLICA> ansible_user=<TU_USUARIO> ansible_ssh_pass=<TU_CONTRASEÑA>
```

## 🎮 Despliegue

Sigue estos pasos para poner en marcha el servidor:

1. **Instalar Docker**:
   ```bash
   ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml
   ```

2. **Ejecutar el contenedor de Mario**:
   ```bash
   ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml
   ```

Una vez completado, la aplicación estará disponible en: `http://<TU_IP_PUBLICA>:8787`

## 📂 Estructura del Proyecto

- `inventory/`: Contiene la definición de los hosts.
- `playbooks/`: Playbooks principales para orquestar las tareas.
- `roles/`:
  - `docker_install`: Lógica para instalar Docker Engine y sus dependencias.
  - `docker_container`: Configuración y ejecución del contenedor de Super Mario.