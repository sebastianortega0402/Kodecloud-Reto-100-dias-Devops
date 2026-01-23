![IPTABLES](https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/a15d57d8a3f10653e59e2d859bc0dec41a5bfbd6/images/IPTABLES.png)

🔥 ¿Qué es iptables?

iptables es una herramienta de Linux que permite controlar el tráfico de red que entra, sale o pasa por un servidor.

👉 En términos simples:

iptables = firewall del sistema

Con iptables decides:

🔓 Qué puertos están abiertos

🔐 Qué conexiones se permiten

❌ Qué tráfico se bloquea

🧠 Conceptos básicos de iptables

📌 Cadenas (Chains)

Las reglas se organizan en cadenas, según el tipo de tráfico:

Cadena	Función

INPUT	Tráfico que entra al servidor

OUTPUT	Tráfico que sale del servidor

FORWARD	Tráfico que pasa por el servidor (modo router)

📌 En este caso, la cadena importante fue INPUT, porque el Jump Host necesitaba conectarse a stapp01.

📌 Reglas

Cada regla básicamente dice:

“Si el tráfico cumple estas condiciones → haz esto”

Ejemplo:

-p tcp --dport 3003 -j ACCEPT


Significado:

-p tcp → usa protocolo TCP

--dport 3003 → puerto destino 3003

-j ACCEPT → permitir la conexión

⚠️ Orden de las reglas (MUY importante)

iptables evalúa las reglas de arriba hacia abajo:

1️⃣ Primera regla
2️⃣ Segunda regla
3️⃣ ...
❌ Si encuentra un REJECT o DROP, el tráfico se bloquea

👉 Por eso insertamos la regla al inicio:

iptables -I INPUT 1 -p tcp --dport 3003 -j ACCEPT

🛠️ Comandos de iptables utilizados
🔹 Ver reglas actuales

iptables -L -n

Opciones:

-L → lista reglas

-n → no resolver nombres (más rápido)

Con números de línea:

iptables -L -n --line-numbers

🔹 Agregar una regla

iptables -I INPUT -p tcp --dport 3003 -j ACCEPT


✔ Permite conexiones entrantes al puerto 3003

🔹 Eliminar una regla
iptables -D INPUT 1


✔ Elimina la regla número 1

🔹 Guardar reglas (persistencia)

iptables-save | tee /etc/sysconfig/iptables


👉 Sin este paso, las reglas se pierden al reiniciar.

🌐 ¿Qué es netstat?

netstat es una herramienta para ver el estado de la red del sistema.

Permite saber:

🔓 Qué puertos están abiertos

👂 Qué servicios están escuchando

🧠 Qué proceso usa cada puerto

🧠 ¿Por qué usamos netstat en el lab?

Apache no arrancaba, así que necesitábamos responder:

❓ ¿Otro proceso ya está usando el puerto 3003?

🛠️ Comando netstat utilizado
netstat -tulnp


Significado de las opciones:

Opción	Significado

-t	TCP

-u	UDP

-l	Listening (escuchando)

-n	Mostrar números

-p	Muestra proceso (PID/servicio)

🔎 Filtrar por puerto 3003

netstat -tulnp | grep 3003


Salida clave observada:

127.0.0.1:3003  LISTEN  485/sendmail


👉 Esto indicó que:

❌ El puerto 3003 estaba ocupado

📬 El proceso era sendmail

🚫 Apache no podía iniciar

🧠 Resumen rápido (ideal para entrevista o examen)

🔹 iptables

Firewall de Linux

Controla tráfico entrante y saliente

Usa reglas organizadas en cadenas

🔹 netstat

Muestra puertos abiertos

Identifica servicios escuchando

Permite detectar conflictos de puertos

🔹 Problema real del laboratorio

Sendmail ocupaba el puerto 3003

Apache no podía arrancar

El firewall bloqueaba el acceso externo

Se abrió el puerto correcto en iptables
