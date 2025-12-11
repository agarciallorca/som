Tu tarea es modificar la configuración de red de tu máquina virtual para que actúe como un equipo independiente en la red local (Modo Puente) y luego configurar manualmente una dirección IP estática.

---

#### PARTE 1: Configuración del Adaptador en la Máquina Virtual

1.  **Modo Puente (Bridge):**
    * Apaga la Máquina Virtual (VM) de Windows.
    * Accede a la **Configuración de la VM** en VirtualBox.
    * Localiza la configuración del **Adaptador de red** (Network Adapter).
    * Cambia el modo de la red de NAT a **Adaptador Puente (Bridged Adapter)**. 
    * Inicia la VM.

2.  **Verificación Inicial:**
    * Una vez que Windows haya iniciado, accede al **Centro de redes y recursos compartidos**.
    * Verifica que el sistema ha intentado obtener una dirección IP de la red física (DHCP).
    * **Registro:** Abre la Terminal y ejecuta el comando `ipconfig`. Anota la dirección IP y la puerta de enlace predeterminada (Default Gateway) que te ha asignado el router.

---

#### PARTE 2: Asistente de Configuración de IP Estática

1.  **Configuración Manual:**
    * Accede a la configuración de las **Propiedades del Adaptador de red** de Windows (puedes hacerlo desde el Panel de Control o la Configuración).
    * Entra en las propiedades del protocolo **Protocolo de Internet versión 4 (TCP/IP v4)**.
    * Selecciona la opción **Usar la siguiente dirección IP**.

2.  **Asignación de Parámetros Estáticos:**
    * Asigna una dirección IP estática que pertenezca al mismo segmento de red que la red física. Toma la IP de tu máquina real y suma 100 al último octeto.
        * **Ejemplo:** Si la IP de tu equipo es `172.30.135.117`, usa `172.30.135.217`.
    * **Máscara de subred:** Configúrala como `255.255.255.0`.
    * **Puerta de enlace predeterminada (Gateway):** Usa la dirección que anotaste en el Paso 2 de la Parte 1.
    * **Servidores DNS:** Configura los servidores DNS de Google:
        * **Preferido:** `8.8.8.8`
        * **Alternativo:** `8.8.4.4`

3.  **Verificación Final:**
    * Ejecuta el comando `ipconfig /all` en la Terminal para confirmar que los parámetros (IP, Máscara y DNS) se han aplicado correctamente.
    * Realiza un `ping` a tu Puerta de Enlace (Gateway) para confirmar la conectividad local.

### 📦 Entrega

Entrega **una única captura de pantalla** que muestre:

1.  La ventana de las **Propiedades de TCP/IP v4** con los parámetros estáticos (IP, Máscara, Gateway, DNS) que configuraste.
2.  La ventana de la **Terminal de comandos** mostrando el resultado exitoso del `ping` a la Puerta de Enlace.
