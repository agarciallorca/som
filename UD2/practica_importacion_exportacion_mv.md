# PRÁCTICA: Importación, clonado y exportación de máquinas virtuales

## Objetivos

Al finalizar esta actividad, serás capaz de:
- Exportar una máquina virtual a formato OVA/OVF
- Importar máquinas virtuales desde archivos
- Clonar máquinas virtuales (completo y enlazado)
- Comprender las diferencias entre los métodos de clonación
- Gestionar y organizar máquinas virtuales de forma eficiente

---

## 1. Conceptos fundamentales

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

## 2. Preparación del entorno

### Requisitos Previos

Antes de comenzar, verifica que tienes:
- [ ] VirtualBox instalado y funcionando
- [ ] Una máquina virtual de Arch Linux operativa
- [ ] Al menos 20 GB de espacio libre en disco

### Configuración Inicial

1. **Abre VirtualBox**

2. **Identifica tu máquina virtual de Arch Linux**
   - Verifica que funciona correctamente (enciéndela y apágala)

3. **Crea una carpeta de trabajo**
   - Ubicación: `D:\VIRTUALBOX_VMS\SOM_XXX\Exportaciones_VM`
   - Aquí guardarás las exportaciones

---

## 3. Ejercicios prácticos

### **EJERCICIO 1: Exportación de una Máquina Virtual**

#### Paso 1: Preparar la VM para exportación

**Apaga completamente** tu máquina virtual de Arch Linux
   - No la suspendas, debe estar apagada
   - Verifica en VirtualBox que el estado es "Apagada"

#### Paso 2: Exportar la VM

1. En VirtualBox, selecciona tu máquina virtual de Arch Linux

2. Ve al menú **Archivo → Exportar servicio virtualizado**

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
   - **Descripción:** "Máquina virtual de Arch Linux para prácticas de SOM"
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

a) ¿Por qué es importante apagar la VM antes de exportar?\
b) ¿Qué ventajas tiene usar formato OVA en lugar de OVF?

---

### **EJERCICIO 2: Clonado Completo de una Máquina Virtual**

#### Paso 1: Crear un clon completo

1. En VirtualBox, **haz clic derecho** sobre tu VM de Arch Linux

2. Selecciona **Clonar**

3. **Configuración del clon:**
   - **Nombre:** ArchLinux_Clon_Completo
   - **Ruta:** Tu carpeta de trabajo de exportaciones
   - **Política de dirección MAC:** Generar nuevas direcciones MAC para todos los adaptadores de red
     
4. Haz clic en **Siguiente**

5. **Tipo de clon:**
   - Selecciona **"Clonación completa"**
   - Lee la descripción que aparece

6. Haz clic en **Clonar**

7. Espera a que complete el proceso

#### Paso 2: Verificar el clon completo

1. Observa que ahora tienes dos VMs en VirtualBox:
   - La original: ArchLinux
   - El clon: ArchLinux_Clon_Completo

2. **Inicia el clon completo** y verifica que funciona correctamente

3. Comprueba el espacio en disco:
   - Ve a la ubicación de las VMs (normalmente `~/VirtualBox VMs/`)
   - Compara el tamaño de las carpetas de ambas VMs
   - **Tamaño VM original:** _____________ GB
   - **Tamaño clon completo:** _____________ GB

4. **Apaga el clon**

**Preguntas de reflexión:**

a) ¿Qué similitudes observas entre el tamaño de la VM original y el clon completo?\
b) ¿Por qué es importante generar nuevas direcciones MAC?

---

### **EJERCICIO 3: Clonado Enlazado de una Máquina Virtual**

#### Paso 1: Crear un clon enlazado

1. En VirtualBox, **haz clic derecho** sobre tu VM de Arch Linux original

2. Selecciona **Clonar**

3. **Configuración del clon:**
   - **Nombre:** ArchLinux_Clon_Enlazado
   - **Ruta:** Tú carpeta de trabajo de exportaciones
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

a) ¿Qué diferencia notable observas en el tamaño entre el clon completo y el enlazado?\
b) ¿Qué pasaría si eliminas la VM original teniendo un clon enlazado?\
c) ¿Cuál fue más rápido de crear? ¿Por qué?

---

### **EJERCICIO 4: Importación de una Máquina Virtual**

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
   - **Carpeta de máquina base:** Carpeta de trabajo de máquinas virtuales
   - **Dirección MAC:** Política: Generar nuevas direcciones MAC para todos los adaptadores de red
   - Puedes modificar RAM, CPU si lo deseas

5. Haz clic en **Importar**

6. **Acepta los términos de licencia** si aparecen

7. Espera a que complete la importación

#### Paso 3: Verificar la importación

1. Comprueba que `ArchLinux_Importado` aparece en tu lista de VMs

2. **Inicia la VM importada** y verifica que funciona correctamente

3. Comprueba que es funcionalmente idéntica a la original

4. **Apaga la VM importada**

**Preguntas de reflexión:**

a) ¿La VM importada conserva todos los archivos y configuraciones de la original?\
b) ¿Qué utilidad práctica tiene poder importar/exportar VMs?

---

### **EJERCICIO 5: Comparativa y Gestión de Snapshots (Instantáneas)**

#### Paso 1: Crear instantáneas

1. Selecciona **ArchLinux_Clon_Completo**

2. Con la VM apagada, haz clic en el botón **Instantáneas** (icono de tres líneas horizontales en la esquina superior derecha)

3. Haz clic en **Tomar** (icono de cámara)

4. **Configuración de la instantánea:**
   - **Nombre:** Estado_Inicial
   - **Descripción:** "Estado limpio antes de realizar cambios"
   
5. Haz clic en **Aceptar**

6. Inicia la VM y realiza algunos cambios:
   - Crea un archivo en tu directorio personal llamado CAMBIOS.txt
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

a) ¿Qué diferencia hay entre una instantánea y un clon?\
b) ¿Cuándo usarías una instantánea en lugar de un clon?

---

### **EJERCICIO 6: Desafío - Exportación Selectiva**

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

a) ¿Qué diferencia de tamaño hay entre `ArchLinux_original.ova` y `ArchLinux_Con_Snapshots.ova`?\
b) ¿Por qué?

---

## PARTE 4: CASOS PRÁCTICOS

### Caso 1: Laboratorio de Pruebas
Necesitas crear 5 entornos de prueba idénticos para probar diferentes configuraciones de red, pero luego vas a modificar cada uno de forma diferente.

**¿Qué método usarías? ¿Por qué?**

### Caso 2: Backup antes de Actualización
Vas a actualizar el sistema completo de tu VM de producción y quieres poder volver atrás si algo falla, pero necesitas hacerlo rápido.

**¿Qué método usarías? ¿Por qué?**

### Caso 3: Compartir con Compañero
Tu compañero necesita una copia exacta de tu VM de Arch Linux para trabajar en su ordenador en casa.

**¿Qué método usarías? ¿Por qué?**

### Caso 4: Desarrollo con Múltiples Ramas
Trabajas en un proyecto y necesitas probar código en diferentes ramas, pero todas parten del mismo sistema base.

**¿Qué método usarías? ¿Por qué?**

---

## PARTE 5: LIMPIEZA Y ORGANIZACIÓN

**Organiza tus máquinas virtuales:** Elimina las VMs que no necesites. Mantén solo: `ArchLinux_Importado`

**Organiza tus archivos OVA:** Elimina todos los archivos `.ova`.

---

## ENTREGA DE LA ACTIVIDAD

**Debes entregar:**

**Documento de respuestas en Writer** con todas las preguntas de reflexión respondidas y los casos prácticos resueltos.

---

## RECURSOS ADICIONALES

### Documentación Oficial
- [VirtualBox Manual - Import/Export](https://www.virtualbox.org/manual/ch01.html#ovf)
- [VirtualBox Manual - Snapshots](https://www.virtualbox.org/manual/ch01.html#snapshots)

### Consejos Importantes
- Siempre apaga las VMs antes de clonar o exportar
- Los clones enlazados son más rápidos pero dependientes
- Las exportaciones OVA son portables entre hipervisores
- Las instantáneas son ideales para puntos de restauración rápidos
- Mantén backups regulares de tus VMs importantes
