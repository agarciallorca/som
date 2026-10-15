# PRÁCTICA: Creación y configuración de máquinas virtuales en VirtualBox

---

## 1. Introducción

Una máquina virtual es un ordenador simulado por software que funciona dentro de otro ordenador. Al ordenador real lo llamamos **anfitrión** y al sistema que funciona dentro de la máquina virtual, **invitado**. VirtualBox es el programa que reparte los recursos del anfitrión (procesador, memoria, disco y red) entre las máquinas virtuales.

En esta práctica aprenderás a crear una máquina virtual y a modificar su configuración, igual que harías con un ordenador real: cambiar sus discos, el orden de arranque, la memoria y los procesadores, y la conexión de red. Después compartirás archivos con el equipo anfitrión y, para terminar, aprenderás a reparar dos errores muy habituales de VirtualBox.

**Material necesario:** VirtualBox 7.x, una imagen ISO de Debian 13 y unos 10 GB libres en el disco D:.

> **Cómo se entrega:** cada vez que veas 📸 haz una captura de pantalla, y cada vez que veas ❓ responde a la pregunta con tus propias palabras. Todo se entregará en un **único documento de Writer**.

---

## Ejercicio 1. Crear una máquina virtual

Crear una máquina virtual consiste en decidir qué "hardware" tendrá: cuánta memoria, cuántos procesadores y qué tamaño de disco. En esta práctica no nos interesa el proceso de instalación del sistema operativo, así que dejaremos que VirtualBox lo haga solo (*instalación desatendida*).

1. Abre VirtualBox y pulsa **Nueva**.
2. Configura la máquina:
3. En el primer bloque:
- Nombre: `Debian 13`
- Ruta: `D:\VIRTUALBOX_VMS\SOM_XXX`
- Selecciona la imagen ISO: `debian-13.7.0-amd64-DVD-1`
- **Marca** la casilla de *proceder con la instalación desatendida*.
3. En el siguiente bloque:
- Usuario: tu nombre de pila
- Contraseña: `1234`
- Nombre de equipo (Host Name): `deb-xxx`
- Nombre de dominio (Domain Name): `som.local`
- Marca **Install Guest Additions**.
4. En el siguiente bloque asigna **2048 MB** de memoria y **2 procesadores**.
5. Por último crea un disco duro virtual de **50 GB**, formato **VDI** y de reserva **dinámica** (**NO** marques Reservar completamente).
6. Finaliza el asistente. La instalación tarda unos 10-20 minutos y la máquina se reiniciará sola. Cuando aparezca el escritorio, inicia sesión con tu usuario.
7. Por comodidad puedes poner el idioma en *Español* desde los **Ajustes** y también cambiar la distribución de teclado.

### A entregar en el documento ###
📸 **Captura 1.** Escritorio del sistema invitado funcionando.

❓ **1.1.** ¿Qué diferencia hay entre un disco de reserva **dinámica** y uno de **tamaño fijo**?

❓ **1.2.** Busca el archivo `.vdi` en el anfitrión. ¿Cuánto ocupa? ¿Por qué no ocupa los 25 GB?

---

## Ejercicio 2. Añadir y quitar discos virtuales

Ampliar el almacenamiento en una máquina virtual es como instalar un disco nuevo en un ordenador real, pero mucho más fácil: el disco es solo un archivo del anfitrión. Estos cambios se hacen con la máquina **apagada**.

1. Apaga el invitado desde su menú y abre **Configuración → Almacenamiento**.
2. Pulsa el icono de **añadir disco duro** junto al controlador SATA, elige **Crear** y genera un disco VDI de **5 GB** llamado `Datos`.
3. Arranca la máquina. Abre la aplicación **Discos** y comprueba que aparece un disco nuevo de 5 GB sin formato.
4. En **Discos**, formatea el disco nuevo (ext4) y móntalo. Crea dentro un archivo de texto llamado `prueba.txt`.
5. Apaga la máquina y quita el disco en **Configuración → Almacenamiento**. Arranca de nuevo y comprueba que el disco ya no aparece.

### A entregar en el documento ###
📸 **Captura 2.** La aplicación Discos mostrando el disco de 5 GB formateado.

❓ **2.1.** Después de quitar el disco de la máquina, ¿el archivo `Datos.vdi` se ha borrado? ¿Dónde puedes comprobarlo?

❓ **2.2.** ¿Qué diferencia hay entre **quitar** un disco de la máquina y **eliminar** su archivo?

---

## Ejercicio 3. Modificar la secuencia de arranque

Al encender un ordenador, el firmware (BIOS/UEFI) busca un dispositivo del que arrancar siguiendo un orden de prioridad. Cambiar ese orden permite, por ejemplo, arrancar desde un instalador o un sistema "Live" en lugar del sistema instalado.

1. Apaga la máquina y abre **Configuración → Sistema → Placa base**. Anota el **orden de arranque** actual.
2. En **Almacenamiento**, inserta la imagen ISO en la unidad óptica (selecciona la unidad y elige el archivo en el desplegable de la derecha).
3. **Prueba 1.** Pon el **disco duro** en primera posición y arranca. Anota qué sistema se inicia.
4. **Prueba 2.** Apaga, pon la **unidad óptica** en primera posición y arranca. Cuando aparezca el menú de la ISO, elige probar el sistema **sin instalar**.
5. Apaga y deja de nuevo el disco duro en primera posición. Retira la ISO de la unidad óptica.

### A entregar en el documento ###
📸 **Captura 3.** Pantalla del orden de arranque con el disco duro en primera posición.

📸 **Captura 4.** El sistema arrancado en modo *Live* desde la ISO (prueba 2).

❓ **3.1.** ¿Por qué, con la ISO insertada y el disco duro en primer lugar, el sistema arranca desde el disco?

❓ **3.2.** Un compañero ha instalado un sistema, pero al reiniciar vuelve a aparecer el instalador. ¿Cómo lo solucionarías?

---

## Ejercicio 4. Modificar los recursos hardware

Una ventaja de la virtualización es que se puede cambiar el hardware con unos pocos clics. Si a una máquina le falta memoria, basta con apagarla, modificar la configuración y volver a arrancarla.

1. Con la máquina arrancada, abre una terminal y ejecuta estos dos comandos. Anota los resultados en la tabla.

   ```bash
   free -h    # memoria RAM
   nproc      # número de procesadores
   ```

2. Apaga la máquina y, en **Configuración → Sistema**, cambia la memoria a **3072 MB** y los procesadores a **4**. Si tu equipo no puede asignar esa memoria sin entrar en la zona roja del control deslizante, elige un valor distinto.
3. Arranca de nuevo y repite los dos comandos.
4. Vuelve a dejar la máquina con 2048 MB y 2 procesadores.

### A entregar en el documento ###
| Recurso | Antes del cambio | Después del cambio |
|---|---|---|
| Memoria RAM | | |
| Procesadores | | |

📸 **Captura 5.** Configuración de VirtualBox con los nuevos valores, junto con el resultado de `free -h` y `nproc`.

❓ **4.1.** ¿Por qué no conviene asignar a una máquina virtual toda la memoria y todos los procesadores del anfitrión?

❓ **4.2.** Con la máquina encendida, ¿qué opciones de **Sistema** aparecen deshabilitadas? ¿Por qué crees que es así?

---

## Ejercicio 5. Configurar las opciones de red

La tarjeta de red de una máquina virtual puede conectarse a "redes" distintas, y de eso depende si la máquina tiene Internet o si el anfitrión puede comunicarse con ella. En esta práctica probarás tres modos:

- **NAT:** la máquina sale a Internet a través del anfitrión, como si estuviera detrás de un router. Es el modo por defecto.
- **Adaptador puente:** la máquina se conecta directamente a la red física del anfitrión, como un equipo más.
- **Red interna:** la máquina solo se comunica con otras máquinas virtuales de la misma red interna; queda aislada del anfitrión y de Internet.

Para cada modo, apaga la máquina, abre **Configuración → Red → Adaptador 1**, cambia el modo, arranca y comprueba en el invitado si puedes navegar con **Mozilla Firefox** (p.e. intenta acceder a Aules) y la dirección IP asignada con el siguiente comando:

```bash
ip a                     # ¿tiene dirección IP?
```

En modo **adaptador puente** selecciona la interfaz de red física del anfitrión (cable o Wi-Fi). En modo **red interna** deja el nombre por defecto (`intnet`). Si en algún modo la máquina no obtiene dirección IP, anótalo en la tabla.

| Modo de red | ¿Tiene IP? ¿Cuál? | ¿Hay Internet? |
|---|---|---|
| NAT | | |
| Adaptador puente | | |
| Red interna | | |

📸 **Captura 6.** Resultado de `ip a` y navegación con Firefox en el modo adaptador puente.

❓ **5.1.** En red interna, ¿qué ocurre con la dirección IP y con el ping? ¿A qué crees que se debe?

❓ **5.2.** ¿Qué modo elegirías para cada caso? Justifica la respuesta.
   - Una máquina de pruebas que solo necesita descargar actualizaciones.
   - Una máquina que actúa como servidor al que deben acceder otros ordenadores del aula.

Cuando termines, deja el adaptador en modo **NAT**.

---

## Ejercicio 6. Compartir archivos entre el invitado y el anfitrión

Las **carpetas compartidas** permiten que una carpeta del anfitrión aparezca también dentro del invitado. Para ello el invitado necesita las **Guest Additions**. Como marcaste su instalación en el ejercicio 1, deberían estar ya instaladas: compruébalo con este comando, que debe devolver al menos una línea.

```bash
lsmod | grep vboxguest
```

1. En el anfitrión, crea una carpeta llamada `Compartida` en el directorio `D:\VIRTUALBOX_VMS\SOM_XXX`.
2. Con la máquina apagada, abre **Configuración → Carpetas compartidas**, pulsa el icono de añadir y selecciona esa carpeta. Marca **Automontar** y establece el punto de montaje a `/media/compartida`.
3. Arranca la máquina. Para tener permisos sobre la carpeta, añade tu usuario al grupo `vboxsf`, actualiza el grupo, cierra sesión y vuelve a entrar:

   ```bash
   sudo usermod -aG vboxsf $USER
   newgrp vboxsf
   ```

4. La carpeta aparecerá en `/media/sf_Compartida`. Crea un archivo `desde_anfitrion.txt` en el anfitrión y otro `desde_invitado.txt` en el invitado. Comprueba que ambos se ven desde los dos lados.

📸 **Captura 7.** Explorador de archivos del invitado mostrando la carpeta compartida con los dos archivos.

❓ **6.1.** ¿Dónde se guardan realmente los archivos de la carpeta compartida: en el disco virtual o en el disco del anfitrión? ¿Qué pasaría con ellos si eliminaras la máquina virtual?

---

## Ejercicio 7. Resolver errores típicos de VirtualBox

VirtualBox no guarda los discos ni las máquinas "dentro" del programa: lo que guarda es un registro con la **ruta** de cada archivo. Si mueves o renombras archivos desde el explorador de archivos sin que VirtualBox lo sepa, la ruta guardada deja de ser válida y aparecen errores. En este ejercicio vas a provocar dos de los más frecuentes, de forma controlada, y a repararlos.

### Parte A. Disco inaccesible

1. Con la máquina apagada, vuelve a conectar el disco `Datos.vdi` del ejercicio 2: en **Configuración → Almacenamiento** pulsa añadir disco duro, elige **Elegir un disco existente** y selecciona el archivo. (Si ya no lo tienes, crea uno nuevo de 1 GB).
2. Cierra VirtualBox por completo. En el explorador de archivos del anfitrión, **mueve** `Datos.vdi` a otra carpeta, por ejemplo el Escritorio.
3. Abre VirtualBox e intenta arrancar la máquina. Aparecerá un mensaje de error que indica que no se puede abrir el disco (suele mencionar que no se encuentra el archivo o el código `VERR_FILE_NOT_FOUND`). Anota el mensaje.
4. Repáralo: abre **Configuración → Almacenamiento**, donde el disco perdido aparece marcado con un aviso. Selecciónalo y quítalo. Después vuelve a añadirlo con **Elegir un disco existente**, indicando su **nueva ubicación**. Si en el **Administrador de medios virtuales** sigue apareciendo la entrada antigua con un aviso, selecciónala y pulsa **Quitar**.
5. Arranca la máquina y comprueba que ya lo hace sin errores.

📸 **Captura 8.** El mensaje de error al intentar arrancar con el disco movido.

### Parte B. Máquina inaccesible por moverla de carpeta

1. Apaga la máquina y cierra VirtualBox por completo.
2. En el explorador de archivos, **mueve la carpeta entera de la máquina** (`Debian 13`, que contiene el archivo `.vbox` y el disco `.vdi`) a otra ubicación, por ejemplo Documentos.
3. Abre VirtualBox. La máquina aparecerá marcada como **Inaccesible**, con un icono de aviso, y no podrás iniciarla.
4. Repárala:
   - Haz clic derecho sobre la máquina y elige **Quitar**. En la ventana que aparece elige **Solo quitar**. **No elijas eliminar todos los archivos**, porque borrarías la máquina de verdad.
   - Ve a **Máquina → Añadir** y selecciona el archivo `.vbox` en su nueva ubicación.
   - Arranca la máquina. Como el disco del sistema está dentro de su carpeta, VirtualBox lo encuentra sin más cambios.
5. Para terminar, vuelve a dejar la máquina en su sitio de la forma correcta: con la opción **Mover** del menú de la máquina (clic derecho sobre ella). Así VirtualBox actualiza él mismo todas las rutas y no hay errores.

📸 **Captura 9.** La máquina marcada como **Inaccesible** en el listado de VirtualBox.

❓ **7.1.** ¿Por qué VirtualBox no encuentra el disco o la máquina cuando los mueves desde el explorador de archivos?

❓ **7.2.** ¿Qué diferencia hay entre **Solo quitar** una máquina y eliminar todos sus archivos?

### Otros errores frecuentes

Estos son otros problemas que te encontrarás a menudo. Todos ellos tienen solución con lo que has aprendido en esta práctica:

| Síntoma | Causa probable | Solución |
|---|---|---|
| `FATAL: No bootable medium found! System halted.` | No hay ninguna ISO ni disco con sistema en el orden de arranque, o el disco no está conectado a la máquina | Revisar el orden de arranque y que el disco esté conectado en **Almacenamiento** (ejercicios 2 y 3) |
| La máquina no tiene Internet | Modo de red equivocado, o la casilla *Cable conectado* está desmarcada | **Red → Adaptador 1**: comprobar el modo y, en **Avanzadas**, que *Cable conectado* esté marcado (ejercicio 5) |
| La carpeta compartida no se ve o da "permiso denegado" | El usuario no pertenece al grupo `vboxsf` o no se ha reiniciado la sesión | `sudo usermod -aG vboxsf $USER`, `newgrp vboxsf` y volver a iniciar sesión (ejercicio 6) |
| Error de que VT-x o AMD-V no está disponible al arrancar | La virtualización está desactivada en la BIOS/UEFI del anfitrión | Activarla en la BIOS/UEFI del anfitrión (opciones tipo *Intel Virtualization Technology* o *SVM Mode*); avisa al profesor |

---

## 7. Entrega

Entrega **un único documento** con tus datos, las **9 capturas** numeradas, las **respuestas** a las preguntas, las **dos tablas** completadas (ejercicios 4 y 5) y unas líneas finales explicando qué te ha resultado más difícil.

## 8. Criterios de evaluación

| Aspecto | Peso |
|---|---|
| Máquina virtual creada y funcionando (ejercicio 1) | 10 % |
| Gestión de discos virtuales (ejercicio 2) | 15 % |
| Secuencia de arranque (ejercicio 3) | 10 % |
| Recursos hardware y tabla (ejercicio 4) | 15 % |
| Configuración de red y tabla (ejercicio 5) | 20 % |
| Carpeta compartida funcionando (ejercicio 6) | 10 % |
| Reparación de errores (ejercicio 7) | 10 % |
| Respuestas y presentación del documento | 10 % |
