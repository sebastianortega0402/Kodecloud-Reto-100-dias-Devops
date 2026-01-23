
🤖 ¿Qué es Ansible?
Ansible es una herramienta de automatización y gestión de configuración usada en DevOps para:
Configurar servidores


Instalar software


Ejecutar tareas repetitivas


Orquestar despliegues


Administrar muchos servidores al mismo tiempo


Todo esto desde una sola máquina, llamada Ansible Controller (en tu caso, el jump host).

🧠 Idea principal
En lugar de entrar servidor por servidor a ejecutar comandos manualmente, Ansible te permite decir:
“Haz esta tarea en todos estos servidores”
…y Ansible se encarga del resto.

🔌 ¿Cómo funciona Ansible?
Ansible funciona así:
1️⃣ Controller
Es la máquina donde instalas Ansible


Desde aquí ejecutas los comandos


Ejemplo: Jump Host


2️⃣ Managed Nodes
Son los servidores que Ansible administra


Ejemplo: App Servers, DB Servers


3️⃣ Comunicación
Usa SSH


No necesita agentes instalados en los servidores


Usa llaves SSH (password-less)



📄 ¿Qué usa Ansible para trabajar?
🔹 Inventory
Archivo donde defines los servidores:
app1
app2
db1


🔹 Módulos
Pequeños programas que hacen tareas específicas:
ping → probar conexión


yum / apt → instalar paquetes


service → manejar servicios


copy → copiar archivos


Ejemplo:
ansible all -m ping


🔹 Playbooks (YAML)
Archivos donde describes qué quieres que pase, no cómo hacerlo:
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


Administración masiva


Resumen rápido 
🧠 Concepto clave antes de empezar
pip3 instala paquetes de Python


Si instalas con un usuario normal → Ansible queda solo para ese usuario


Si instalas con root (sudo) → Ansible queda disponible globalmente


El binario quedará en /usr/local/bin/ansible


Por eso usamos sudo con pip3.

Se instaló con:

 sudo pip3 install ansible==4.9.0


Se verificó con:

 ansible --version
¿Dónde quedó instalado Ansible?
Puedes confirmarlo con:
which ansible

Normalmente será:
/usr/local/bin/ansible

Ese directorio está en el PATH global, por eso todos los usuarios pueden usarlo.
