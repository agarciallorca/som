# 🌐 Práctica: Despliegue de servidor web y gestión de permisos

**Objetivo:** Instalar el servidor web Apache2, crear un sitio web personalizado y entender cómo afectan los permisos de Linux a la visibilidad de una web en internet.

---

## 🛠️ Tarea 1: Instalación del Servidor (El Entorno)

Antes de publicar nada, necesitamos que nuestra máquina Debian sea capaz de "servir" contenido web.

1.  **Actualiza los repositorios:**
    ```bash
    sudo apt update
    ```
2.  **Instala el paquete Apache2:**
    ```bash
    sudo apt install apache2 -y
    ```
3.  **Verificación:** Abre el navegador de tu Debian y escribe `localhost` en la barra de direcciones. 
    * ¿Ves la página por defecto de Debian? **[ SI / NO ]**

---

## ✍️ Tarea 2: Creación de tu Contenido (En Local)

Vamos a trabajar primero en nuestra carpeta personal para luego "subir" el trabajo al servidor.

1.  **Crea una carpeta de proyecto:**
    ```bash
    mkdir ~/mi_web
    cd ~/mi_web
    ```
2.  **Crea tu página de inicio:** Usa el editor `nano` para crear un archivo llamado `index.html`.
    ```bash
    nano index.html
    ```
3.  **Escribe el código HTML:** (Copia y pega esto, cambiando el nombre).
    ```html
    <html>
      <body>
        <h1>🚀 Servidor de: [TU NOMBRE]</h1>
        <p>Esta página ha sido configurada desde la terminal de Linux.</p>
      </body>
    </html>
    ```
    *(Pulsa `Ctrl+O` para guardar y `Ctrl+X` para salir)*.

---

## 🏗️ Tarea 3: Publicación y Conflicto de Permisos

El servidor web busca los archivos en la ruta: `/var/www/html/`. Vamos a mover nuestra web allí.

1.  **Limpia el servidor:** Borra la página por defecto de Debian (necesitarás sudo).
    ```bash
    sudo rm /var/www/html/index.html
    ```
2.  **Mueve tu archivo:**
    ```bash
    sudo mv ~/mi_web/index.html /var/www/html/
    ```
3.  **El problema de los permisos:** Por defecto, al mover un archivo con `sudo`, el dueño puede cambiar o los permisos pueden ser restrictivos.
    * Comprueba los permisos actuales:
        ```bash
        ls -l /var/log/apache2/error.log  # (Opcional: para ver si hay errores)
        ls -l /var/www/html/index.html
        ```

---

## 🔐 Tarea 4: Asegurando el Acceso (Lectura para el Mundo)

Si los permisos no son correctos, el navegador mostrará un error **"403 Forbidden"**.

1.  **Asigna el dueño correcto:** El servidor web en Debian usa el usuario `www-data`.
    ```bash
    sudo chown www-data:www-data /var/www/html/index.html
    ```
2.  **Aplica permisos estándar:** Queremos que el dueño escriba, pero que el resto solo pueda leer.
    ```bash
    sudo chmod 644 /var/www/html/index.html
    ```
3.  **Verificación Final:** * Desde tu máquina: Abre `localhost` en el navegador.
    * Desde la máquina de un compañero: Pon la IP de tu servidor (búscala con `ip a`).

---

## ❓ Cuestionario de Control

1.  ¿Qué sucede si le quitas el permiso de lectura a `otros` (`chmod 640`) e intentas ver la web desde otro PC?
2.  ¿En qué carpeta se guardan los archivos que el servidor Apache muestra al mundo?
3.  ¿Por qué es necesario usar `sudo` para mover archivos a `/var/www/html/`?

---

**ENTREGA:** Captura de pantalla de tu navegador mostrando tu página personalizada con la IP de tu máquina visible.
