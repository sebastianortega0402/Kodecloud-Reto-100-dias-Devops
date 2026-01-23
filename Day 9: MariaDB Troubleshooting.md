![MARIADB](https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/36b9326add591a908de670cc9a6df093eea89f32/images/Maria%20DB.png)


# 🗄️ MariaDB – Sistema de Gestión de Bases de Datos

MariaDB es un **Database Server** que almacena, organiza y entrega información a las aplicaciones.

En este escenario:

- 🧩 La aplicación **Nautilus** necesita conectarse a MariaDB  
- 📥 Para leer y guardar datos críticos  
- ❌ Si MariaDB está caído, la aplicación **no puede funcionar**

---

## ❌ Problema detectado

El problema **NO era**:

- 🚫 La red  
- 🚫 La aplicación  

👉 El error real fue que el directorio de datos de MariaDB **no existía**:

/var/lib/mysql


---

## 📂 ¿Para qué sirve `/var/lib/mysql`?

MariaDB lo usa para:

- 🗄️ Guardar las bases de datos  
- 📊 Almacenar tablas  
- 👤 Gestionar usuarios  
- ⚙️ Mantener configuraciones internas  

❗ Al no existir el directorio:

- MariaDB no podía inicializarse  
- El servicio fallaba al arrancar  
- Nautilus no podía conectarse a la base de datos  

Por eso aparecía el error al ejecutar:

```bash
systemctl start mariadb
🛠️ Cómo se corrigió el problema
⚠️ Nota importante:
Este procedimiento crea una base de datos limpia.
Si la aplicación dependía de datos anteriores y no hay backup, esos datos ya no estarán disponibles.

1️⃣ Crear el directorio de datos
sudo mkdir -p /var/lib/mysql
2️⃣ Asignar permisos correctos
sudo chown -R mysql:mysql /var/lib/mysql
sudo chmod 755 /var/lib/mysql
3️⃣ Inicializar la base de datos
Ejecuta uno de estos comandos (elige el que esté disponible en tu sistema):

sudo mariadb-install-db --user=mysql --datadir=/var/lib/mysql
4️⃣ Levantar el servicio MariaDB
sudo systemctl start mariadb
5️⃣ Verificar el estado del servicio
sudo systemctl status mariadb
✅ Si el estado aparece como active (running), MariaDB está funcionando correctamente.



