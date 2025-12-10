Debes crear dos tareas programadas distintas para demostrar tu habilidad en la automatización de acciones: una para programas y otra para comandos de sistema.

---

#### PARTE 1: Automatización de Aplicaciones (Recordatorio Diario)

1.  **Creación de la Tarea:**
    * Accede al **Programador de Tareas** de Windows.
    * Crea una **Tarea Básica**.
    * **Nombre:** Asígnale el nombre: **`Recordatorio_Diario_TU_NOMBRE`**.
    * **Disparador (Trigger):** Configura la tarea para que se ejecute **Diariamente** a la hora **12:00**.
    * **Acción (1ª Acción):** Configura que se ejecute el **Bloc de Notas** (`notepad.exe`).

2.  **Modificación de la Tarea:**
    * Localiza la tarea **`Recordatorio_Diario_TU_NOMBRE`**.
    * Accede a sus **Propiedades** y ve a la pestaña **Acciones**.
    * **Añade una 2ª Acción:**
        * Configura esta acción para que ejecute la **Calculadora** de Windows (`calc.exe`).

3.  **Gestión y Comprobación:**
    * **Deshabilita** la tarea **`Recordatorio_Diario_TU_NOMBRE`**.
    * **Captura 1:** Realiza una captura de pantalla que muestre la tarea en la Biblioteca del Programador de Tareas, con su **Estado** como **Deshabilitada** y su **Próxima hora de ejecución** configurada para las 08:00 AM del día siguiente.

---

#### PARTE 2: Automatización de Comandos (Apagado de Sistema)

1.  **Creación de la Tarea de Comando:**
    * Crea una **Tarea Básica** nueva.
    * **Nombre:** Asígnale el nombre: **`Apagado_Automatico_TU_NOMBRE`**.
    * **Disparador (Trigger):** Configura la tarea para que se ejecute **Una vez** a una hora dentro de los próximos 5 minutos (para poder probarla manualmente antes de deshabilitarla).
    * **Acción (Acción Única):** Configura que la acción sea **Iniciar un programa**.
    * **Programa/Script:** Escribe: `shutdown`
    * **Agregar argumentos (opcional):** Escribe: `-s -t 120` (Esto apagará el equipo en 120 segundos).

2.  **Gestión y Comprobación Final:**
    * **IMPORTANTE:** Para evitar el apagado del equipo, **deshabilita** inmediatamente la tarea **`Apagado_Automatico_TU_NOMBRE`**.
    * **Captura 2:** Realiza una captura de pantalla que muestre la tarea **`Apagado_Automatico_TU_NOMBRE`** y en sus **Propiedades** (pestaña General o Acciones) los argumentos del comando `shutdown`.

### 📦 Entrega

Entrega **dos capturas de pantalla** que cumplan con los requisitos de la **Captura 1** y la **Captura 2** de ambas partes.

---

### Rúbrica de Evaluación Sugerida para el Criterio (h) (Final)

| Elemento | Nivel de Logro | Puntuación Máxima |
| :--- | :--- | :--- |
| **Parte 1: Tarea de Aplicaciones** | Se crea con el nombre, disparador y ambas acciones (`notepad.exe`, `calc.exe`) correctas. Tarea deshabilitada. | 50% |
| **Parte 2: Tarea de Comandos** | Se crea con el nombre y disparador correctos. El comando `shutdown` se configura como programa y los argumentos `-s -t 120` se añaden correctamente. Tarea deshabilitada. | 50% |
| **Puntuación Total** | **100%** | |
| **Nivel Básico (50%)** | Logras completar todos los pasos de una de las dos tareas de forma correcta, o completas ambas tareas con errores en los nombres, disparadores o la inclusión de argumentos. | |
| **Nivel No Alcanzado (0%)** | No logras crear ninguna de las tareas o no demuestras el uso de disparadores y acciones. | |
