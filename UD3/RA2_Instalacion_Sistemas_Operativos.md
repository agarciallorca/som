# Instalación de sistemas operativos

**Módulo:** Sistemas Operativos Monopuesto (SMR) · **RA 2:** Instala sistemas operativos, relacionando sus características con el hardware del equipo y el software de aplicación.

Instalar un sistema operativo no consiste en pulsar «Siguiente» hasta que termine. Es un proceso con decisiones previas (¿sirve este equipo?, ¿qué sistema conviene?), una fase de preparación, una instalación propiamente dicha y un trabajo posterior (actualizar, comprobar, documentar). Este documento recorre ese proceso en el mismo orden en que se hace en la vida real, y cada apartado indica entre paréntesis el criterio de evaluación que cubre.

---

## 1. Verificar la idoneidad del hardware (criterio a)

Antes de instalar nada hay que comprobar que el equipo es capaz de ejecutar el sistema que queremos. Cada sistema operativo publica sus **requisitos mínimos** y, aunque menos visibles, unos **requisitos recomendados**. Los mínimos indican con qué se puede arrancar el sistema; los recomendados, con qué se trabaja con comodidad. Un equipo que cumple justo el mínimo funcionará, pero lento, y se quedará obsoleto enseguida.

Los componentes que hay que revisar son:

- **Procesador:** la arquitectura (32 o 64 bits), la frecuencia y el número de núcleos. Hoy la mayoría de sistemas ya solo se publican para 64 bits.
- **Memoria RAM:** es el factor que más se nota en el día a día. Un escritorio moderno con navegador y ofimática necesita bastante más que el mínimo oficial.
- **Almacenamiento:** el espacio libre necesario para el sistema, pero también para las actualizaciones, el software y los datos del usuario. Un disco SSD mejora de forma muy notable el arranque y la respuesta del sistema frente a un disco mecánico.
- **Firmware y arranque:** si el equipo usa BIOS clásica o UEFI, y si permite *Secure Boot*. Algunos sistemas exigen UEFI y, en el caso de Windows 11, un módulo de seguridad TPM.
- **Gráfica, red y periféricos:** que existan controladores (drivers) para ellos. Un sistema perfectamente instalable puede ser inútil si no funciona la tarjeta de red.

Una buena práctica es **comprobar el hardware real antes de instalar**: en Windows con `msinfo32` o el Administrador de tareas, y en Linux con órdenes como `lscpu`, `free -h`, `lsblk` o `lspci`. También es habitual arrancar desde un sistema *Live* (un sistema que se ejecuta desde el USB sin instalarse) para probar que el hardware es compatible antes de comprometerse a instalar.

> Las cifras concretas de requisitos cambian con cada versión. Conviene consultarlas siempre en la web oficial del fabricante en lugar de memorizarlas.

## 2. Seleccionar el sistema operativo (criterio b)

Elegir sistema es un ejercicio de **ajustar necesidades y restricciones**. No hay un sistema «mejor» en abstracto, sino uno más adecuado para un contexto. Los factores a considerar son:

- **Uso previsto del equipo:** puesto de ofimática, equipo de diseño, servidor doméstico, aula de formación, equipo antiguo que se quiere reaprovechar.
- **Hardware disponible:** un equipo con pocos recursos se beneficia de distribuciones ligeras; un equipo moderno admite cualquier opción.
- **Software de aplicación necesario:** si la empresa depende de una aplicación que solo existe para Windows, ese dato condiciona todo lo demás. Es el sentido de la segunda parte del enunciado del RA: relacionar el sistema con el *software de aplicación*.
- **Coste y licencias:** sistemas de pago, gratuitos o de código abierto (se desarrolla en el apartado 7).
- **Soporte y ciclo de vida:** cuánto tiempo recibirá actualizaciones de seguridad. Un sistema sin soporte es un riesgo, porque deja de recibir parches. Por eso en entornos profesionales se prefieren las versiones de **soporte extendido (LTS)**, que se mantienen durante años.
- **Conocimientos del usuario:** el coste de formación y de soporte también cuenta.

Un caso práctico para razonar: una pequeña asesoría quiere renovar cinco equipos que usan un programa de contabilidad solo disponible para Windows. Aunque una distribución Linux saldría gratis, la decisión razonable es Windows. Si el mismo despacho solo necesitara navegador y ofimática, Linux pasaría a ser una opción muy competitiva. La respuesta correcta depende de los requisitos, y la justificación es lo que se evalúa.

## 3. Elaborar un plan de instalación (criterio c)

Un plan de instalación es un documento breve que recoge **qué se va a hacer, en qué orden y qué se hará si algo falla**. En un equipo personal puede parecer exagerado, pero en un aula con treinta equipos, o en una empresa, es lo que separa una instalación ordenada de un desastre.

Un plan razonable incluye:

1. **Datos del equipo y del sistema elegido**, con el resultado de la comprobación de hardware.
2. **Copia de seguridad** de los datos existentes, si el equipo no está vacío. Instalar suele implicar formatear, y lo formateado no se recupera.
3. **Medio de instalación:** descargar la imagen ISO desde la fuente oficial, verificar su integridad (con la suma de comprobación o *hash* que publica el fabricante) y crear un USB de arranque o montar la ISO en la máquina virtual.
4. **Esquema de particionado:** cuántas particiones, de qué tamaño y con qué sistema de archivos.
5. **Parámetros de configuración:** nombre del equipo, usuarios, idioma, zona horaria, red.
6. **Software adicional y controladores** que habrá que instalar después.
7. **Pruebas finales y documentación:** qué se comprobará al terminar para dar la instalación por buena.
8. **Plan de contingencia:** cómo se vuelve atrás si algo falla.

Cuando hay que instalar muchos equipos iguales, el plan suele contemplar también **métodos de instalación desatendida o por clonación de imagen**, que ahorran tiempo y garantizan que todos los equipos queden idénticos.

## 4. Configurar los parámetros básicos de la instalación (criterio d)

Durante el asistente de instalación hay que tomar una serie de decisiones. Las más importantes son:

**Idioma, distribución del teclado y zona horaria.** Parecen detalles menores, pero una distribución de teclado equivocada complica hasta escribir la contraseña que se acaba de crear.

**Particionado y sistema de archivos.** Es la decisión más delicada. Un disco se divide en **particiones**, y cada una se formatea con un **sistema de archivos** (NTFS en Windows; ext4 es el habitual en Linux). Conviene entender dos conceptos:

- El **esquema de particiones**: *MBR*, heredado de la BIOS clásica y con limitaciones, o *GPT*, asociado a UEFI y sin esas limitaciones. El esquema debe ser coherente con el modo de arranque del equipo.
- La **partición de arranque**: en equipos UEFI existe una pequeña partición del sistema (*EFI System Partition*, ESP) donde residen los gestores de arranque.

En Linux es frecuente separar la partición del sistema (`/`) de la de los datos de los usuarios (`/home`), de modo que se pueda reinstalar el sistema sin perder los datos. También suele crearse un área de **intercambio** (*swap*), que el sistema usa como apoyo cuando se agota la RAM. En Windows el asistente suele crear automáticamente las particiones auxiliares que necesita.

**Cuentas de usuario.** Se crea al menos un usuario con su contraseña. Conviene trabajar con un usuario sin privilegios de administrador y recurrir a los permisos elevados solo cuando haga falta, igual que se aplica el principio de mínimo privilegio en cualquier sistema.

**Nombre del equipo y red.** El nombre del equipo debe seguir la nomenclatura de la organización, y la configuración de red (automática por DHCP o manual) se ajusta al entorno.

## 5. Configurar un gestor de arranque (criterio e)

El **gestor de arranque** es el pequeño programa que el firmware ejecuta al encender el equipo y cuya misión es **cargar el sistema operativo** en memoria. Cuando solo hay un sistema instalado casi no se nota; cuando hay varios, el gestor de arranque es quien presenta el menú para elegir entre ellos.

La secuencia, de forma resumida, es esta: el equipo se enciende, el firmware (BIOS o UEFI) hace una comprobación del hardware, busca un dispositivo de arranque según el orden configurado, ejecuta el gestor de arranque que encuentra y este carga el núcleo del sistema.

Los gestores más habituales son:

- **Windows Boot Manager**, el gestor de Windows.
- **GRUB**, el gestor habitual en las distribuciones Linux, muy configurable.

El caso que más enseña es el **arranque dual** (*dual boot*): dos sistemas instalados en el mismo equipo. Hay una regla práctica importante: **se instala primero Windows y después Linux**, porque el instalador de Linux detecta a Windows y lo añade al menú de GRUB, mientras que el instalador de Windows ignora otros sistemas y puede dejarlos inaccesibles al sobrescribir el gestor de arranque. Si esto ocurre, el sistema Linux no se ha perdido: basta con reparar o reinstalar GRUB desde un medio *Live*.

Configurar el gestor de arranque significa, por ejemplo, decidir **qué sistema arranca por defecto**, **cuánto tiempo espera el menú** antes de arrancarlo y **en qué orden** se muestran las opciones. También se incluye la configuración del **orden de dispositivos de arranque** en el firmware, que es lo que permite arrancar desde el USB para realizar la instalación.

## 6. Describir las incidencias de la instalación (criterio f)

Las instalaciones no siempre salen bien a la primera, y un técnico competente sabe **diagnosticar, resolver y documentar** lo ocurrido. Documentar es una parte profesional del trabajo: la incidencia resuelta hoy será la que alguien vuelva a encontrar dentro de seis meses.

Algunas incidencias frecuentes:

| Síntoma | Causa habitual | Línea de actuación |
|---|---|---|
| El equipo no arranca desde el USB | Orden de arranque incorrecto, o el USB está creado para otro modo de arranque (BIOS/UEFI) | Revisar el firmware y recrear el USB |
| El instalador no ve el disco | Controlador de almacenamiento no incluido o modo del disco en el firmware | Cargar el controlador o cambiar el modo en el firmware |
| La instalación se bloquea o da errores aleatorios | ISO corrupta o memoria defectuosa | Comprobar el *hash* de la ISO y probar la RAM |
| El sistema instalado no arranca | Gestor de arranque mal instalado o esquema MBR/GPT incoherente | Reparar el gestor de arranque desde un medio de recuperación |
| Tras instalar no hay red, sonido o vídeo correcto | Faltan controladores | Instalar los controladores del fabricante |
| Tras el arranque dual, un sistema desaparece del menú | El gestor de arranque fue sobrescrito | Reparar o reinstalar el gestor de arranque |

Para **describir** una incidencia conviene seguir siempre el mismo esquema: *qué ocurrió* (el síntoma, con el mensaje de error si lo hay), *en qué momento*, *cuál fue la causa* y *cómo se resolvió*. Hay que anotar también lo que se probó y no funcionó, porque ahorra tiempo en el futuro.

## 7. Respetar las normas de utilización del software: licencias (criterio g)

Cuando alguien instala un programa no se hace dueño de él: obtiene el **derecho de usarlo** bajo unas condiciones, que son las de la **licencia**. Usar software sin respetar su licencia es una infracción legal, y en un entorno profesional puede acarrear sanciones a la empresa.

Conviene distinguir los grandes tipos:

- **Software propietario (privativo):** se paga por el derecho de uso y no se puede modificar ni redistribuir. Dentro de él hay varias modalidades:
  - **Licencia OEM:** viene asociada al equipo con el que se vende y no se puede transferir a otro.
  - **Licencia *retail* (venta al público):** se compra por separado y, en general, se puede pasar a otro equipo (aunque solo se use en uno a la vez).
  - **Licencia por volumen:** pensada para organizaciones que necesitan muchos equipos con un único contrato.
- **Software libre:** garantiza al usuario cuatro libertades: usarlo para cualquier fin, estudiar cómo funciona, redistribuirlo y mejorarlo. Linux se distribuye con licencias de este tipo (por ejemplo, la GPL). **Libre no significa necesariamente gratis**, aunque habitualmente lo sea.
- **Software de código abierto (*open source*):** pone el acento en la disponibilidad del código fuente; en la práctica coincide en gran medida con el software libre.
- ***Freeware*:** se puede usar gratis, pero no se tiene acceso al código ni derecho a modificarlo.
- ***Shareware* y versiones de evaluación:** se pueden probar durante un tiempo limitado o con funciones recortadas antes de pagar.

Las licencias se materializan en la práctica mediante **claves de producto**, **activación** y **contratos**. Una organización seria mantiene un **inventario de licencias** que permita saber qué se ha comprado, para cuántos equipos y cuándo caduca. Cumplir las normas también significa leer y aceptar el **acuerdo de licencia** que aparece durante la instalación, en lugar de pulsar «Acepto» sin más.

## 8. Actualizar el sistema operativo (criterio h)

Un sistema recién instalado **no está terminado**: las imágenes de instalación se preparan semanas o meses antes de que las usemos, y en ese tiempo han aparecido correcciones. Actualizar inmediatamente después de instalar y mantener el sistema al día es una de las tareas de seguridad más eficaces.

Las actualizaciones se agrupan en varios tipos:

- **Actualizaciones de seguridad:** corrigen vulnerabilidades. Son las más urgentes.
- **Correcciones de errores:** solucionan fallos de funcionamiento.
- **Actualizaciones de controladores:** mejoran la compatibilidad con el hardware.
- **Actualizaciones de versión (*upgrade*):** pasan a una versión mayor del sistema. Son más delicadas y conviene planificarlas y hacer copia de seguridad antes.

Cada sistema ofrece su propio mecanismo. En **Windows** se gestiona con *Windows Update*, que permite controlar cuándo se reinicia el equipo. En **Linux** se utiliza el **gestor de paquetes** de la distribución: en las derivadas de Debian, `sudo apt update` actualiza la lista de paquetes disponibles y `sudo apt upgrade` instala las nuevas versiones. Merece la pena entender la diferencia: la primera orden solo *consulta* qué hay de nuevo y la segunda *aplica* los cambios.

Hay que prever también que algunas actualizaciones **requieren reiniciar**, y que en un entorno profesional es habitual **probar las actualizaciones en un equipo piloto** antes de extenderlas al resto, porque una actualización puede, en ocasiones, causar problemas de compatibilidad.

Un último aspecto es el **fin del soporte**: cuando un sistema deja de recibir actualizaciones, seguirlo usando supone un riesgo creciente. Planificar la migración antes de que llegue esa fecha forma parte de la selección del sistema operativo (apartado 2).

---

## 9. Instalación masiva: clonación de equipos (criterios c, d y h)

Todo lo anterior describe la instalación de **un** equipo. Pero en un aula con treinta ordenadores, en una oficina que renueva su parque informático o en un taller que prepara equipos para entregar a clientes, repetir el asistente de instalación treinta veces es lento y, además, poco fiable: cada instalación manual puede salir con alguna pequeña diferencia (un programa olvidado, una opción distinta). Para estos casos se usan **procedimientos de instalación masiva**, y el más extendido es la **clonación**.

La idea es sencilla: se instala, configura y actualiza **un único equipo de referencia** hasta dejarlo exactamente como se quiere; después se captura su contenido y se copia en el resto de equipos. Si has clonado alguna vez una máquina virtual, ya conoces el concepto; la clonación de equipos físicos es lo mismo a mayor escala y con algunas precauciones adicionales.

### Clonar o crear una imagen

Aunque a menudo se usan como sinónimos, conviene distinguir dos formas de trabajar:

- La **clonación** copia directamente un disco (o una partición) sobre otro. Es cómoda para duplicar un equipo concreto.
- La **imagen de disco** guarda el contenido del disco en un **archivo** que se puede almacenar y restaurar tantas veces como se quiera, en equipos distintos. Es la forma habitual de trabajo en una instalación masiva, porque la imagen se crea una vez y se reutiliza. Al equipo de referencia con el que se crea se le llama **imagen maestra** (o *golden image*).

### Procedimiento

Un despliegue por imagen sigue estas fases, que encajan con el plan de instalación del apartado 3:

1. **Preparar el equipo de referencia.** Se instala el sistema, se aplican las actualizaciones, se instala el software común y se configuran los parámetros que serán iguales para todos (apartado 4). No debe contener datos personales ni contraseñas reales.
2. **Generalizar la imagen.** Es el paso que más se olvida y el que más problemas evita (se explica más abajo).
3. **Capturar la imagen** con la herramienta elegida y guardarla en un almacenamiento accesible.
4. **Desplegar la imagen** en los equipos de destino, de uno en uno o varios a la vez.
5. **Personalizar cada equipo.** Cada uno necesita, como mínimo, su propio nombre y, según el caso, usuarios o configuración de red específicos.
6. **Verificar** que los equipos arrancan, funcionan y quedan correctamente identificados.
7. **Mantener la imagen.** Con el tiempo la imagen se queda desfasada: hay que actualizarla (apartado 8) y volver a capturarla, en lugar de actualizar los equipos uno por uno después de desplegar.

### El problema de las identidades duplicadas

Un sistema recién instalado genera información que lo identifica de forma **única**. Si se copia tal cual a otros equipos, todos quedan con la misma identidad, y eso provoca fallos reales:

- En **Windows**, cada instalación tiene un identificador de seguridad (SID). Por eso Microsoft exige preparar la imagen con la herramienta **Sysprep** y la opción de *generalizar* antes de capturarla: esta orden elimina la información única de la instalación para que la imagen se pueda reutilizar en otros equipos, y debe hacerse incluso si el hardware de destino es idéntico. Microsoft no da soporte a equipos desplegados con otras herramientas que dupliquen el SID. Para capturar la imagen ya generalizada se puede usar, por ejemplo, la orden `DISM /capture-image`.
- En **Linux**, el sistema guarda un identificador propio de la máquina (`/etc/machine-id`) y genera claves de servidor SSH únicas. Si se duplican, los equipos pueden presentarse en la red con la misma identidad (incluso recibir la misma dirección IP del servidor DHCP) y compartir una clave que debería ser secreta y exclusiva de cada equipo. Antes de capturar la imagen se deben limpiar esos datos y dejar que cada clon genere los suyos al arrancar. También hay que dar a cada clon un nombre de equipo distinto.

La regla práctica es: **antes de copiar, preguntarse qué información de este equipo debe ser única**, y eliminarla o regenerarla.

### Herramientas habituales

**Clonezilla** es un software libre (licencia GPL) de clonación e imágenes de disco muy utilizado en educación. Tiene dos variantes: *Clonezilla Live*, pensada para trabajar con un solo equipo, y *Clonezilla Server Edition* (y su versión *lite server*), pensada para el despliegue masivo en red. Una de sus ventajas es que solo copia los bloques del disco que contienen datos, lo que acorta los tiempos. Se puede arrancar desde USB, DVD o por red.

Otras soluciones, como **FOG**, ofrecen también despliegue de imágenes por red. En el entorno Windows, el propio sistema incluye herramientas de captura y aplicación de imágenes (como DISM), y los instaladores permiten además la **instalación desatendida** mediante un archivo de respuestas, una alternativa a la clonación que no copia un equipo ya instalado, sino que automatiza las respuestas del asistente. Las distribuciones Linux ofrecen mecanismos equivalentes (por ejemplo, *preseed* en Debian, *autoinstall* en Ubuntu o *kickstart* en la familia Red Hat).

### Despliegue por red

Cuando son muchos equipos, llevar un USB a cada uno no es práctico. Lo habitual es arrancar los equipos **por red** mediante **PXE** (que exige activar el arranque por red en el firmware, tal como se vio en el apartado 5): el equipo obtiene su dirección por DHCP, descarga un pequeño sistema de arranque desde el servidor y restaura la imagen sin intervención. Si el servidor envía la imagen en **multicast**, un único flujo de datos sirve a todos los equipos a la vez, en lugar de enviar una copia distinta a cada uno. Para que funcione bien conviene usar **red cableada** (el arranque por PXE y el multicast son poco fiables por Wi-Fi), que servidor y equipos estén en la misma red local y que los dispositivos de red permitan el tráfico multicast.

### Ventajas y precauciones

| Ventajas | Precauciones |
|---|---|
| Ahorro enorme de tiempo en grandes grupos de equipos | La imagen debe prepararse (generalizarse) antes de capturarla |
| Todos los equipos quedan idénticos y configurados igual | Hardware muy distinto entre equipos puede requerir controladores adicionales o varias imágenes |
| Se vuelve al estado inicial con rapidez si un equipo falla o se estropea | El disco de destino debe ser suficiente para el contenido de la imagen |
| Reduce los errores humanos de la instalación manual | Hay que mantener la imagen actualizada y probar siempre la restauración |

Hay además un aspecto legal que no se debe olvidar (apartado 7): **clonar un equipo no elimina la necesidad de tener una licencia válida para cada copia instalada**. Las licencias OEM están ligadas al equipo original y las de volumen son las pensadas para este tipo de despliegues en organizaciones. Por último, en entornos Windows corporativos no debe clonarse un equipo que ya esté unido a un dominio en la nube o gestionado por un sistema de administración de dispositivos: la imagen maestra debe mantenerse limpia, sin unir, y generalizarse antes de capturarla.

---

## Resumen del proceso

| Fase | Pregunta clave | Criterio |
|---|---|---|
| Antes | ¿Sirve este equipo? | a |
| Antes | ¿Qué sistema conviene y por qué? | b |
| Antes | ¿Qué voy a hacer, en qué orden y con qué plan B? | c |
| Durante | ¿Qué decisiones debo tomar en el asistente? | d |
| Durante | ¿Cómo arranca el equipo y qué sistema se carga? | e |
| Durante | ¿Qué hago si algo falla? | f |
| Siempre | ¿Tengo derecho a usar este software? | g |
| Después | ¿Está el sistema al día? | h |
| Varios equipos | ¿Puedo preparar una vez y copiar al resto? | c, d, h |

---

## Bibliografía y enlaces de consulta

Estas son las fuentes en las que se apoyan los contenidos de este documento. Se recomienda consultar siempre la documentación oficial, porque requisitos, versiones y fechas de soporte cambian con el tiempo.

### Requisitos de hardware y selección del sistema (criterios a, b)

- Microsoft. *Requisitos de Windows 11* (UEFI con Secure Boot, TPM 2.0, memoria y almacenamiento mínimos): <https://learn.microsoft.com/windows/whats-new/windows-11-requirements>
- Canonical. *Ciclo de lanzamientos de Ubuntu* (versiones LTS cada dos años y cinco años de mantenimiento de seguridad estándar): <https://ubuntu.com/about/release-cycle>
- Canonical. *Versiones de Ubuntu* (qué es una versión LTS y cómo se organiza el soporte): <https://ubuntu.com/project/docs/release-team/ubuntu-releases/>

### Gestor de arranque y arranque dual (criterio e)

- Comunidad Ubuntu. *Arranque dual con Windows* (por qué conviene instalar primero Windows): <https://help.ubuntu.com/community/DualBoot/Windows>
- Comunidad Ubuntu. *Arranque dual: instalar primero Windows* (GRUB y arranque de Windows): <https://help.ubuntu.com/community/DualBoot/WindowsFirst>
- OneUptime. *How to Dual Boot Ubuntu and Windows 11 Without Losing Data* (fuente secundaria; GRUB y la partición EFI compartida, reparación de GRUB desde un medio Live): <https://oneuptime.com/blog/post/2026-03-02-dual-boot-ubuntu-windows-11-without-losing-data/view>

### Licencias (criterio g)

- Proyecto GNU. *¿Qué es el software libre?* (las cuatro libertades; libre no significa gratis): <https://www.gnu.org/philosophy/free-sw.html>
- Free Software Foundation Europe. *What is Free Software?* (explicación divulgativa y relación con «código abierto»): <https://fsfe.org/freesoftware/>
- Microsoft. *Licensing Logic: What's the difference between OEM, Retail and Volume Licenses?* (tipos de licencia de Windows y derechos de transferencia): <https://learn.microsoft.com/en-us/archive/blogs/uktechnet/licensing-logic-whats-the-difference-between-oem-retail-and-volume-licenses>
- Windows Central. *How to determine if your Windows 11 (or 10) license type is OEM, Retail, or Volume* (fuente secundaria): <https://www.windowscentral.com/how-determine-if-license-oem-retail-volume-windows-10>

### Actualización del sistema (criterio h)

- Linuxize. *apt update vs apt upgrade vs apt full-upgrade* (diferencia entre actualizar la lista de paquetes y actualizar los paquetes; `apt upgrade` no elimina paquetes instalados): <https://linuxize.com/post/apt-update-vs-upgrade/>
- Debian. *The Debian Administrator's Handbook*, sección sobre APT (actualizaciones periódicas y `apt full-upgrade` para cambios de versión mayor): <https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.ko.html>

### Instalación masiva y clonación (criterios c, d, h)

- Microsoft. *Sysprep (Generalize) a Windows installation* (qué elimina `/generalize` y captura de la imagen con DISM): <https://learn.microsoft.com/es-es/previous-versions/windows/it-pro/windows-8.1-and-8/hh824938(v=win.10)>
- Microsoft. *generalize* (pasada de configuración que elimina datos únicos como el SID): <https://technet.microsoft.com/en-us/library/hh824983>
- Microsoft. *Sysprep will not run correctly on a Windows 10 device that has been MDM enrolled* (obligación de usar Sysprep al clonar, soporte y precauciones con equipos unidos a Entra ID o gestionados por MDM): <https://docs.microsoft.com/en-us/troubleshoot/mem/intune/troubleshoot-sysprep-windows-10-device-enrolled-mdm>
- Proyecto Clonezilla. *Página oficial* (variantes Live y servidor, multicast, BitTorrent): <https://clonezilla.org/>
- Proyecto Clonezilla. *Clonezilla live doc* (guías paso a paso, incluido el despliegue masivo con lite server): <https://clonezilla.org/clonezilla-live-doc.php>
- Endless OS. *Clonezilla: massive deployment* (arranque PXE y restauración automática de la imagen; servidor y clientes en la misma red local): <https://support.endlessos.org/en/installation/clonezilla/massive-deployment>
- Ubicloud. *Generalize a machine image* (identificadores que deben ser únicos en Linux: claves SSH, machine-id): <https://www.ubicloud.com/docs/machine-images/generalize>
- OneUptime. *How to Stop a Cloned Photon OS VM from Reusing Its DHCP Identity* (fuente secundaria; el `machine-id` duplicado y su efecto en el identificador DHCP): <https://oneuptime.com/blog/post/2026-09-18-photon-clone-dhcp-identity/view>
- CBackup. *How to Image Multiple Computers at Once* (fuente secundaria; Wi-Fi poco fiable para PXE y multicast, FOG y Clonezilla SE): <https://www.cbackup.com/best/how-to-image-multiple-computers-at-once-2578-iw.amp.html>

### Notas sobre las fuentes

- Los apartados de **incidencias de la instalación** (criterio f) y la **estructura del plan de instalación** (criterio c) son una síntesis de buenas prácticas del propio autor del material y no proceden de una única fuente.
- En el apartado 9, lo relativo a las herramientas de instalación desatendida (*preseed*, *autoinstall*, *kickstart*) y a FOG procede del conocimiento general del autor o de fuentes secundarias, y conviene contrastarlo con la documentación oficial de cada proyecto antes de usarlo en clase.
- Las fuentes marcadas como *secundarias* son artículos divulgativos: sirven como ejemplo práctico, pero la referencia oficial prevalece en caso de discrepancia.
