# Actividades: Permisos y propiedad en Linux

### 1. Conversión entre notación simbólica y octal
Traduce estos códigos numéricos a notación de letras (`rwx`) o viceversa:

* **755** $\rightarrow$ `___ ___ ___`  *(Ejemplo: rwx r-x r-x)*
* **644** $\rightarrow$ `___ ___ ___`
* **700** $\rightarrow$ `___ ___ ___`
* **rw- r-- r--** $\rightarrow$ Número: ________
* **rwx r-x ---** $\rightarrow$ Número: ________
* **r-- r-- r--** $\rightarrow$ Número: ________

---

### 2. ¿Qué comando usarías?
Escribe el comando completo (incluyendo `sudo` si crees que es necesario) para resolver cada reto:

1.  **Privacidad:** Tienes un archivo llamado `nomina.txt`. Quieres que el **dueño** pueda leerlo y escribirlo, pero que el **grupo** y el **resto del mundo** no puedan hacer absolutamente nada.
    * **Comando:** `________________________________________________`

2.  **Scripting:** Has creado un script llamado `backup.sh`. Al intentar ejecutarlo con `./backup.sh`, el sistema dice "Permiso denegado". Quieres dar permiso de **ejecución** al dueño y al grupo.
    * **Comando:** `________________________________________________`

3.  **Traspaso:** Un compañero ha dejado el proyecto. Tienes que cambiar la propiedad del archivo `memoria.docx` para que el nuevo dueño sea el usuario `jefe` y el grupo sea `directivos`.
    * **Comando:** `________________________________________________`

4.  **Recursividad:** Tienes una carpeta llamada `web_proyecto` que contiene cientos de imágenes y archivos. Necesitas que la carpeta y **todo su contenido** tenga permisos `755` de una sola vez.
    * **Comando:** `________________________________________________`

---

### 3. Razona

**Escenario:** Intentas entrar en una carpeta llamada `CONFIDENCIAL` usando el comando `cd CONFIDENCIAL`. El sistema te responde: **"bash: cd: CONFIDENCIAL: Permiso denegado"**.

Al hacer un `ls -l`, ves la siguiente línea:
`drw- r-- r--  2 alumno alumno  4096 mar 20 12:00 CONFIDENCIAL`

**Pregunta:** Si tú eres el usuario `alumno` y el archivo te pertenece, ¿por qué no puedes entrar a pesar de tener permisos de lectura (`r`) y escritura (`w`)? ¿Qué cambio de permisos deberías hacer sobre la carpeta para permitirte el paso?
