# Guía de PowerShell - Línea de Comandos

## Índice
1. [Introducción a PowerShell](#introducción)
2. [Cmdlets básicos](#cmdlets-básicos)
3. [Comodines](#comodines)
4. [Redirección de salida](#redirección-de-salida)
5. [Ejercicios prácticos](#ejercicios-prácticos)

---

## Introducción

PowerShell es un shell de línea de comandos y lenguaje de scripting diseñado especialmente para la administración del sistema. A diferencia de CMD tradicional, PowerShell utiliza **cmdlets** (commandlets), que son comandos específicos que siguen una estructura consistente.

### Estructura de un Cmdlet
Los cmdlets siguen el patrón **Verbo-Sustantivo**, por ejemplo:
- `Get-ChildItem` (Obtener elementos hijos)
- `New-Item` (Crear nuevo elemento)
- `Remove-Item` (Eliminar elemento)

---

## Cmdlets de Navegación

### 1. Set-Location
Cambia el directorio de trabajo actual (similar a `cd` en CMD)

**Sintaxis básica:**
```powershell
Set-Location -Path "ruta"
```

**Ejemplos:**
```powershell
# Ir a una carpeta específica
Set-Location -Path "C:\Users\Usuario\Documentos"

# Forma abreviada (sin -Path)
Set-Location "C:\Windows"

# Subir un nivel (ir a la carpeta padre)
Set-Location ..

# Subir dos niveles
Set-Location ..\..

# Ir al disco D:
Set-Location D:\

# Volver a la carpeta personal del usuario
Set-Location ~
```

**Alias comunes:** `cd`, `chdir`, `sl`

**Conceptos importantes:**
- `.` representa el directorio actual
- `..` representa el directorio padre
- `~` representa la carpeta personal del usuario

---

### 2. Get-Location
Muestra el directorio de trabajo actual (similar a `pwd` en Linux)

**Sintaxis básica:**
```powershell
Get-Location
```

**Ejemplos:**
```powershell
# Mostrar directorio actual
Get-Location

# Guardar la ubicación en una variable
$ubicacion = Get-Location
Write-Output "Estás en: $ubicacion"

# Mostrar solo la ruta como texto
(Get-Location).Path
```

**Alias comunes:** `pwd`, `gl`

---

### 3. Test-Path
Verifica si existe un archivo o carpeta

**Sintaxis básica:**
```powershell
Test-Path -Path "ruta"
```

**Ejemplos:**
```powershell
# Verificar si existe un archivo
Test-Path -Path "C:\datos.txt"
# Devuelve: True o False

# Verificar si existe una carpeta
Test-Path -Path "C:\MisCarpetas"

# Verificar múltiples archivos con comodines
Test-Path "*.txt"
# Devuelve True si existe al menos un archivo .txt
```

**Uso práctico:**
Es muy útil para evitar errores antes de:
- Copiar o mover archivos
- Crear carpetas (verificar que no existan)
- Leer contenido de archivos

---

## Cmdlets de Gestión de Archivos y Carpetas

### 4. New-Item
Crea nuevos elementos (archivos, carpetas, etc.)

**Sintaxis básica:**
```powershell
New-Item -Path "ruta" -ItemType "tipo"
```

**Ejemplos:**
```powershell
# Crear una carpeta
New-Item -Path "C:\MisCarpetas\Nueva" -ItemType Directory

# Crear un archivo de texto
New-Item -Path "C:\MisCarpetas\archivo.txt" -ItemType File

# Crear archivo con contenido
New-Item -Path "documento.txt" -ItemType File -Value "Este es el contenido inicial"
```

---

### 5. Get-ChildItem
Muestra los elementos contenidos en una ubicación (similar a `dir` o `ls`)

**Sintaxis básica:**
```powershell
Get-ChildItem -Path "ruta"
```

**Ejemplos:**
```powershell
# Listar contenido del directorio actual
Get-ChildItem

# Listar contenido de una carpeta específica
Get-ChildItem -Path "C:\Users"

# Listar solo archivos con extensión .txt
Get-ChildItem -Path "C:\Documentos" -Filter *.txt

# Listar incluyendo archivos ocultos
Get-ChildItem -Force

# Búsqueda recursiva (incluye subcarpetas)
Get-ChildItem -Path "C:\Proyectos" -Recurse
```

**Alias comunes:** `gci`, `dir`, `ls`

---

## Cmdlets de Contenido

### 10. Get-Content
Lee el contenido de un archivo

**Sintaxis básica:**
```powershell
Get-Content -Path "archivo"
```

**Ejemplos:**
```powershell
# Leer todo el contenido de un archivo
Get-Content -Path "notas.txt"

# Leer las primeras 5 líneas
Get-Content -Path "registro.log" -TotalCount 5

# Leer las últimas 10 líneas
Get-Content -Path "registro.log" -Tail 10
```

**Alias comunes:** `gc`, `cat`, `type`

---

### 6. Copy-Item
Copia elementos (archivos o carpetas) de un lugar a otro

**Sintaxis básica:**
```powershell
Copy-Item -Path "origen" -Destination "destino"
```

**Ejemplos:**
```powershell
# Copiar un archivo
Copy-Item -Path "documento.txt" -Destination "C:\Backup\documento.txt"

# Copiar una carpeta completa (recursivo)
Copy-Item -Path "C:\Proyecto" -Destination "D:\Backup\Proyecto" -Recurse

# Copiar varios archivos usando comodines
Copy-Item -Path "*.jpg" -Destination "C:\Imagenes"

# Copiar con confirmación
Copy-Item -Path "importante.txt" -Destination "C:\Backup" -Confirm
```

**Alias comunes:** `copy`, `cp`, `cpi`

---

### 7. Move-Item
Mueve elementos de un lugar a otro (cortar y pegar)

**Sintaxis básica:**
```powershell
Move-Item -Path "origen" -Destination "destino"
```

**Ejemplos:**
```powershell
# Mover un archivo
Move-Item -Path "temporal.txt" -Destination "C:\Archivos\temporal.txt"

# Mover una carpeta completa
Move-Item -Path "C:\Temp\Proyecto" -Destination "D:\Proyectos"

# Mover y renombrar al mismo tiempo
Move-Item -Path "viejo.txt" -Destination "C:\Nuevos\nuevo.txt"

# Mover varios archivos
Move-Item -Path "*.log" -Destination "C:\Registros"
```

**Alias comunes:** `move`, `mv`, `mi`

---

### 8. Remove-Item
Elimina elementos (archivos o carpetas)

**Sintaxis básica:**
```powershell
Remove-Item -Path "elemento"
```

**Ejemplos:**
```powershell
# Eliminar un archivo
Remove-Item -Path "borrar.txt"

# Eliminar una carpeta vacía
Remove-Item -Path "C:\CarpetaVacia"

# Eliminar carpeta con contenido (recursivo)
Remove-Item -Path "C:\CarpetaConArchivos" -Recurse

# Eliminar con confirmación
Remove-Item -Path "importante.txt" -Confirm

# Eliminar forzosamente (archivos de solo lectura)
Remove-Item -Path "protegido.txt" -Force
```

**Alias comunes:** `del`, `erase`, `rm`, `ri`

⚠️ **Advertencia:** Ten cuidado con este comando, especialmente con `-Recurse` y `-Force`, ya que la eliminación es permanente.

---

### 9. Rename-Item
Renombra elementos (archivos o carpetas)

**Sintaxis básica:**
```powershell
Rename-Item -Path "nombre_actual" -NewName "nombre_nuevo"
```

**Ejemplos:**
```powershell
# Renombrar un archivo
Rename-Item -Path "viejo_nombre.txt" -NewName "nuevo_nombre.txt"

# Renombrar una carpeta
Rename-Item -Path "CarpetaVieja" -NewName "CarpetaNueva"

# Cambiar extensión
Rename-Item -Path "documento.txt" -NewName "documento.md"
```

**Alias comunes:** `ren`, `rni`

---

### 8. Write-Output
Envía objetos al pipeline (los muestra en pantalla o los redirige)

**Sintaxis básica:**
```powershell
Write-Output "texto"
```

**Ejemplos:**
```powershell
# Mostrar texto simple
Write-Output "Hola, mundo"

# Mostrar múltiples líneas
Write-Output "Línea 1" "Línea 2" "Línea 3"

```

**Alias comunes:** `echo`, `write`

---

## Cmdlets de Atributos y Propiedades

### 14. Get-ItemProperty
Obtiene las propiedades de un archivo o carpeta (atributos, fechas, tamaño, etc.)

**Sintaxis básica:**
```powershell
Get-ItemProperty -Path "ruta"
```

**Ejemplos:**
```powershell
# Ver todas las propiedades de un archivo
Get-ItemProperty -Path "documento.txt"

# Ver propiedades de una carpeta
Get-ItemProperty -Path "C:\MisCarpetas"

# Ver solo los atributos
(Get-ItemProperty "archivo.txt").Attributes

# Ver tamaño del archivo
(Get-ItemProperty "video.mp4").Length

# Ver fecha de creación
(Get-ItemProperty "foto.jpg").CreationTime

# Ver fecha de última modificación
(Get-ItemProperty "datos.txt").LastWriteTime

```

**Propiedades comunes:**
- `Attributes` - Atributos del archivo (ReadOnly, Hidden, Archive, System)
- `Length` - Tamaño en bytes
- `CreationTime` - Fecha de creación
- `LastWriteTime` - Fecha de última modificación
- `LastAccessTime` - Fecha de último acceso
- `FullName` - Ruta completa

---

### 15. Set-ItemProperty
Modifica las propiedades y atributos de archivos o carpetas

**Sintaxis básica:**
```powershell
Set-ItemProperty -Path "ruta" -Name "propiedad" -Value "valor"
```

**Ejemplos:**

**Establecer atributo de Solo Lectura:**
```powershell
# Hacer un archivo de solo lectura
Set-ItemProperty -Path "importante.txt" -Name IsReadOnly -Value $true

# Quitar el atributo de solo lectura
Set-ItemProperty -Path "importante.txt" -Name IsReadOnly -Value $false
```

**Establecer atributo de Oculto:**
```powershell
# Ocultar un archivo
Set-ItemProperty -Path "secreto.txt" -Name Attributes -Value Hidden

# Mostrar un archivo oculto
Set-ItemProperty -Path "secreto.txt" -Name Attributes -Value Normal

# Ocultar una carpeta
Set-ItemProperty -Path "C:\CarpetaOculta" -Name Attributes -Value Hidden
```

**Combinar atributos:**
```powershell
# Archivo oculto Y solo lectura
Set-ItemProperty -Path "config.sys" -Name Attributes -Value "Hidden,ReadOnly"

# Archivo oculto Y de sistema
Set-ItemProperty -Path "boot.ini" -Name Attributes -Value "Hidden,System"
```

**Ejemplos prácticos:**
```powershell
# Proteger un archivo contra modificaciones
Set-ItemProperty -Path "original.txt" -Name IsReadOnly -Value $true

# Ocultar archivos temporales
Get-ChildItem "temp_*.txt" | ForEach-Object {
    Set-ItemProperty -Path $_.FullName -Name Attributes -Value Hidden
}

# Verificar y cambiar atributo
if ((Get-ItemProperty "datos.txt").IsReadOnly -eq $true) {
    Set-ItemProperty -Path "datos.txt" -Name IsReadOnly -Value $false
    Write-Output "Archivo desbloqueado"
}
```

**Atributos disponibles:**
- `Normal` - Sin atributos especiales
- `ReadOnly` - Solo lectura (no se puede modificar)
- `Hidden` - Oculto (no visible por defecto)
- `System` - Archivo del sistema
- `Archive` - Marcado para backup
- `Directory` - Es un directorio

**⚠️ Nota importante:**
Para ver archivos ocultos con Get-ChildItem, usa el parámetro `-Force`:
```powershell
Get-ChildItem -Force
```

---

## Cmdlets de Ayuda

### 16. Get-Help
Muestra información de ayuda sobre cmdlets y conceptos de PowerShell

**Sintaxis básica:**
```powershell
Get-Help nombre-cmdlet
```

**Ejemplos:**
```powershell
# Ayuda básica de un cmdlet
Get-Help Get-ChildItem

# Ayuda detallada
Get-Help Get-ChildItem -Detailed

# Ver todos los ejemplos
Get-Help Copy-Item -Examples

# Ayuda completa (muy detallada)
Get-Help Remove-Item -Full

# Ayuda solo de parámetros
Get-Help New-Item -Parameter *

# Buscar ayuda sobre un tema
Get-Help *content*

# Ayuda sobre conceptos
Get-Help about_wildcards
Get-Help about_redirection

# Ver ayuda en ventana separada (más cómodo)
Get-Help Get-Content -ShowWindow
```

**Alias comunes:** `help`, `man`

**Diferencia entre alias:**
```powershell
# 'help' muestra la ayuda página por página
help Get-ChildItem

# 'Get-Help' muestra toda la ayuda de una vez
Get-Help Get-ChildItem
```

**Consejos:**
- Usa `-Examples` cuando solo necesites ver cómo usar el cmdlet
- Usa `-ShowWindow` para una lectura más cómoda
- Los temas "about_" explican conceptos: `Get-Help about_*` para ver todos

---

## Comodines

Los comodines permiten hacer coincidir patrones en nombres de archivos y carpetas.

### Asterisco (*)
Representa **cero o más caracteres** de cualquier tipo.

**Ejemplos:**
```powershell
# Todos los archivos .txt
Get-ChildItem *.txt

# Todos los archivos que empiezan con "informe"
Get-ChildItem informe*

# Todos los archivos que terminan con "2024"
Get-ChildItem *2024.*

# Todos los archivos
Get-ChildItem *.*
```

### Interrogación (?)
Representa **exactamente un carácter** de cualquier tipo.

**Ejemplos:**
```powershell
# Archivos como test1.txt, test2.txt, testA.txt
Get-ChildItem test?.txt

# Archivos de 3 letras con extensión .log
Get-ChildItem ???.log

# Combinar ambos comodines
Get-ChildItem foto_???_*.jpg
# Coincide con: foto_001_vacaciones.jpg, foto_abc_familia.jpg
```

### Ejemplos combinados
```powershell
# Copiar todos los .jpg y .png
Copy-Item *.jpg, *.png -Destination C:\Imagenes

# Eliminar archivos temporales
Remove-Item temp*.*, *_backup.* -Confirm

# Mover archivos de un patrón específico
Move-Item documento_202?.txt -Destination C:\Archivos2020s
```

---

## Redirección de Salida

La redirección permite enviar la salida de un comando a un archivo en lugar de mostrarla en pantalla.

### Operadores de redirección

| Operador | Descripción | Ejemplo |
|----------|-------------|---------|
| `>` | Crea o sobrescribe un archivo | `comando > archivo.txt` |
| `>>` | Añade al final del archivo | `comando >> archivo.txt` |
| `2>` | Redirige errores | `comando 2> errores.txt` |
| `2>&1` | Redirige errores a salida estándar | `comando > todo.txt 2>&1` |

### Ejemplos prácticos

```powershell
# Guardar lista de archivos en un archivo
Get-ChildItem > lista.txt

# Añadir al final sin borrar contenido previo
Get-ChildItem C:\Windows >> lista.txt

# Guardar contenido de un archivo en otro
Get-Content original.txt > copia.txt

# Guardar salida de múltiples comandos
Write-Output "=== Directorio actual ===" > informe.txt
Get-ChildItem >> informe.txt
Write-Output "`n=== Procesos activos ===" >> informe.txt
Get-Process >> informe.txt

# Redirigir solo errores
Get-ChildItem C:\NoExiste 2> errores.log

# Redirigir todo (salida y errores)
Get-ChildItem C:\Windows > salida_completa.txt 2>&1
```

### Diferencias clave

**Usando `>`:**
```powershell
# Primera ejecución
Write-Output "Primera línea" > archivo.txt
# Contenido: "Primera línea"

# Segunda ejecución (BORRA el contenido anterior)
Write-Output "Segunda línea" > archivo.txt
# Contenido: "Segunda línea"
```

**Usando `>>`:**
```powershell
# Primera ejecución
Write-Output "Primera línea" >> archivo.txt
# Contenido: "Primera línea"

# Segunda ejecución (AÑADE al contenido anterior)
Write-Output "Segunda línea" >> archivo.txt
# Contenido: 
# "Primera línea"
# "Segunda línea"
```

---

## Ejercicios Prácticos

### Ejercicio 1: Navegación y verificación
Realiza las siguientes tareas:
1. Muestra tu directorio actual
2. Navega a tu carpeta de Documentos
3. Verifica si existe una carpeta llamada "Practica"
4. Si no existe, créala
5. Entra en la carpeta "Practica"

**Solución:**
```powershell
Get-Location
Set-Location ~\Documents
Test-Path "Practica"
New-Item -Path "Practica" -ItemType Directory
Set-Location Practica
```

---

### Ejercicio 2: Gestión básica de archivos
Crea la siguiente estructura de carpetas y archivos:
```
Practica/
├── Documentos/
│   ├── carta.txt
│   └── informe.txt
├── Imagenes/
└── Backup/
```

**Comandos:**
```powershell
New-Item -Path "Practica" -ItemType Directory
New-Item -Path "Practica\Documentos" -ItemType Directory
New-Item -Path "Practica\Imagenes" -ItemType Directory
New-Item -Path "Practica\Backup" -ItemType Directory
New-Item -Path "Practica\Documentos\carta.txt" -ItemType File
New-Item -Path "Practica\Documentos\informe.txt" -ItemType File
```

---

### Ejercicio 3: Trabajo con contenido de archivos
1. Crea un archivo "tareas.txt" con el contenido "Lista de tareas pendientes"
2. Añade tres tareas al archivo
3. Lee el contenido completo del archivo
4. Guarda la lista en otro archivo llamado "tareas_backup.txt"

**Solución:**
```powershell
Set-Content -Path "tareas.txt" -Value "Lista de tareas pendientes"
Add-Content -Path "tareas.txt" -Value "1. Estudiar PowerShell"
Add-Content -Path "tareas.txt" -Value "2. Hacer ejercicios prácticos"
Add-Content -Path "tareas.txt" -Value "3. Repasar para el examen"
Get-Content -Path "tareas.txt"
Get-Content -Path "tareas.txt" | Set-Content -Path "tareas_backup.txt"
```

---

### Ejercicio 4: Atributos de archivos
1. Crea un archivo llamado "confidencial.txt"
2. Escribe algo de contenido en él
3. Hazlo de solo lectura
4. Verifica que es de solo lectura
5. Ocúltalo
6. Lista todos los archivos (incluidos ocultos) para verificar

**Solución:**
```powershell
New-Item -Path "confidencial.txt" -ItemType File
Set-Content -Path "confidencial.txt" -Value "Información confidencial"
Set-ItemProperty -Path "confidencial.txt" -Name IsReadOnly -Value $true
Get-ItemProperty -Path "confidencial.txt" | Select-Object Name, IsReadOnly
Set-ItemProperty -Path "confidencial.txt" -Name Attributes -Value "Hidden,ReadOnly"
Get-ChildItem -Force
```

---

### Ejercicio 5: Uso de comodines
1. Lista todos los archivos .txt del directorio actual
2. Copia todos los archivos que empiecen con "doc" a la carpeta Backup
3. Renombra todos los .txt añadiendo "_old" antes de la extensión

---

### Ejercicio 6: Redirección
1. Lista el contenido de tu carpeta de usuario y guárdalo en "mi_directorio.txt"
2. Añade al mismo archivo la fecha actual usando `Get-Date`
3. Lee el contenido del archivo creado

---

### Ejercicio 7: Combinando cmdlets (Proyecto completo)
Crea un script que:
1. Cree una carpeta llamada "Proyecto2024"
2. Dentro cree tres archivos: notas.txt, tareas.txt, resumen.txt
3. Escriba "Inicio del proyecto" en cada archivo
4. Copie todos los archivos a una carpeta "Backup"
5. Liste el contenido de Backup y guárdelo en un archivo de registro

**Desafío adicional:**
6. Haz que el archivo de registro sea de solo lectura
7. Usa Get-Help para aprender sobre un cmdlet que no conocías

---

## Contenido Avanzado

### Permisos NTFS (Nivel avanzado)

Para cuando avancéis en el curso, PowerShell también permite gestionar permisos NTFS completos mediante:

**Get-Acl** - Obtiene las listas de control de acceso (ACL)
```powershell
# Ver permisos de un archivo
Get-Acl "archivo.txt" | Format-List

# Ver permisos de una carpeta
Get-Acl "C:\MisCarpetas" | Format-List
```

**Set-Acl** - Establece las listas de control de acceso
```powershell
# Copiar permisos de un archivo a otro
$acl = Get-Acl "archivo_origen.txt"
Set-Acl "archivo_destino.txt" -AclObject $acl
```

**Nota:** La gestión de permisos NTFS es un tema complejo que incluye:
- Usuarios y grupos
- Permisos efectivos
- Herencia de permisos
- Tipos de acceso (lectura, escritura, modificación, control total)

Este contenido se estudiará más adelante cuando veáis gestión de usuarios y grupos en profundidad.

---

## Consejos Útiles

1. **Usa Tab para autocompletar**: Escribe las primeras letras y presiona Tab
2. **Historial de comandos**: Usa las flechas ↑ ↓ para navegar por comandos previos
3. **Obtén ayuda**: Usa `Get-Help nombre-cmdlet` o `nombre-cmdlet -?`
4. **Parámetro -WhatIf**: Prueba qué haría un comando sin ejecutarlo realmente
   ```powershell
   Remove-Item *.txt -WhatIf
   ```
5. **Parámetro -Confirm**: Pide confirmación antes de ejecutar
   ```powershell
   Remove-Item importante.txt -Confirm
   ```

---

## Resumen de Cmdlets por Categoría

### Navegación
| Cmdlet | Alias | Descripción |
|--------|-------|-------------|
| Set-Location | `cd`, `chdir`, `sl` | Cambiar directorio |
| Get-Location | `pwd`, `gl` | Mostrar directorio actual |
| Test-Path | - | Verificar existencia |

### Gestión de archivos y carpetas
| Cmdlet | Alias | Descripción |
|--------|-------|-------------|
| New-Item | `ni` | Crear archivo/carpeta |
| Get-ChildItem | `gci`, `dir`, `ls` | Listar contenido |
| Copy-Item | `copy`, `cp`, `cpi` | Copiar |
| Move-Item | `move`, `mv`, `mi` | Mover |
| Remove-Item | `del`, `rm`, `ri` | Eliminar |
| Rename-Item | `ren`, `rni` | Renombrar |

### Contenido
| Cmdlet | Alias | Descripción |
|--------|-------|-------------|
| Get-Content | `gc`, `cat`, `type` | Leer contenido |
| Set-Content | `sc` | Escribir/sobrescribir |
| Add-Content | `ac` | Añadir al final |
| Write-Output | `echo`, `write` | Mostrar en pantalla |

### Propiedades y atributos
| Cmdlet | Alias | Descripción |
|--------|-------|-------------|
| Get-ItemProperty | `gp` | Ver propiedades |
| Set-ItemProperty | `sp` | Modificar propiedades |

### Ayuda
| Cmdlet | Alias | Descripción |
|--------|-------|-------------|
| Get-Help | `help`, `man` | Mostrar ayuda |

---

## Resumen de Alias Útiles

| Cmdlet | Alias comunes |
|--------|---------------|
| Set-Location | `cd`, `chdir`, `sl` |
| Get-Location | `pwd`, `gl` |
| Get-ChildItem | `gci`, `dir`, `ls` |
| Get-Content | `gc`, `cat`, `type` |
| Set-Content | `sc` |
| Add-Content | `ac` |
| Copy-Item | `copy`, `cp`, `cpi` |
| Move-Item | `move`, `mv`, `mi` |
| Remove-Item | `del`, `rm`, `ri` |
| Rename-Item | `ren`, `rni` |
| Write-Output | `echo`, `write` |
| Get-Help | `help`, `man` |

---

**Última actualización:** Enero 2025
