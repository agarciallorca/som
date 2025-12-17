Tu tarea es demostrar el ciclo completo de recuperación del sistema: crear un punto de restauración, provocar un cambio no deseado o un fallo, y luego revertir el sistema a su estado anterior usando el punto de restauración creado.

#### Pasos a Seguir

1.  **Estado Inicial y Creación de Punto Estable:**
    * **1.1. Verificación:** Accede a las propiedades del sistema y verifica que la **Protección del Sistema** esté **activada** para la unidad principal (C:). Si no lo está, actívala.
    * **1.2. Prueba:** Crea en el escritorio un archivo de texto llamado **`ANTES_DEL_FALLO.txt`** con el texto "Este archivo debe desaparecer".
    * **1.3. Punto de Restauración:** Crea un nuevo punto de restauración manual.
      * **Nombre:** Ponle el nombre: **`PUNTO_LIMPIO_TU_NOMBRE`**.
    
2.  **Provocación del Fallo (Cambio Indeseado):**
    * **2.1. Cambio Visual:** Cambia el fondo de escritorio.
    * **2.2. Cambio Crítico (Fallo Simulado):** Deshabilita el servicio de **Cola de impresión (Spooler)** de forma permanente (tipo de inicio "Deshabilitado") para simular un fallo grave en la gestión de servicios.
    * **2.3. Cambio de Archivo:** En el escritorio, **elimina** el archivo **`ANTES_DEL_FALLO.txt`**.

3.  **Ejecución de la Recuperación:**
    * **3.1. Inicio:** Accede a la utilidad **Restaurar sistema**.
    * **3.2. Selección:** Selecciona la opción **Elegir otro punto de restauración**.
    * **3.3. Restauración:** Selecciona el punto que creaste en el Paso 1: **`PUNTO_LIMPIO_TU_NOMBRE`**.
    * Haz clic en **Finalizar** e inicia la restauración. (La máquina virtual se reiniciará).

4.  **Verificación Final:**
    * Una vez que la máquina virtual se haya reiniciado y la restauración haya finalizado, verifica lo siguiente:
        * El **Fondo de escritorio** deben haber vuelto a la configuración anterior al fallo (Paso 2.1).
        * El archivo **`ANTES_DEL_FALLO.txt`** debe **haber reaparecido** en el escritorio.
        * El servicio de **Cola de impresión** debe haber vuelto a su estado original (probablemente "Automático").
    * **Captura:** Realiza capturas de pantalla que muestren claramente el archivo **`ANTES_DEL_FALLO.txt`**, el fondo de escritorio restaurado y el servicio restarurado a su configuración original.

### 📦 Entrega

Entrega las capturas de pantalla realizadas en la actividad.
