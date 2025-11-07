# PRÁCTICA: CLONADO Y RESTAURACIÓN DE SISTEMAS CON CLONEZILLA

## 1. ¿QUÉ ES CLONEZILLA?

### Definición

**Clonezilla** es un software libre y gratuito de clonación y restauración de discos y particiones. Funciona de manera similar a Norton Ghost o Acronis True Image, pero es completamente gratuito y de código abierto.

### Características principales

#### Ventajas
✓ **Gratuito y de código abierto**\
✓ **Soporta múltiples sistemas de archivos:** ext2, ext3, ext4, FAT, NTFS, HFS+, etc.\
✓ **Clona solo bloques usados** (ahorra espacio y tiempo)\
✓ **Compresión de imágenes** para ahorrar espacio\
✓ **Diferentes modos de clonación:** disco a disco, disco a imagen\
✓ **Multicast** para clonar múltiples equipos simultáneamente\
✓ **Arranque desde USB o CD/DVD**

#### Limitaciones
✗ Interfaz en modo texto (puede resultar intimidante al principio)\
✗ No permite operaciones en caliente (el sistema debe estar apagado)\
✗ Requiere conocimientos básicos de particiones y sistemas de archivos

### Versiones de Clonezilla

#### Clonezilla Live
- **Uso:** Un solo equipo
- **Distribución:** ISO para CD/DVD/USB
- **Ideal para:** Usuarios domésticos, técnicos, laboratorios pequeños

#### Clonezilla SE (Server Edition)
- **Uso:** Múltiples equipos simultáneamente (multicast)
- **Distribución:** Servidor dedicado
- **Ideal para:** Aulas de informática, empresas grandes

**En esta práctica usaremos Clonezilla Live**

### ¿Cuándo usar Clonezilla?

- **Copias de seguridad completas** del sistema
- **Migración de sistemas** a discos nuevos
- **Despliegue masivo** de sistemas operativos
- **Recuperación ante desastres**
- **Clonación de laboratorios** informáticos
- **Actualización de hardware** (disco duro a SSD)

---

## 2. PREPARACIÓN DEL ENTORNO

### Escenario de práctica

Para esta práctica utilizaremos **VirtualBox** con el siguiente esquema:

![Esquema de la práctica](../img/Esquema_practica_clonezilla.png)

---

## 3. DESCARGA E INSTALACIÓN DE CLONEZILLA

### Paso 1: Descargar Clonezilla Live

Descarga la ISO de Clonezilla del servidor de aula

### Paso 2: Montar ISO en VirtualBox

#### En la máquina origen
1. Con la VM apagada, ve a **Configuración → Almacenamiento**
2. Haz clic en el icono de CD (vacío)
3. En el menú de la derecha, haz clic en el icono de CD
4. Selecciona **Elegir archivo de disco**
5. Busca y selecciona la ISO de Clonezilla
6. Acepta los cambios

### Paso 3: Configurar orden de arranque

1. En VirtualBox: **Configuración → Sistema → Orden de arranque**
2. Asegúrate de que **Óptico** está antes que **Disco duro**
3. O usa el **menú de arranque** (F12 durante el inicio de la VM)

---

## 4. PRÁCTICA 1: CLONAR DISCO/PARTICIÓN A IMAGEN

### Objetivo
Crear una imagen de respaldo del disco completo de nuestra máquina virtual.

### Paso 2: Arrancar Clonezilla

1. **Inicia la máquina virtual**
   - Debería arrancar desde la ISO de Clonezilla

2. **Primera pantalla: Selección de idioma**
   - Se muestra el menú de arranque de Clonezilla
   - Espera 30 segundos o presiona Enter para la opción por defecto
   - Opción recomendada: **Clonezilla live (Default settings, VGA 800x600)**

3. **Seleccionar idioma**
   - Usa las flechas del teclado y selecciona **Español** o **English** (según prefieras)

4. **Seleccionar distribución de teclado**
   - Selecciona **Don't touch keymap** (no cambiar distribución) o elige tu distribución específica

5. **Iniciar Clonezilla**
   - Elige la opción "Start Clonezilla"

### Paso 3: Modo de Clonezilla

Como queremos crear la imagen del disco de la máquina elegiremos la opción `device-image` (disco/partición a imagen)

### Paso 4: Ubicación para guardar la imagen

Clonezilla nos pregunta dónde guardar la imagen. En nuestro caso vamos a utilizar el disco local (disco externo simulado) que hemos conectado en el proceso de configuración de la máquina virtual de origen. Por lo tanto seleccionamos la opción `local_dev` (dispositivo local).

### Paso 5: Montar dispositivo de almacenamiento

1. **Insertar dispositivo**
   - El sistema pide que insertes el USB/disco externo donde guardar la imagen. Como ya lo tenemos conectado previamente, no debemos hacer nada.
   - Presiona **Enter** cuando esté listo

2. **Espera a que detecte los dispositivos**
   - Clonezilla buscará dispositivos disponibles
   - Aparecerá una lista de particiones disponibles

3. **Seleccionar partición de destino**
   - Verás algo como:
     ```
     sda1  vfat  500M
     sda2  ext4  19.5G  ← (tu disco principal)
     sdb1  ntfs  128G   ← (disco externo adicional)
     ```
   - **Selecciona** la partición correspondiente al disco externo. En este ejemplo será `sdb1`
   - **Presiona:** Enter

4. **Confirmar directorio**
   - Clonezilla montará la partición
   - Preguntará el directorio donde guardar las imágenes
   - Por defecto sugiere la raíz: `/home/partimag`
   - **Presiona:** Enter para aceptar o escribe una ruta personalizada

5. **Verificación**
   - Mostrará información sobre el espacio disponible
   - **Presiona:** Enter para continuar

### Paso 6: Modo de operación

Para esta práctica utilizaremos el modo `Beginner` (modo principiante).

### Paso 7: Tipo de clonación

Como queremos hacer la imagen del disco completo seleccionaremos la opción `savedisk` (guardar disco completo como imagen). 

**Nota:** También podrías usar `saveparts` si solo quieres clonar una partición específica.

### Paso 8: Nombre de la imagen

Se pedirá un nombre para la imagen. Escribe por ejemplo `img-maquina1-aaaa-mm-dd` (siendo aaaa el año, mm el mes y dd el día de la fecha de realización de la imagen) y pulsa Enter.

### Paso 8: Seleccionar disco origen

Aparecerá una lista de discos disponibles. En nuestro caso sólo aparecerá el disco sda, que es el disco principal de la máquina de origen. Usa **barra espaciadora** para marcar/desmarcar el disco y preseiona Enter.

### Paso 9: Verificar sistema de archivos

Clonezilla nos pregunta si queremos verificar el sistema de archivos del disco de origen antes de realizar la imagen. Nosotros elegiremos la opción `-sfsck` para omitir este paso.

**Nota:** Si seleccionamos la opción `-fsck-src-part` (verificar sistema de archivos) nos asegura que no hay errores antes de clonar. Esto es interesante en entornos reales de trabajo.

### Paso 10: Verificar imagen guardada

A continuación podemos hacer que Clonezilla verifique la imagen después de guardarla. Seleccionamos la opción `-scs` para omitir esta comprobación.

**Nota:**: Como en el caso anterior, en entornos reales de trabajo es interesante verificar la imagen después de guardarla. Para ello seleccionaríamos la opción `-sc`.

### Paso 11: Acción después de finalizar

En este paso seleccionamos lo que queremos que haga Clonezilla al terminar el proceso de generación de la imagen. Hay que tener en cuenta que el proceso puede ser largo si el disco duro de origen contiene mucha información. Nosotros seleccionaremos la opción `-p poweroff` para que la máquina se apague cuando finalice el proceso.

### Paso 12: Confirmar y ejecutar

1. **Resumen de operación**
   - Clonezilla mostrará un resumen de la operación
   - Revisa cuidadosamente:
     - Disco origen
     - Ubicación destino
     - Nombre de imagen
     - Opciones seleccionadas

2. **Confirmación**
   - Escribe Y y presiona Enter.

### Paso 13: Proceso de clonación

1. **Verificación del sistema de archivos** (si hemos seleccionado esta opción)
   - Clonezilla verificará el sistema de archivos origen
   - Mostrará el progreso

2. **Clonación en progreso**
   - Verás una barra de progreso
   - Información mostrada:
     ```
     Current  rate: XXX MB/min
     Avg. rate: XXX MB/min
     Elapsed time: XX:XX:XX
     Remaining time: XX:XX:XX
     ```

3. **Compresión**
   - Los datos se comprimen automáticamente
   - Reduce el tamaño de la imagen

4. **Verificación** (si hemos seleccionado esta opción)
   - Al terminar la clonación, verifica la integridad
   - Puede tardar algunos minutos adicionales

5. **Finalización**
   - Mensaje: "The disk or partition image was saved successfully!"
   - **Presiona:** Enter

### Paso 14: Acción posterior

La máquina se apagará automáticamente después de un tiempo de espera, ya que seleccionamos la opción `poweroff` anteriormente.

### Resultado esperado

En el disco externo simulado deberías tener una carpeta llamada `img-maquina1-aaaa-mm-dd` con los ficheros que componen la imagen del disco completo.
