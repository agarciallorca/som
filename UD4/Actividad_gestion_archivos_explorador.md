Has sido contratado como asistente en un departamento que maneja la documentación de tres proyectos diferentes. Tu tarea es organizar la información según las normativas internas, garantizando la seguridad y la accesibilidad de ciertos documentos clave.

#### Pasos a Seguir

1.  **Creación de la Estructura (Máster):**
    * En la raíz de su carpeta de trabajo (`C:\Usuarios\SuNombre`), crea una carpeta principal con el nombre: **`GESTION_DOCUMENTAL_PROYECTOS`**.
    * Dentro de esta carpeta, crea tres subcarpetas, una para cada proyecto: **`PROYECTO_A`**, **`PROYECTO_B`**, y **`PROYECTO_C`**.
    * Dentro de la carpeta **`PROYECTO_A`**, crea la siguiente estructura jerárquica de subcarpetas:
        * `01_Borradores`
        * `02_Finalizados`
        * `03_Recursos_Graficos`
        * `99_Entrega_Cliente`

2.  **Manejo de Archivos (Mover, Copiar, Renombrar):**
    * Asume que dispones de 10 archivos de texto (creándolos con el Bloc de notas). Nómbralos del `doc_1.txt` al `doc_10.txt` y colócalos inicialmente en la carpeta **`01_Borradores`**.
    * **Mover:** Mueve los archivos del `doc_1.txt` al `doc_4.txt` a la carpeta **`02_Finalizados`**.
    * **Renombrar:** Dentro de **`02_Finalizados`**, renombra los archivos movidos con el prefijo `FINAL_` (ej. `doc_1.txt` pasa a ser `FINAL_doc_1.txt`).
    * **Copiar:** Copia el archivo `FINAL_doc_3.txt` y pégalo en la carpeta **`99_Entrega_Cliente`**, renombrándolo como **`Informe_Final_A.txt`**.

3.  **Compresión y Gestión de Atributos:**
    * **Compresión:** Comprime la carpeta completa **`PROYECTO_A`** en un único archivo ZIP llamado **`Backup_Proyecto_A.zip`** y almacénalo en la carpeta **`PROYECTO_B`**.
    * **Atributos de Seguridad:** El archivo **`Informe_Final_A.txt`** es crítico y no debe ser modificado por error. Configura el **atributo de solo lectura** para este archivo.
    * **Eliminación:** Elimina permanentemente la carpeta **`03_Recursos_Graficos`** de **`PROYECTO_A`** (asumiendo que ya no se necesita).

4.  **Búsqueda Avanzada:**
    * Realiza una búsqueda dentro de la carpeta **`GESTION_DOCUMENTAL_PROYECTOS`** para localizar todos los archivos que contengan el prefijo **`FINAL_`**.
    * Captura una imagen de la ventana del Explorador de archivos mostrando los resultados de esta búsqueda.

### 📦 Entrega

El resultado de la actividad es la propia estructura de carpetas y archivos modificada en el sistema. Para la evaluación, muestra al profesor lo siguiente:

1.  La **ruta completa** de la carpeta **`GESTION_DOCUMENTAL_PROYECTOS`**.
2.  La **captura de pantalla** de la búsqueda avanzada realizada en el paso 4.

---

### Criterios de Puntuación (Rúbrica de Evaluación)

| Elemento a Evaluar | Puntuación Máxima | Criterios de Logro |
| :--- | :--- | :--- |
| **Estructura Jerárquica** | 20% | Creación correcta de las 7 carpetas con los nombres exactos y en la jerarquía solicitada. |
| **Manejo de Archivos** | 30% | Ejecución correcta de las operaciones de **mover**, **copiar** y **renombrar** según las especificaciones. |
| **Compresión y Atributos** | 30% | Compresión adecuada de la carpeta en formato ZIP y aplicación correcta del **atributo de solo lectura**. |
| **Eliminación y Búsqueda** | 20% | Eliminación correcta de la carpeta no necesaria y uso eficiente de la herramienta de **búsqueda avanzada** (evidenciado por la captura). |
