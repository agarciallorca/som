# ACTIVIDAD PRÁCTICA: IMPORTACIÓN, CLONADO Y EXPORTACIÓN DE MÁQUINAS VIRTUALES

## Información General
- **Software:** Oracle VM VirtualBox
- **Sistema Operativo:** Arch Linux
- **Nivel:** Básico
- **Duración estimada:** 1-2 horas

---

## Objetivos de la Actividad

Al finalizar esta actividad, serás capaz de:
- Exportar una máquina virtual a formato OVA/OVF
- Importar máquinas virtuales desde archivos
- Clonar máquinas virtuales (completo y enlazado)
- Comprender las diferencias entre los métodos de clonación
- Gestionar y organizar máquinas virtuales de forma eficiente

---

## PARTE 1: CONCEPTOS FUNDAMENTALES

### ¿Qué es la Exportación de Máquinas Virtuales?

La **exportación** es el proceso de guardar una máquina virtual completa en un archivo portable que puede:
- Transferirse a otro ordenador
- Compartirse con otros usuarios
- Servir como copia de seguridad
- Importarse en diferentes hipervisores

### Formatos de Exportación

#### OVF (Open Virtualization Format)
- Formato abierto estándar
- Compatible con múltiples hipervisores
- Genera múltiples archivos (descriptores + discos virtuales)

#### OVA (Open Virtualization Archive)
- Archivo único comprimido
- Contiene todos los componentes de la VM
- Más fácil de transportar y compartir
- **Formato recomendado para esta práctica**

### ¿Qué es el Clonado de Máquinas Virtuales?

El **clonado** crea una copia de una máquina virtual existente. Existen dos tipos:

#### Clonado Completo
- Copia **independiente** de la VM original
- Ocupa el mismo espacio en disco que la original
- Cambios en el clon **NO afectan** a la original
- **Uso:** Cuando necesitas VMs totalmente independientes

#### Clonado Enlazado
- Copia **dependiente** de la VM original
- Ocupa mucho menos espacio (solo diferencias)
- Requiere que la VM original exista
- Más rápido de crear
- **Uso:** Para pruebas rápidas o entornos de desarrollo

### ¿Qué es la Importación de Máquinas Virtuales?

La **importación** es el proceso de cargar una máquina virtual desde un archivo OVA/OVF a VirtualBox.

---

## PARTE 2: PREPARACIÓN DEL ENTORNO

### Requisitos Previos

Antes de comenzar, verifica que tienes:
- [ ] VirtualBox instalado y funcionando
- [ ] Una máquina virtual de Arch Linux operativa
- [ ] Al menos 20 GB de espacio libre en disco
- [ ] Permisos de administrador (si es necesario)

### Configuración Inicial

1. **Abre VirtualBox**

2. **Identifica tu máquina virtual de Arch Linux**
   - Anota su nombre: _______________________
   - Verifica que funciona correctamente (enciéndela y apágala)

3. **Crea una carpeta de trabajo**
   - Ubicación recomendada: `~/Documentos/VirtualBox_Exportaciones`
   - Aquí guardarás las exportaciones

---

## PARTE 3: EJERCICIOS PRÁCTICOS

### 🎯 **EJERCICIO 1: Exportación de una Máquina Virtual**

#### Paso 1: Preparar la VM para exportación

1. **Apaga completamente** tu máquina virtual de Arch Linux
   - No la suspendas, debe estar apagada
   - Verifica en VirtualBox que el estado es "Apagada"

2. **Limpia la VM (opcional pero recomendado)**
   - Si la VM está encendida, puedes ejecutar:
   ```bash
   sudo pacman -Sc    # Limpia caché de paquetes
   sudo journalctl --vacuum-time=1d  # Limpia logs antiguos
   ```

#### Paso 2: Exportar la VM

1. En VirtualBox, selecciona tu máquina virtual de Arch Linux

2. Ve al menú **Archivo → Exportar servicio virtualizado**
   - O usa el atajo: `Ctrl + E`

3. **Configuración de exportación:**
   - **Formato:** Open Virtualization Format 2.0
   - **Archivo:** Navega a tu carpeta de trabajo y nómbralo `ArchLinux_original.ova`
   - **Modo de archivo:** Selecciona **"Crear un archivo manifiesto"**
   - **Incluir dirección MAC:** Desmarcado (recomendado)

4. Haz clic en **Siguiente**

5. **Información del servicio virtualizado:**
   - **Nombre:** ArchLinux_Exportado
   - **Producto:** Arch Linux VM
   - **Versión:** 1.0
   - **Descripción:** "Máquina virtual de Arch Linux para prácticas de SO"
   - Puedes dejar los demás campos como están

6. Haz clic en **Exportar**

7. **Espera a que complete el proceso**
   - Esto puede tardar varios minutos dependiendo del tamaño de la VM
   - Observa la barra de progreso

#### Paso 3: Verificar la exportación

1. Navega a tu carpeta de trabajo

2. Comprueba que existe el archivo `ArchLinux_original.ova`

3. **Anota el tamaño del archivo:** _____________ MB/GB

4. **Anota el tiempo que tardó la exportación:** _____________ minutos

**Preguntas de reflexión:**

a) ¿Por qué es importante apagar la VM antes de exportar?

_________________________________________________________________

b) ¿Qué ventajas tiene usar formato OVA en lugar de OVF?

_________________________________________________________________

---

### 🎯 **EJERCICIO 2: Clonado Completo de una Máquina Virtual**

#### Paso 1: Crear un clon completo

1. En VirtualBox, **haz clic derecho** sobre tu VM de Arch Linux

2. Selecciona **Clonar**

3. **Configuración del clon:**
   - **Nombre:** ArchLinux_Clon_Completo
   - **Ruta:** Déjala por defecto (o selecciona tu ubicación preferida)
   - **Política de dirección MAC:** Generar nuevas direcciones MAC para todos los adaptadores de red
   - Marca **"Incluir sólo las instantáneas de la máquina actual"** (si tienes instantáneas)

4. Haz clic en **Siguiente**

5. **Tipo de clon:**
   - Selecciona **"Clonación completa"**
   - Lee la descripción que aparece

6. Haz clic en **Clonar**

7. Espera a que complete el proceso

#### Paso 2: Verificar el clon completo

1. Observa que ahora tienes dos VMs en VirtualBox:
   - La original: _______________________
   - El clon: ArchLinux_Clon_Completo

2. **Inicia el clon completo** y verifica que funciona correctamente

3. Comprueba el espacio en disco:
   - Ve a la ubicación de las VMs (normalmente `~/VirtualBox VMs/`)
   - Compara el tamaño de las carpetas de ambas VMs
   - **Tamaño VM original:** _____________ GB
   - **Tamaño clon completo:** _____________ GB

4. **Apaga el clon**

**Preguntas de reflexión:**

a) ¿Qué similitudes observas entre el tamaño de la VM original y el clon completo?

_________________________________________________________________

b) ¿Por qué es importante generar nuevas direcciones MAC?

_________________________________________________________________

---

### 🎯 **EJERCICIO 3: Clonado Enlazado de una Máquina Virtual**

#### Paso 1: Crear un clon enlazado

1. En VirtualBox, **haz clic derecho** sobre tu VM de Arch Linux original

2. Selecciona **Clonar**

3. **Configuración del clon:**
   - **Nombre:** ArchLinux_Clon_Enlazado
   - **Ruta:** Déjala por defecto
   - **Política de dirección MAC:** Generar nuevas direcciones MAC para todos los adaptadores de red

4. Haz clic en **Siguiente**

5. **Tipo de clon:**
   - Selecciona **"Clonación enlazada"**
   - Lee atentamente la advertencia que aparece

6. Haz clic en **Clonar**

7. El proceso será muy rápido (mucho más que el clon completo)

#### Paso 2: Verificar el clon enlazado

1. Observa que ahora tienes tres VMs en VirtualBox:
   - La original
   - El clon completo
   - El clon enlazado

2. **Inicia el clon enlazado** y verifica que funciona

3. Comprueba el espacio en disco del clon enlazado:
   - **Tamaño clon enlazado:** _____________ GB

4. **Apaga el clon enlazado**

**Preguntas de reflexión:**

a) ¿Qué diferencia notable observas en el tamaño entre el clon completo y el enlazado?

_________________________________________________________________

b) ¿Qué pasaría si eliminas la VM original teniendo un clon enlazado?

_________________________________________________________________

c) ¿Cuál fue más rápido de crear? ¿Por qué?

_________________________________________________________________

---

### 🎯 **EJERCICIO 4: Importación de una Máquina Virtual**

#### Paso 1: Eliminar la VM original (simulación)

⚠️ **IMPORTANTE:** Vamos a eliminar la VM original de VirtualBox (pero el archivo OVA que exportamos sigue existiendo).

1. En VirtualBox, **haz clic derecho** sobre tu VM original de Arch Linux

2. Selecciona **Eliminar**

3. En la ventana que aparece:
   - Selecciona **"Eliminar todos los archivos"**
   - Esto borrará completamente la VM

4. Confirma la eliminación

5. Verifica que la VM original ya no aparece en VirtualBox
   - Deberían quedar solo los dos clones

#### Paso 2: Importar la VM desde el archivo OVA

1. Ve al menú **Archivo → Importar servicio virtualizado**
   - O usa el atajo: `Ctrl + I`

2. **Seleccionar archivo:**
   - Haz clic en el icono de carpeta
   - Navega hasta tu carpeta de trabajo
   - Selecciona el archivo `ArchLinux_original.ova`
   - Haz clic en **Abrir**

3. Haz clic en **Siguiente**

4. **Configuración del servicio:**
   - Revisa la información de la VM
   - **Nombre:** Cambia el nombre a `ArchLinux_Importado`
   - **Carpeta de máquina base:** Déjala por defecto
   - **Dirección MAC:** Política: Generar nuevas direcciones MAC para todos los adaptadores de red
   - Puedes modificar RAM, CPU si lo deseas (opcional)

5. Haz clic en **Importar**

6. **Acepta los términos de licencia** si aparecen

7. Espera a que complete la importación

#### Paso 3: Verificar la importación

1. Comprueba que `ArchLinux_Importado` aparece en tu lista de VMs

2. **Inicia la VM importada** y verifica que funciona correctamente

3. Comprueba que es funcionalmente idéntica a la original

4. **Apaga la VM importada**

**Preguntas de reflexión:**

a) ¿La VM importada conserva todos los archivos y configuraciones de la original?

_________________________________________________________________

b) ¿Qué utilidad práctica tiene poder importar/exportar VMs?

_________________________________________________________________

---

### 🎯 **EJERCICIO 5: Comparativa y Gestión de Snapshots (Instantáneas)**

#### Paso 1: Crear instantáneas

1. Selecciona **ArchLinux_Clon_Completo**

2. Con la VM apagada, haz clic en el botón **Instantáneas** (icono de tres líneas horizontales en la esquina superior derecha)

3. Haz clic en **Tomar** (icono de cámara)

4. **Configuración de la instantánea:**
   - **Nombre:** Estado_Inicial
   - **Descripción:** "Estado limpio antes de realizar cambios"
   
5. Haz clic en **Aceptar**

6. Inicia la VM y realiza algunos cambios:
   - Crea un archivo en el escritorio
   - Instala un paquete pequeño: `sudo pacman -S htop`

7. Apaga la VM

8. Crea otra instantánea:
   - **Nombre:** Con_Cambios
   - **Descripción:** "Después de instalar htop y crear archivo"

#### Paso 2: Restaurar instantáneas

1. En el panel de instantáneas, selecciona **Estado_Inicial**

2. Haz clic en **Restaurar**

3. Confirma la restauración

4. Inicia la VM y comprueba:
   - ¿Está el archivo que creaste? __________
   - ¿Está htop instalado? (ejecuta `htop`) __________

5. Apaga la VM

**Preguntas de reflexión:**

a) ¿Qué diferencia hay entre una instantánea y un clon?

_________________________________________________________________

b) ¿Cuándo usarías una instantánea en lugar de un clon?

_________________________________________________________________

---

### 🎯 **EJERCICIO 6: Desafío - Exportación Selectiva**

#### Objetivo
Exportar solo el clon completo con sus instantáneas.

#### Pasos

1. Exporta **ArchLinux_Clon_Completo** con el nombre `ArchLinux_Con_Snapshots.ova`

2. Durante la exportación, observa las opciones disponibles

3. Elimina **ArchLinux_Clon_Completo** de VirtualBox (con todos sus archivos)

4. Importa de nuevo desde `ArchLinux_Con_Snapshots.ova` con el nombre `ArchLinux_Recuperado`

5. Verifica:
   - ¿Se conservaron las instantáneas? __________
   - ¿Puedes restaurar a los estados anteriores? __________

**Responde:**

a) ¿Qué diferencia de tamaño hay entre `ArchLinux_original.ova` y `ArchLinux_Con_Snapshots.ova`?

_________________________________________________________________

b) ¿Por qué existe esa diferencia?

_________________________________________________________________

---

## PARTE 4: TABLA COMPARATIVA

Completa la siguiente tabla con tus observaciones:

| Característica | Clon Completo | Clon Enlazado | Exportación/Importación |
|----------------|---------------|---------------|-------------------------|
| **Espacio en disco** | _________ GB | _________ GB | _________ GB |
| **Tiempo de creación** | _________ min | _________ min | _________ min |
| **Independencia de la original** | Sí / No | Sí / No | Sí / No |
| **Portabilidad** | Alta / Media / Baja | Alta / Media / Baja | Alta / Media / Baja |
| **Uso recomendado** | ____________ | ____________ | ____________ |

---

## PARTE 5: CASOS PRÁCTICOS

### Caso 1: Laboratorio de Pruebas
Necesitas crear 5 entornos de prueba idénticos para probar diferentes configuraciones de red, pero luego vas a modificar cada uno de forma diferente.

**¿Qué método usarías? ¿Por qué?**

_________________________________________________________________

### Caso 2: Backup antes de Actualización
Vas a actualizar el sistema completo de tu VM de producción y quieres poder volver atrás si algo falla, pero necesitas hacerlo rápido.

**¿Qué método usarías? ¿Por qué?**

_________________________________________________________________

### Caso 3: Compartir con Compañero
Tu compañero necesita una copia exacta de tu VM de Arch Linux para trabajar en su ordenador en casa.

**¿Qué método usarías? ¿Por qué?**

_________________________________________________________________

### Caso 4: Desarrollo con Múltiples Ramas
Trabajas en un proyecto y necesitas probar código en diferentes ramas, pero todas parten del mismo sistema base.

**¿Qué método usarías? ¿Por qué?**

_________________________________________________________________

---

## PARTE 6: LIMPIEZA Y ORGANIZACIÓN

### Tarea Final

1. **Organiza tus máquinas virtuales:**
   - Elimina las VMs que no necesites
   - Mantén solo: ArchLinux_Importado y una de las clonadas
   
2. **Organiza tus archivos OVA:**
   - Mueve todos los archivos .ova a una carpeta de backups
   - Nómbralos con fecha: `ArchLinux_2024-XX-XX.ova`

3. **Crea un documento de inventario:**
   - Lista todas las VMs que tienes
   - Anota su propósito
   - Anota su tamaño en disco

---

## PARTE 7: PREGUNTAS DE EVALUACIÓN

1. **Define con tus propias palabras qué es una máquina virtual exportada.**

   _________________________________________________________________

2. **¿Cuál es la principal diferencia entre un clon completo y uno enlazado?**

   _________________________________________________________________

3. **¿En qué formato se exportan las máquinas virtuales en VirtualBox?**

   _________________________________________________________________

4. **¿Qué ventajas tiene exportar una VM en lugar de copiar simplemente su carpeta?**

   _________________________________________________________________

5. **¿Puedes usar un clon enlazado si eliminas la VM original? ¿Por qué?**

   _________________________________________________________________

6. **¿Qué es mejor para hacer un backup: clon completo, instantánea o exportación? Justifica tu respuesta.**

   _________________________________________________________________

7. **Si quieres distribuir una VM a 30 compañeros de clase, ¿qué método usarías?**

   _________________________________________________________________

8. **¿Qué precauciones debes tomar antes de exportar una VM?**

   _________________________________________________________________

---

## CRITERIOS DE EVALUACIÓN

La actividad se evaluará según los siguientes criterios:

| Criterio | Puntuación |
|----------|------------|
| Exportación correcta de VM | 20% |
| Creación de clones (completo y enlazado) | 25% |
| Importación exitosa de VM | 20% |
| Gestión de instantáneas | 15% |
| Respuestas a preguntas de reflexión | 10% |
| Casos prácticos resueltos | 10% |

---

## ENTREGA DE LA ACTIVIDAD

**Debes entregar:**

1. **Documento de respuestas** con:
   - Todas las preguntas de reflexión respondidas
   - Tabla comparativa completada
   - Casos prácticos resueltos
   - Preguntas de evaluación respondidas

2. **Capturas de pantalla:**
   - Proceso de exportación (ventana de configuración)
   - Lista de VMs mostrando original, clones e importada
   - Panel de instantáneas con las capturas creadas
   - Tamaño de los archivos .ova en el explorador de archivos

3. **Inventario de VMs** (documento de texto o hoja de cálculo)

---

## RECURSOS ADICIONALES

### Documentación Oficial
- [VirtualBox Manual - Import/Export](https://www.virtualbox.org/manual/ch01.html#ovf)
- [VirtualBox Manual - Snapshots](https://www.virtualbox.org/manual/ch01.html#snapshots)

### Atajos de Teclado Útiles
- `Ctrl + E` - Exportar servicio virtualizado
- `Ctrl + I` - Importar servicio virtualizado
- `Ctrl + T` - Tomar instantánea (con VM seleccionada)

### Consejos Importantes
- Siempre apaga las VMs antes de clonar o exportar
- Los clones enlazados son más rápidos pero dependientes
- Las exportaciones OVA son portables entre hipervisores
- Las instantáneas son ideales para puntos de restauración rápidos
- Mantén backups regulares de tus VMs importantes

---

**¡Éxito con la práctica!** 💻
