![NGNIX](https://github.com/sebastianortega0402/Kodecloud-Reto-100-dias-Devops/blob/54f10498cffccd7027325cd2455893b02c6fdf63/images/nginix.png)

# 🌐 Nginx – Servidor web de alto rendimiento

Nginx es un servidor web ligero y rápido que puede:

- 📄 Servir páginas web estáticas (HTML, imágenes, CSS, etc.)
- 🔐 Manejar HTTPS (SSL/TLS)
- 🔁 Actuar como proxy inverso para otras aplicaciones (Python, Node.js, Java, etc.)
- ⚖️ Balancear carga entre múltiples servidores

---

## 🔑 Conceptos clave de Nginx

| Concepto               | Explicación |
|------------------------|------------|
| **server**             | Bloque que define un sitio web: puerto, dominio y configuración |
| **listen**             | Puerto y protocolo donde Nginx escucha (HTTP / HTTPS) |
| **root**               | Directorio desde donde se sirven los archivos web |
| **SSL Certificate / Key** | Certificado y llave necesarios para habilitar HTTPS |

---

## 1️⃣ Instalar Nginx (stapp01)

```bash
sudo yum install -y nginx

# Habilitar y arrancar el servicio
sudo systemctl enable nginx
sudo systemctl start nginx

# Verificar estado
sudo systemctl status nginx
Debe aparecer: active (running) ✅

2️⃣ Mover certificado y llave a la ubicación correcta
📌 Ubicación estándar de SSL en Nginx: /etc/nginx/ssl/

# Crear el directorio
sudo mkdir -p /etc/nginx/ssl

# Mover archivos
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/

# Ajustar permisos
sudo chmod 600 /etc/nginx/ssl/nautilus.key
sudo chmod 644 /etc/nginx/ssl/nautilus.crt

3️⃣ Configurar Nginx para HTTPS
Edita el archivo principal de configuración:

sudo vi /etc/nginx/nginx.conf
Busca un bloque server y asegúrate de que exista uno como este (o agrégalo sin borrar los demás):

server {
    listen 443 ssl;
    server_name _;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;
}
💡 Nota: No elimines otros bloques server; solo asegúrate de que este esté presente.

4️⃣ Crear el archivo index.html
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html

# Verificar contenido
cat /usr/share/nginx/html/index.html

5️⃣ Validar configuración y reiniciar Nginx
# Validar sintaxis
sudo nginx -t

# Salida esperada:
# syntax is ok
# test is successful

# Reiniciar servicio
sudo systemctl restart nginx
✅ Resultado final
Nginx instalado y activo

HTTPS habilitado con certificado SSL

Página accesible desde el puerto 443

index.html servido correctamente
