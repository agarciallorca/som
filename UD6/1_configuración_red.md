## Objetivo de la actividad
Configurar la máquina Debian 12 con dos perfiles de red conmutables (uno estático para **"OFICINA"** y otro dinámico para **"MOVIL"**) utilizando tanto la terminal (`nmcli`) como la interfaz gráfica.

---

## Tarea 1: Perfil "OFICINA" (IP estática mediante terminal)
*Escenario: Trabajas en una oficina técnica donde necesitas una IP fija para que otros compañeros puedan acceder a tus servicios locales.*

1.  **Identificación:** Averigua el nombre de tu interfaz de red (ej: `enp0s3` o `eth0`).
    ```bash
    nmcli device status
    ```
2.  **Creación:** Crea el perfil de red estática. 
    *Usa los siguientes datos (o los que te asigne el profesor):*
    * **Nombre de conexión:** `OFICINA`
    * **IP:** `172.30.135.2XX/24` siendo `XX` el número de tu ordenador.
    * **Puerta de enlace:** `172.30.135.1`
    * **DNS:** `10.239.3.7`

    **Comando a ejecutar:**
    ```bash
    sudo nmcli con add type ethernet con-name OFICINA ifname [TU_INTERFAZ] ipv4.method manual ipv4.addresses [TU_IP] ipv4.gateway [TU_PUERTA_ENLACE] ipv4.dns [TU_DNS]
    ```
3.  **Activación:** Levanta la conexión y verifica la IP.
    ```bash
    sudo nmcli con up OFICINA
    ip a
    ```

---

## Tarea 2: Perfil "MOVIL" (IP Dinámica mediante interfaz gráfica)
*Escenario: Te desplazas a una cafetería o a casa, donde la red te asigna la configuración automáticamente mediante DHCP.*

1.  Abre el panel de **Configuración** de Debian y ve a **Red**.
2.  Pulsa el botón **+** para añadir una nueva conexión de tipo **Cableada/Ethernet**.
3.  Configura el nombre como `MOVIL`.
4.  En la pestaña **IPv4**, selecciona el método **Automático (DHCP)**.
5.  Pulsa en **Añadir / Guardar**.

---

## Tarea 3: Conmutación y Pruebas
*El objetivo de tener perfiles es poder "saltar" de uno a otro según nuestra ubicación sin reconfigurar nada.*

1.  **Cambio a Dinámico:** Desde la terminal, activa el perfil móvil.
    ```bash
    sudo nmcli con up MOVIL
    ```
2.  **Verificación:** Ejecuta `ip a`. ¿Qué IP tienes ahora? ¿Es distinta a la de la Tarea 1?
3.  **Cambio a Estático:** Vuelve al perfil de oficina usando la terminal.
    ```bash
    sudo nmcli con up OFICINA
    ```

---

## Tarea 4: Modificación y Prioridades
1.  **Modificar DNS:** Cambia el DNS del perfil `OFICINA` a `8.8.4.4` sin borrar la conexión:
    ```bash
    sudo nmcli con mod OFICINA ipv4.dns "8.8.8.8,8.8.4.4"
    sudo nmcli con up OFICINA
    ```
2.  **Prioridad:** Configura el perfil `OFICINA` para que tenga prioridad sobre el `MOVIL` (auto-conexión).
    ```bash
    sudo nmcli con mod OFICINA connection.autoconnect-priority 10
    sudo nmcli con mod MOVIL connection.autoconnect-priority 5
    ```

---

## Cuestionario de Reflexión

1. ¿Qué ventaja tiene crear perfiles de red frente a editar cada vez la conexión?
2. Si ejecutas `nmcli connection show`, ¿de qué color aparece la conexión activa?
3. ¿Qué sucede si activas el perfil `OFICINA` pero el cable de red está desconectado?
4. ¿Cómo borrarías el perfil `MOVIL` por completo usando la terminal?

---

## Entrega
Adjunta un documento con:
* Captura de pantalla de `nmcli connection show` con ambos perfiles creados.
* Captura de pantalla de `ip a` con el perfil `OFICINA` activo.
* Respuestas al cuestionario.
