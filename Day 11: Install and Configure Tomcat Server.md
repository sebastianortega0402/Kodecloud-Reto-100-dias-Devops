<p align="center">
  <img src="https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/4c1526345524ed9608a35fb84e8f5ec064b3a1b9/images/TOMCAT.png" width="500">
</p>


# 🐱‍💻 Apache Tomcat Server

Apache Tomcat es un **servidor de aplicaciones web especializado en Java**.  
No es solo un servidor web como Apache HTTP o Nginx, sino un **contenedor de aplicaciones Java**.

---

## 🌐 ¿Qué hace Tomcat?

Tomcat:

- Recibe peticiones web (HTTP)  
- ☕ Ejecuta aplicaciones hechas en Java  
- 📤 Devuelve respuestas al navegador o a herramientas como `curl`  

---

## 🧩 Tipos de aplicaciones que ejecuta Tomcat

Tomcat corre aplicaciones Java basadas en:

- **Servlets**  
- **JSP (Java Server Pages)**  

Estas aplicaciones se empaquetan en archivos llamados **WAR**.

---

## 🌐 Ejemplo de funcionamiento

Al ejecutar:

```bash
curl http://stapp03:6400
Tomcat:

Escucha en el puerto 6400

Recibe la solicitud HTTP

Ejecuta la aplicación Java

Devuelve la respuesta (HTML, JSON, etc.)

📦 ¿Qué es un archivo .war?
WAR = Web Application Archive
Es un archivo comprimido (similar a .zip) que contiene:

Código Java compilado

Archivos HTML / JSP

Configuración de la aplicación

📁 Estructura interna típica de un WAR
📦 ROOT.war
├── 📄 index.jsp
├── 📁 META-INF/
└── 📁 WEB-INF/
    ├── 📄 web.xml
    └── 📁 classes/

🚀 Qué hace Tomcat con un archivo .war
Al colocar un .war en /usr/share/tomcat/webapps/:

Tomcat detecta el archivo

Lo descomprime automáticamente

Despliega y ejecuta la aplicación

✅ No requiere pasos adicionales

🌳 Significado de ROOT.war

En Tomcat, cada aplicación tiene un contexto, que determina la URL:

Archivo WAR	URL resultante
app.war	http://host:puerto/app
test.war	http://host:puerto/test
ROOT.war	http://host:puerto/
ROOT.war = aplicación principal, accesible directamente desde la raíz /.

🧠 Analogía sencilla

Tomcat → el edificio 🏬

Puerto 6400 → la puerta de entrada

WAR → una tienda

ROOT.war → la tienda principal

❌ Si el archivo no se llama ROOT.war, la URL base / no funcionará.

✅ Resumen rápido Tomcat

Servidor de aplicaciones Java

Ejecuta aplicaciones web

Usa archivos WAR para despliegue

ROOT.war

Aplicación Java

Se despliega en la raíz /

Permite acceso directo a la URL base

📦 Paso 1: Instalar Tomcat
En CentOS / RHEL:

sudo yum install tomcat -y
Instala:

Apache Tomcat

Java (dependencia)

Archivos en /usr/share/tomcat

⚙️ Paso 2: Configurar Tomcat en el puerto 6400
Edita el archivo de configuración:

sudo vi /usr/share/tomcat/conf/server.xml
Busca el conector (normalmente puerto 8080):

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

# Verificar estado
sudo systemctl status tomcat
Debe aparecer: active (running) ✅

📁 Paso 4: Copiar ROOT.war desde el Jump Host
scp /tmp/ROOT.war stapp03:/tmp
📦 Paso 5: Desplegar la aplicación en Tomcat
En App Server 3:

sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
Tomcat descomprime automáticamente ROOT.war

El nombre ROOT.war despliega la app en /

🔄 Paso 6: Reiniciar Tomcat
sudo systemctl restart tomcat
🧪 Paso 7: Verificar que la aplicación funciona
curl http://stapp03:6400
✅ Si recibes HTML o contenido de la app → TODO CORRECTO



🧪 Paso 8: Verificar que la aplicación funciona
Ejecuta:

curl http://stapp03:6400

✅ Si ves HTML o contenido de la app → TODO CORRECTO
