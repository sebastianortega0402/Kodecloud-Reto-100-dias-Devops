![Ansible](https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/90ac0d156923d91301c9655ab20e9bdb19d3505c/images/ANSIBLE.png)

🤖 ¿Qué es Ansible?

Ansible es una herramienta de automatización y gestión de configuración muy usada en DevOps.
Permite administrar servidores y aplicaciones de forma simple, segura y escalable.

Con Ansible puedes:

⚙️ Configurar servidores

📦 Instalar software

🔁 Ejecutar tareas repetitivas

🚀 Orquestar despliegues

🖥️ Administrar múltiples servidores al mismo tiempo

Todo esto desde una sola máquina, llamada Ansible Controller (en este caso, el Jump Host).

🧠 Idea principal

En lugar de conectarte servidor por servidor y ejecutar comandos manualmente, con Ansible solo dices:

“Haz esta tarea en todos estos servidores”

Y Ansible se encarga del resto ✨

🔌 ¿Cómo funciona Ansible?

1️⃣ Controller

Es la máquina donde se instala Ansible

Desde aquí se ejecutan los comandos y playbooks

Ejemplo: Jump Host

2️⃣ Managed Nodes

Son los servidores que Ansible administra

Ejemplos:

App Servers

DB Servers

3️⃣ Comunicación

Usa SSH

❌ No necesita agentes en los servidores

🔑 Utiliza llaves SSH (password-less authentication)

📄 ¿Qué usa Ansible para trabajar?
🔹 Inventory

Archivo donde defines los servidores que serán administrados:

app1
app2
db1

🔹 Módulos

Pequeños programas que ejecutan tareas específicas:

ping → probar conexión

yum / apt → instalar paquetes

service → manejar servicios

copy → copiar archivos

Ejemplo:

ansible all -m ping

🔹 Playbooks (YAML)

Archivos donde describes qué quieres que pase, no cómo hacerlo.

Ejemplo:

- hosts: app
  tasks:
    - name: Install httpd
      yum:
        name: httpd
        state: present

⭐ Ventajas principales de Ansible

✔ No necesita agentes
✔ Usa SSH
✔ Fácil de aprender
✔ Usa YAML (legible para humanos)
✔ Escala muy bien
✔ Ideal para automatización y CI/CD

🔁 ¿Para qué se usa Ansible en la vida real?

Configurar servidores nuevos

Mantener sistemas consistentes

Automatizar despliegues

Aplicar parches

Administración masiva de infraestructura

🧠 Conceptos clave antes de empezar

pip3 instala paquetes de Python

Si instalas con un usuario normal, Ansible queda disponible solo para ese usuario

Si instalas con root (sudo), Ansible queda disponible globalmente

El binario normalmente se instala en:

/usr/local/bin/ansible


👉 Por eso usamos sudo con pip3.

📦 Instalación de Ansible
Instalar:
sudo pip3 install ansible==4.9.0

Verificar versión:
ansible --version

Confirmar ubicación:
which ansible


Salida esperada:

/usr/local/bin/ansible
Ese directorio está en el PATH global, por eso todos los usuarios pueden usarlo.
