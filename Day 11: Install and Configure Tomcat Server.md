<p align="center">
  <img src="https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/4c1526345524ed9608a35fb84e8f5ec064b3a1b9/images/TOMCAT.png" width="500">
</p>


🐱‍💻 ¿Qué es Apache Tomcat Server?

Apache Tomcat es un servidor de aplicaciones web especializado en Java.
No es solo un servidor web como Apache HTTP o Nginx, sino un contenedor de aplicaciones Java.

👉 En palabras simples, Tomcat es el programa que:

🌐 Recibe peticiones web (HTTP)

☕ Ejecuta aplicaciones hechas en Java

📤 Devuelve respuestas al navegador o a herramientas como curl

🧩 ¿Qué tipo de aplicaciones ejecuta Tomcat?

Tomcat corre aplicaciones Java basadas en:

Servlets

JSP (Java Server Pages)

Estas aplicaciones se empaquetan en archivos llamados WAR.

🌐 Ejemplo real de funcionamiento

Cuando ejecutas:

curl http://stapp03:6400


Tomcat hace lo siguiente:

Escucha en el puerto 6400

Recibe la solicitud HTTP

Ejecuta la aplicación Java

Devuelve la respuesta (HTML, JSON, etc.)

📦 ¿Qué es un archivo .war?

WAR significa: Web Application Archive

Es un archivo comprimido (similar a .zip) que contiene:

Código Java compilado

Archivos HTML / JSP

Configuración de la aplicación

## 📁 Estructura interna típica
📦 ROOT.war
├── 📄 index.jsp
├── 📁 META-INF/
└── 📁 WEB-INF/
├── 📄 web.xml
└── 📁 classes/

🚀 ¿Qué hace Tomcat con un archivo .war?

Cuando colocas un .war en:  /usr/share/tomcat/webapps/

Tomcat:

Detecta el archivo

Lo descomprime automáticamente

Despliega y ejecuta la aplicación

👉 Sin necesidad de pasos adicionales 👍

🌳 ¿Qué significa ROOT.war?

Este punto es clave en Tomcat.

🔹 En Tomcat, cada aplicación tiene un contexto:

Archivo WAR	URL resultante

app.war	http://host:puerto/app
test.war	http://host:puerto/test
ROOT.war	http://host:puerto/

⭐ ROOT.war = aplicación principal

Por eso funciona directamente:

curl http://stapp03:6400


Sin /ROOT ni /app.

🧠 Analogía sencilla

Imagina Tomcat como un centro comercial 🏬:

Tomcat → el edificio

Puerto 6400 → la puerta de entrada

WAR → una tienda

ROOT.war → la tienda principal al entrar

🧪 ¿Qué pasaría si NO fuera ROOT.war?

Si el archivo se llamara:

beta.war


La URL sería:

http://stapp03:6400/beta


❌ Y la URL base (/) no funcionaría.

✅ Resumen rápido

Tomcat

✔ Servidor de aplicaciones Java
✔ Ejecuta aplicaciones web
✔ Usa archivos WAR para despliegue

ROOT.war

✔ Aplicación Java
✔ Se despliega en la raíz /
✔ Permite acceso directo a la URL base

📦 Paso 1: Instalar Tomcat

En sistemas CentOS / RHEL:

sudo yum install tomcat -y


📌 Esto instala:

Apache Tomcat

Java (dependencia)

Archivos en /usr/share/tomcat

⚙️ Paso 2: Configurar Tomcat para usar el puerto 6400

Edita el archivo de configuración:

sudo vi /usr/share/tomcat/conf/server.xml


Busca el conector (normalmente puerto 8080):

```xml
<Connector port="8080" protocol="org.apache.coyote.http11.Http11NioProtocol"
           connectionTimeout="20000"
           redirectPort="8443" />


✏️ Cámbialo a:

<Connector port="6400" protocol="org.apache.coyote.http11.Http11NioProtocol"
           connectionTimeout="20000"
           redirectPort="8443" />



Guarda y sal (ESC :wq).

🚀 Paso 3: Iniciar y habilitar Tomcat

sudo systemctl start tomcat
sudo systemctl enable tomcat

Verifica el estado:

sudo systemctl status tomcat

Debe aparecer active (running) ✅

📁 Paso 4: Copiar ROOT.war desde el Jump Host

Desde el Jump Host:

scp /tmp/ROOT.war stapp03:/tmp

📦 Paso 5: Desplegar la aplicación en Tomcat

En App Server 3:

sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/


📌 Tomcat descomprime automáticamente ROOT.war
📌 El nombre ROOT.war despliega la app en /

🔄 Paso 6: Reiniciar Tomcat

sudo systemctl restart tomcat

🧪 Paso 7: Verificar que la aplicación funciona

curl http://stapp03:6400

✅ Si recibes HTML o contenido de la app → TODO CORRECTO

🧪 Paso 8: Verificar que la aplicación funciona
Ejecuta:

curl http://stapp03:6400

✅ Si ves HTML o contenido de la app → TODO CORRECTO
