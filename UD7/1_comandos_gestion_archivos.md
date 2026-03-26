# Comandos de gestión de archivos en Linux

## 1. Repaso: operaciones básicas
En Linux, "todo es un archivo". Antes de avanzar, recuerda los comandos esenciales de manipulación. **Nota:** Bash distingue entre mayúsculas y minúsculas (`Archivo.txt` no es lo mismo que `archivo.txt`).

| Comando | Acción | Ejemplo |
| :--- | :--- | :--- |
| `cd` | Cambiar a un directorio | `cd /etc` |
| `pwd` | **P**rint **W**orking **D**irectory: ¿Dónde estoy? | `pwd` |
| `ls -lh` | Listar archivos (**l**: formato largo, **h**: tamaño humano) | `ls -lh /var/log` |
| `cp` | Copiar archivos o carpetas (usa `-r` para carpetas) | `cp nota.txt nota_bak.txt` |
| `mv` | Mover o **renombrar** un archivo | `mv archivo.txt documentos/` |
| `rm` | Eliminar (¡Cuidado! No hay papelera de reciclaje) | `rm -rf carpeta_vieja` |
| `mkdir` | Crear una carpeta (`-p` para crear rutas completas) | `mkdir -p practicas/linux` |

---

## 2. Localización de archivos: comando `find`
Mientras que `ls` se utiliza para listar el contenido de un directorio concreto, `find` es un motor de búsqueda que rastrea de forma recursiva todo el árbol de directorios para localizar archivos que cumplan condiciones específicas.

**Estructura:** `find [ruta] [opciones] [valor]`

* **Por nombre:** `find /etc -name "*.conf"` (Busca archivos .conf en /etc).
* **Por tamaño:** `find /var/log -size +50M` (Archivos mayores de 50MB).
* **Por usuario:** `find /home -user alumno` (Archivos que pertenecen a 'alumno').
* **Silenciando errores:** Al buscar en carpetas del sistema, verás muchos errores de "Permiso denegado". Para limpiar la pantalla, redirige los errores al "agujero negro" de Linux, el fichero `/dev/null`:
  * `find / -name "secreto.txt" 2>/dev/null`

---

## 3. Lectura inteligente: head, tail y wc
Para leer archivos cortos usamos `cat` (ver todo) o `nano` (editar). Sin embargo, en servidores, los archivos de Log pueden pesar **Gigabytes**.

> **¡Ojo!:** Intentar abrir un log de 2GB con `cat` o `nano` puede bloquear tu terminal o saturar la memoria RAM del servidor. Para archivos grandes, usa "muestreo":

### `head`
Muestra el principio del archivo. Útil para leer cabeceras o versiones.
* `head -n 15 archivo.txt` (Muestra las primeras 15 líneas).

### `tail`
Muestra el final del archivo. Es la herramienta principal para ver lo más reciente.
* `tail -n 10 /var/log/syslog` (Muestra los últimos 10 eventos del sistema).
* **Monitorizar un fichero en tiempo real (`tail -f`):** Mantiene el archivo abierto. Si el sistema escribe algo nuevo, aparece en tu pantalla al instante. **Imprescindible para monitorizar servidores.**
  * `sudo tail -f /var/log/apache2/access.log`

### 📍 `wc`
Cuenta líneas, palabras o caracteres. Se usa mucho con tuberías (`|`).
* `wc -l archivo.txt` (Cuenta cuántas líneas tiene el archivo).

---

## 4. Filtrado de contenido: `grep`
`grep` es un buscador de texto. Es como hacer un `Ctrl + F` en un documento, pero desde la terminal.

* **Básico:** `grep "error" /var/log/syslog`
* **Ignorar mayúsculas (`-i`):** `grep -i "ERROR" archivo.log`
* **Invertir búsqueda (`-v`):** Muestra las líneas que **NO** contienen la palabra. Ideal para limpiar comentarios:
  * `grep -v "^#" /etc/fstab` (Muestra el archivo ocultando las líneas que empiezan por `#`).

---

## 5. Tuberías (`|`)
La tubería conecta comandos: la salida del primero es la entrada del segundo. En Linux, esto nos permite procesar texto plano de forma infinita.

**Ejemplos Reales:**
1. **Contar cuántos archivos hay en una carpeta:**
   `ls /usr/bin | wc -l`
2. **Buscar un error específico en las últimas líneas de un log:**
   `tail -n 100 /var/log/syslog | grep -i "usb"`
3. **Saber si el servidor Apache está instalado (en el listado de paquetes):**
   `dpkg -l | grep "apache2"`

---

## Ejercicios
1.  **Búsqueda pesada:** Busca en todo el disco archivos de más de 100MB y oculta los errores de "Permiso denegado".
2.  **Monitorización:** Deja la pantalla "escuchando" los nuevos mensajes del sistema en el archivo `/var/log/syslog`.
3.  **Filtrado de usuarios:** El archivo `/etc/passwd` contiene todos los usuarios. Muestra solo las líneas que contengan tu nombre de usuario.
4.  **Limpieza de config:** Muestra el archivo `/etc/ssh/sshd_config` saltándote todas las líneas que sean comentarios (que empiezan por `#`).
5.  **Contador de errores:** Cuenta cuántas veces aparece la palabra "Failed" en el archivo `/var/log/auth.log`.
6.  **Contador de logs:** ¿Cómo podrías saber cuántos archivos con extensión `.log` existen dentro de la carpeta `/var/log`?
7.  **El Sándwich (Nivel 1):** Extrae únicamente la **línea número 15** de un archivo de texto largo.
8.  **El Sándwich (Nivel 2):** Extrae las líneas de la **20 a la 25** de un archivo (un total de 6 líneas).
9.  **Listado selectivo:** Lista el contenido de `/usr/bin` y cuenta cuántos comandos empiezan por la letra "z".
10.  **Rastreo de logs:** Busca en los últimos 50 eventos de `/var/log/syslog` si aparece la palabra "kernel".
11. **Seguridad:** Busca todos los archivos que pertenezcan al usuario `root` dentro de la carpeta `/home` de un usuario normal.
12. **Inventario:** ¿Cómo podrías saber cuántos archivos con extensión `.conf` hay en el directorio `/etc` y todas sus subcarpetas?
13. **Análisis de rendimiento:** Si un log ocupa 5GB, ¿qué comando usarías para ver solo las primeras 20 líneas y cuál para ver las 20 últimas? ¿Por qué no usarías `cat`?
