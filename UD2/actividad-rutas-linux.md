# ACTIVIDAD PRÁCTICA: RUTAS ABSOLUTAS Y RELATIVAS EN ARCH LINUX

## Objetivos de la Actividad
- Comprender la diferencia entre rutas absolutas y relativas
- Practicar la navegación por el sistema de archivos de Linux
- Dominar los comandos básicos de gestión de archivos y directorios
- Desarrollar habilidades para moverse eficientemente por la estructura de directorios

---

## PARTE 1: CONCEPTOS BÁSICOS

### ¿Qué es una ruta?
Una **ruta** (o path) es la ubicación de un archivo o directorio en el sistema de archivos.

### Ruta Absoluta
- Siempre comienza desde la **raíz del sistema** (/)
- Especifica la ubicación completa desde el directorio raíz
- **No depende** de dónde estés ubicado actualmente
- Ejemplos:
  - `/home/alumno/documentos`
  - `/etc/hostname`
  - `/usr/bin/ls`

### Ruta Relativa
- Comienza desde el **directorio actual** donde te encuentras
- **Depende** de tu ubicación actual
- Símbolos especiales:
  - `.` = directorio actual
  - `..` = directorio padre (un nivel arriba)
  - `~` = directorio home del usuario
- Ejemplos (si estás en `/home/alumno`):
  - `documentos` (subcarpeta del directorio actual)
  - `../otro_usuario` (sube un nivel y entra en otro_usuario)
  - `./archivo.txt` (archivo en el directorio actual)

---

## PARTE 2: PREPARACIÓN DEL ENTORNO

### Paso 1: Crear la estructura de directorios

Abre una terminal y ejecuta los siguientes comandos para crear la estructura con la que trabajaremos:

```bash
cd ~
mkdir -p proyecto_so/documentos
mkdir -p proyecto_so/imagenes
mkdir -p proyecto_so/scripts
mkdir -p proyecto_so/backups
mkdir -p proyecto_so/documentos/apuntes
mkdir -p proyecto_so/documentos/ejercicios
mkdir temporal
```

### Paso 2: Crear archivos de prueba

```bash
cd ~/proyecto_so/documentos
nano bienvenida.txt
```
Escribe: "Este es el archivo de bienvenida" y guarda (Ctrl+O, Enter, Ctrl+X)

```bash
nano apuntes/tema1.txt
```
Escribe: "Apuntes del tema 1: Sistemas Operativos" y guarda

```bash
nano ejercicios/practica1.txt
```
Escribe: "Ejercicio 1: Práctica con rutas" y guarda

```bash
cd ~/proyecto_so/scripts
nano script_ejemplo.sh
```
Escribe: "#!/bin/bash" y guarda

```bash
cd ~/temporal
nano notas.txt
```
Escribe: "Archivo temporal de notas" y guarda

---

## PARTE 3: EJERCICIOS PRÁCTICOS

### 🎯 **EJERCICIO 1: Navegación Básica**

**Situación inicial:** Estás en tu directorio home (`~`)

Realiza las siguientes tareas y anota el comando que utilizas:

1. Muestra el contenido del directorio `proyecto_so` usando **ruta relativa**
   - Comando: ________________

2. Muestra el contenido del directorio `proyecto_so` usando **ruta absoluta**
   - Comando: ________________

3. Entra en el directorio `proyecto_so/documentos` usando **ruta relativa**
   - Comando: ________________

4. Vuelve a tu directorio home usando el símbolo especial
   - Comando: ________________

5. Entra en el directorio `proyecto_so/scripts` usando **ruta absoluta**
   - Comando: ________________

---

### 🎯 **EJERCICIO 2: Visualización de Archivos**

**Situación inicial:** Estás en `~/proyecto_so/scripts`

1. Visualiza el contenido de `bienvenida.txt` usando **ruta relativa**
   - Comando: ________________

2. Visualiza el contenido de `tema1.txt` usando **ruta relativa**
   - Comando: ________________

3. Visualiza el contenido de `notas.txt` (que está en temporal) usando **ruta absoluta**
   - Comando: ________________

4. Muestra el contenido del directorio `apuntes` usando **ruta relativa**
   - Comando: ________________

---

### 🎯 **EJERCICIO 3: Copia de Archivos**

**Situación inicial:** Estás en `~/proyecto_so/documentos`

1. Copia `bienvenida.txt` al directorio `backups` usando **ruta relativa**
   - Comando: ________________

2. Copia `apuntes/tema1.txt` a la carpeta actual usando **ruta relativa**
   - Comando: ________________

3. Copia `~/temporal/notas.txt` al directorio `ejercicios` usando **ruta absoluta**
   - Comando: ________________

4. Verifica que las copias se han realizado correctamente
   - Comando: ________________

---

### 🎯 **EJERCICIO 4: Mover Archivos**

**Situación inicial:** Estás en `~/proyecto_so`

1. Mueve el archivo `tema1.txt` (que copiaste en el ejercicio anterior) desde `documentos` a `backups` usando **ruta relativa**
   - Comando: ________________

2. Mueve `script_ejemplo.sh` desde `scripts` a `documentos` usando **rutas relativas**
   - Comando: ________________

3. Navega a `~/temporal` y mueve `notas.txt` a `~/proyecto_so/backups` usando **ruta absoluta**
   - Comando: ________________

---

### 🎯 **EJERCICIO 5: Creación de Directorios y Archivos**

**Situación inicial:** Estás en `~/proyecto_so/documentos/apuntes`

1. Crea un directorio llamado `tema2` en la ubicación actual usando **ruta relativa**
   - Comando: ________________

2. Crea un directorio llamado `configuracion` en `~/proyecto_so` usando **ruta absoluta**
   - Comando: ________________

3. Crea un archivo llamado `resumen.txt` en el directorio actual
   - Comando: ________________

4. Crea un archivo llamado `README.txt` en `~/proyecto_so` usando **ruta absoluta**
   - Comando: ________________

---

### 🎯 **EJERCICIO 6: Navegación Avanzada con .. y .**

**Situación inicial:** Estás en `~/proyecto_so/documentos/ejercicios`

1. Muestra el contenido del directorio padre (`documentos`) usando `..`
   - Comando: ________________

2. Muestra el contenido del directorio `apuntes` (hermano del actual) usando `..`
   - Comando: ________________

3. Navega al directorio `imagenes` usando rutas relativas con `..`
   - Comando: ________________

4. Desde `imagenes`, navega a `scripts` usando solo rutas relativas
   - Comando: ________________

5. Copia el archivo `resumen.txt` de `apuntes/tema2` a `backups` usando rutas relativas con `..`
   - Comando: ________________

---

### 🎯 **EJERCICIO 7: Eliminación de Archivos y Directorios**

**Situación inicial:** Estás en `~/proyecto_so`

⚠️ **ADVERTENCIA:** Ten mucho cuidado con los comandos de eliminación. Asegúrate de estar en el directorio correcto.

1. Elimina el archivo `script_ejemplo.sh` de `documentos` usando **ruta relativa**
   - Comando: ________________

2. Elimina el directorio vacío `tema2` (dentro de apuntes) usando **ruta relativa**
   - Comando: ________________

3. Elimina el directorio `temporal` de tu home usando **ruta absoluta**
   - Comando: ________________

4. Elimina todos los archivos del directorio `backups` usando **ruta relativa** (NO el directorio)
   - Comando: ________________

---

### 🎯 **EJERCICIO 8: Desafío Final - Ruta Compleja**

**Situación inicial:** Estás en `~/proyecto_so/documentos/apuntes`

Realiza las siguientes tareas usando SOLO rutas relativas (prohibido usar rutas absolutas o ~):

1. Lista el contenido del directorio `scripts`
   - Comando: ________________

2. Crea un archivo llamado `desafio.txt` en el directorio `imagenes`
   - Comando: ________________

3. Copia `bienvenida.txt` desde `documentos` a `configuracion`
   - Comando: ________________

4. Navega al directorio `ejercicios` (hermano de apuntes)
   - Comando: ________________

5. Desde ejercicios, muestra el contenido de `README.txt` que está en `proyecto_so`
   - Comando: ________________

---

## PARTE 4: PREGUNTAS DE REFLEXIÓN

Responde a las siguientes preguntas para consolidar tu aprendizaje:

1. **¿Cuál es la principal diferencia entre una ruta absoluta y una relativa?**
   
   _______________________________________________________________________

2. **¿En qué situaciones es más conveniente usar rutas absolutas?**
   
   _______________________________________________________________________

3. **¿En qué situaciones es más conveniente usar rutas relativas?**
   
   _______________________________________________________________________

4. **¿Qué significan los símbolos `.` y `..` en las rutas?**
   
   _______________________________________________________________________

5. **Si estás en `/home/alumno/proyecto_so/documentos` y ejecutas `cd ../scripts`, ¿dónde acabarás?**
   
   _______________________________________________________________________

6. **¿Cómo puedes volver rápidamente a tu directorio home desde cualquier ubicación?**
   
   _______________________________________________________________________

---

## PARTE 5: VERIFICACIÓN FINAL

Para comprobar que has completado correctamente la actividad, ejecuta:

```bash
cd ~/proyecto_so
ls -R
```

Deberías ver una estructura similar a esta:

```
proyecto_so/
├── backups/
├── configuracion/
│   └── bienvenida.txt
├── documentos/
│   ├── apuntes/
│   │   └── tema1.txt
│   ├── bienvenida.txt
│   └── ejercicios/
│       ├── notas.txt
│       └── practica1.txt
├── imagenes/
│   └── desafio.txt
├── scripts/
└── README.txt
```

---

## ENTREGA DE LA ACTIVIDAD

**Formato de entrega:**
- Documento de texto con todos los comandos utilizados en cada ejercicio
- Respuestas a las preguntas de reflexión
- Captura de pantalla del resultado del comando `ls -R` en el directorio `proyecto_so`

**Criterios de evaluación:**
- Correcta diferenciación entre rutas absolutas y relativas (30%)
- Uso apropiado de los comandos (30%)
- Navegación eficiente por el sistema de archivos (20%)
- Respuestas correctas a las preguntas de reflexión (20%)

---

## RECURSOS ADICIONALES

### Recordatorio de comandos:
- `pwd` - Muestra el directorio actual (Print Working Directory)
- `cd [ruta]` - Cambia de directorio
- `ls [ruta]` - Lista el contenido de un directorio
- `cat [archivo]` - Muestra el contenido de un archivo
- `cp [origen] [destino]` - Copia archivos
- `mv [origen] [destino]` - Mueve o renombra archivos
- `rm [archivo]` - Elimina archivos
- `mkdir [directorio]` - Crea directorios
- `rmdir [directorio]` - Elimina directorios vacíos
- `nano [archivo]` - Editor de texto

### Símbolos especiales:
- `/` - Raíz del sistema
- `~` - Directorio home del usuario
- `.` - Directorio actual
- `..` - Directorio padre
- `-` - Directorio anterior (con cd -)

---

**¡Buena suerte con la práctica!** 🐧