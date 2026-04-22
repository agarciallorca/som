# Comandos de gestión de procesos y recursos del sistema

Un técnico de sistemas debe saber qué está ocurriendo en el ordenador. En Linux, cada programa en ejecución es un **proceso** con un número de identidad único llamado **PID**.

---

## 1. Monitorización en tiempo real: `top` e `htop`
Para saber el uso de recursos que están realizando los procesos del sistema. Podemos ver el consumo de RAM y CPU.

* **`top`**: Es el monitor nativo.
    * Pulsa `M` para ordenar por uso de Memoria.
    * Pulsa `P` para ordenar por uso de CPU.
    * Pulsa `q` para salir.
* **`htop`**: Es la versión moderna y visual (si no está instalado: `sudo apt install htop`). Permite usar el ratón y ver los núcleos de la CPU de forma gráfica.

---

## 2. Listado de procesos: `ps`
Muestra una *fotografía* de los procesos en este preciso instante.

* `ps aux`: Muestra **todos** los procesos de **todos** los usuarios con detalle.
* `ps -u usuario`: Muestra solo los procesos de un usuario concreto.
* **Combinación con `grep`:** Úsalo con `grep` para buscar un programa específico.
  * *Ejemplo:* `ps aux | grep "apache"` (Busca si el servidor web está corriendo).

---

## 3. Finalizar procesos: `kill` y `killall`
Cuando un programa no responde o queremos detener un servicio de forma manual.

* **`kill [PID]`**: Envía una señal para que el proceso se cierre ordenadamente.
* **`kill -9 [PID]`**: "Cierre forzado". Se usa cuando el proceso está totalmente bloqueado y no responde al comando anterior.
* **`killall [nombre]`**: Mata todos los procesos que se llamen igual (ej: `killall firefox`).

---

## 4. Estado del almacenamiento: `df` y `du`
Los comandos `df` y `du` nos permiten ver qué espacio libre o utilizado hay en las unidades de almacenamiento.

* **`df -h`**: (Disk Free) Muestra cuánto espacio libre queda en las particiones (la **h** es de "human-readable", para verlo en GB y MB).
* **`du -sh [carpeta]`**: (Disk Usage) Te dice cuánto ocupa una carpeta específica y todo lo que tiene dentro.
  * *Ejemplo:* `sudo du -sh /var/log` (¿Cuánto pesan mis registros?).

---

## 5. Quién está usando el equipo: `who` y `w`
Útil en servidores multiusuario o para saber si hay alguien conectado por red.

* `who`: Lista simple de usuarios conectados.
* `w`: Muestra quién está conectado, desde dónde y **qué está haciendo** (qué comando está ejecutando).

---

## Escenarios de soporte (Actividades)

Resuelve estas situaciones usando comandos:

1.  **El proceso rebelde:** Un usuario te dice que su navegador se ha colgado.
    * Encuentra el PID del proceso "firefox" y ciérralo por la fuerza.
2.  **Alerta de espacio:** El sistema avisa de que el disco está casi lleno.
    * Usa el comando adecuado para ver qué carpeta de `/var` es la que más ocupa.
3.  **Análisis de logs:**
    * Obtén el espacio ocupado por la carpeta `/var/log`. 
    * Usa `ls` con las opciones adecuadas para ver cuál es el archivo más grande de este directorio.
4.  **Vigilante de CPU:** Abre `top` o `htop` y responde:
    * ¿Cuál es el proceso que más memoria RAM está consumiendo ahora mismo?
    * ¿Y el que más CPU usa?
