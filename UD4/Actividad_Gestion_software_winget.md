Tienes que demostrar tu habilidad para gestionar las siguientes utilidades utilizando **exclusivamente** la línea de comandos de Windows (Terminal/PowerShell/CMD) y la herramienta **Winget**.

* **Windows PowerToys** (Instalar).
* **Notepad++** (Instalar, Actualizar, Desinstalar).

#### Pasos a Seguir

1.  **Investigación y confirmación de paquetes:**
    * Abre la Terminal de Windows y usa `winget search` para encontrar los IDs exactos para **Windows PowerToys** y **Notepad++**.
    * **Registro:** Anota los dos **IDs de paquete** que encontraste.

2.  **Instalación de utilidades:**
    * **Instalación 1 (PowerToys):** Instala **Windows PowerToys** utilizando su ID.
      * *Comando:* `winget install [ID de PowerToys]`
    * **Instalación 2 (Notepad++):** Instala **Notepad++** utilizando su ID.
      * *Comando:* `winget install [ID de Notepad++]`
    * **Verificación:** Comprueba que ambas aplicaciones aparecen en el Menú Inicio.

3.  **Gestión de actualizaciones:**
    * **3.1. Listar actualizaciones pendientes:** Lista todas las aplicaciones instaladas en el sistema que tienen una actualización disponible a través de Winget.
      * *Comando:* `winget upgrade`
    * **3.2. Aplicar actualización:** Si Winget indica que hay alguna aplicación que pueda actualizar, ejecuta el comando para actualizar esa aplicación específica.
      * *Comando a utilizar (si aplica)*: `winget upgrade [ID de la app a actualizar]`
    * **3.2. Aplicar actualización:** Actualiza **solo** la aplicación **Notepad++** a la última versión disponible (asumiendo que hay una más reciente o forzando la actualización).
      * *Comando:* `winget upgrade [ID de Notepad++]`
    * **Verificación:** Ejecuta nuevamente el comando `winget upgrade` para verificar que **Notepad++** ya no aparece en la lista de actualizaciones pendientes (o captura el mensaje de que ya está en la versión más reciente).

4.  **Desinstalación selectiva:**
    * Desinstala **solamente** la utilidad **Notepad++** del sistema. **PowerToys debe permanecer instalado.**
    * *Comando:* `winget uninstall [ID de Notepad++]`
    * **Verificación:** Confirma que Notepad++ ya no aparece en la lista de Programas Instalados con el comando `winget list`.

### 📦 Entrega

Para la evaluación, entrega un archivo de texto con el siguiente contenido:

1.  Los dos **IDs de paquete** utilizados para PowerToys y Notepad++.
2.  El **comando exacto** utilizado para la **instalación** de PowerToys.
3.  La **salida completa** del comando `winget upgrade` ejecutado **después** de las instalaciones, mostrando si hay alguna aplicación que podría actualizarse.
4.  El **comando exacto** utilizado para **actualizar** una aplicación concreta.
5.  El **comando exacto** utilizado para la **desinstalación** de Notepad++.

---

### Rúbrica de Evaluación

| Nivel de Logro | Tareas Ejecutadas | Puntuación |
| :--- | :--- | :--- |
| **Excelente (4 pts.)** | Logras buscar, instalar **ambas** aplicaciones, listar las actualizaciones, aplicar la actualización a una aplicación correctamente y desinstalar **solo** la aplicación solicitada. Comandos y verificaciones perfectos. | 100% |
| **Satisfactorio (3 pts.)** | Logras la instalación y desinstalación, y listar las actualizaciones, pero tienes fallos menores en la sintaxis de la actualización o no la aplicas correctamente. PowerToys permanece instalado. | 75% |
| **Básico (2 pts.)** | Logras realizar la instalación de al menos una aplicación y la desinstalación. Fallas en las tareas de **`upgrade`** o necesitas ayuda considerable. | 50% |
| **No Alcanzado (0 pts.)** | No logras completar las tareas principales de instalación o desinstalación. No demuestras el uso efectivo de la herramienta Winget. | 0% |
