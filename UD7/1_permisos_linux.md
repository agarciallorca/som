# Permisos y propiedad en Linux

---

## 1. Anatomía de un archivo (`ls -l`)

Al ejecutar `ls -l`, la primera columna define quién puede hacer qué:
`- rwx r-x r--`

| Posición | Sigla | Significado |
| :--- | :--- | :--- |
| **1ª** | `-` / `d` | **-** es un archivo normal. **d** es un directorio (carpeta). |
| **2ª-4ª** | **User** | Permisos del **Dueño** del archivo. |
| **5ª-7ª** | **Group** | Permisos del **Grupo** asignado al archivo. |
| **8ª-10ª** | **Others** | Permisos para el **Resto** de usuarios del sistema. |

---

## 2. Notación octal

En Linux, los permisos se representan con números del 0 al 7. Solo tienes que saber sumar estas tres cifras:

* **4** = Leer (**r**)
* **2** = Escribir (**w**)
* **1** = Ejecutar (**x**) / *Entrar en carpetas*
* **0** = Sin permisos (---)

### Combinaciones más frecuentes:

| Número | Letras | Uso común |
| :--- | :--- | :--- |
| **7** | `rwx` | Control total (4+2+1). |
| **6** | `rw-` | Leer y escribir, pero no ejecutar (4+2). |
| **5** | `r-x` | Leer y poder entrar en la carpeta (4+1). |
| **4** | `r--` | Solo lectura (4). |

---

## 3. Notación simbólica

En Linux, los permisos también se pueden conceder, retirar o asignar de forma individual sin modificar el resto de ámbitos (**u**, **g**, **o**):

* **+** Concede un permiso
* **-** Retira un permiso
* **=** Asigna un permiso

### Ejemplos:

Para un fichero con estos permisos iniciales: `rw- rw- r--`

| Letras | Resultado | Significado |
| :--- | :--- | :--- |
| `u+x` | `rwx rw- r--` | Conceder permiso de ejecución al usuario propietario. |
| `ug+x` | `rwx rwx r--` | Conceder permiso de ejecución al usuario propietario y al grupo. |
| `o-r` | `rwx rw- ---` | Quitar permiso de lectura al resto de usuarios del sistema (otros). |
| `ug=rwx` | `rwx rwx r--` | Se asignan los permisos de lectura y escritura al usuario y al grupo, para el resto de usuarios queda como estaba. |
| `a+x` | `rwx rwx r-x` | Se concede permiso de ejecución a todos los ámbitos. |

---

## 4. Comandos de gestión

### Cambiar permisos (`chmod`)
Modifica **qué** se puede hacer con el archivo.
* `chmod 755 archivo` → Dueño hace todo, los demás solo leen y entran.
* `chmod 644 archivo` → Dueño lee/escribe, los demás solo leen. (Estándar para archivos).
* `chmod -R 755 carpeta` → Aplica los permisos a la carpeta **y a todo su contenido** (Recursivo).
* `chmod u+x archivo` → Dueño puede ejecutar un archivo. (Un script, por ejemplo).

### Cambiar propiedad (`chown`)
Modifica **de quién** es el archivo. Requiere `sudo`.
* `sudo chown usuario archivo` → Cambia el dueño.
* `sudo chown usuario:grupo archivo` → Cambia dueño y grupo a la vez.
* `sudo chown :grupo archivo` → Cambia solo el grupo.
