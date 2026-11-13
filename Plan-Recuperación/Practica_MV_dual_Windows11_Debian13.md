# Práctica: máquina virtual de arranque dual con Windows 11 y Debian 13

---

## 1. Presentación

Imagina que eres el técnico de una pequeña empresa de formación. El responsable te encarga preparar un equipo de pruebas en el que el profesorado pueda comprobar, en un mismo ordenador, cómo se comportan Windows 11 y Debian 13. No hay presupuesto para un segundo equipo, así que montarás ese equipo como una **máquina virtual (MV) con arranque dual**: un único disco virtual con los dos sistemas instalados y un gestor de arranque que permita elegir con cuál iniciar.

El trabajo no consiste solo en instalar. Consiste en **planificar** antes de tocar nada, **instalar** tomando decisiones razonadas, **comprobar** que todo funciona y **documentar** el proceso de modo que otra persona pueda repetirlo. Esa documentación es lo que se evalúa.

Esta práctica está diseñada para hacerse sin ayuda directa. Por eso cada fase termina con un **punto de control**: una serie de comprobaciones que te dicen si puedes seguir adelante o si debes corregir algo antes. Si un punto de control no se cumple, no avances: consulta la guía de problemas del apartado 11 y, si el problema persiste, consulta con el profesor.

---

## 2. Cómo trabajar esta práctica

**Lee cada fase completa antes de empezar a hacerla.** Muchas decisiones (por ejemplo, cómo se reparte el disco) condicionan pasos posteriores y no siempre se pueden deshacer sin empezar de nuevo.

**Personaliza todo con tus iniciales.** Toma la inicial de tu nombre y las dos primeras letras de tu primer apellido (por ejemplo, *Ana López* → `alo`) y úsalas en los nombres que verás a continuación. Es imprescindible: las capturas en las que no aparezcan tus nombres personalizados no se tendrán en cuenta.

| Elemento | Nombre que debes usar |
|---|---|
| Nombre de la MV en VirtualBox | `SOM_DUAL_xxx` |
| Nombre del equipo en Windows | `WIN11-xxx` |
| Usuario en Windows y en Debian | `som_xxx` |
| Nombre del equipo (hostname) en Debian | `deb13-xxx` |

(Sustituye `xxx` por tus iniciales). Elige contraseñas que recuerdes, pero **no las incluyas en el informe**.

**Usa instantáneas como red de seguridad.** Una instantánea (*Máquina → Tomar instantánea*) guarda el estado exacto de la MV en un momento dado y permite volver a él si algo sale mal. En esta práctica se te indica cuándo tomar cada una. Si tienes que revertir, hazlo sin miedo: es precisamente para eso.

**Guarda las evidencias según avanzas.** Hacer las capturas después, de memoria, es mucho más costoso que hacerlas en el momento. En el apartado 12 tienes la lista numerada de capturas (C1 a C12) que debes reunir. En el informe debes explicar lo que muestra cada una, no solo pegarla.

**Crea un fichero de verificación en cada sistema.** Cuando tengas escritorio en Windows y en Debian, crea en cada uno un fichero de texto llamado `verificacion.txt` con tu nombre completo, la fecha del día y el nombre del sistema operativo. Aparecerá en algunas capturas y sirve para demostrar que el trabajo es tuyo.

---

## 3. Requisitos y descargas

### Equipo anfitrión

Necesitas un ordenador con al menos **8 GB de RAM** (le cederás 4 GB a la MV), un procesador con la **virtualización activada en la BIOS/UEFI** (se llama VT-x en Intel y AMD-V o SVM en AMD) y unos **60 GB de disco libre**. El disco virtual será de 80 GB, pero se crea con tamaño dinámico, es decir, solo ocupa en el equipo real el espacio que realmente se va usando (al terminar, entre 25 y 35 GB aproximadamente).

Si el equipo no cumple los requisitos, díselo al profesor antes de empezar y no intentes forzar la instalación con menos recursos.

### Software

- **VirtualBox 7.x** (no hace falta el Extension Pack para esta práctica).
- **ISO de Windows 11** (x64), desde la web oficial de Microsoft. Es una descarga gratuita; sin clave de producto el sistema funciona con algunas limitaciones (ver apartado 10).
- **ISO de Debian 13** («Trixie»), imagen `netinst` para amd64, desde debian.org. El instalador descargará los paquetes de Internet durante la instalación, por lo que necesitarás conexión.

Los enlaces concretos están en el apartado 14. Descarga las dos ISO antes de comenzar y comprueba que el tamaño del fichero descargado es coherente con el indicado en la web (una descarga cortada es una causa frecuente de errores de instalación).

---

## 4. Fase 0: análisis y plan de instalación

Antes de crear nada, tienes que decidir qué vas a instalar y con qué recursos. Esta fase no se hace en VirtualBox, se hace en tu informe.

### 4.1. Requisitos de hardware

Busca en las fuentes oficiales los requisitos mínimos de Windows 11 y los de Debian 13 y completa esta tabla en el informe. En la última columna escribe el valor que asignarás a la MV y justifica por qué es suficiente (o por qué decides dar más que el mínimo).

| Requisito | Windows 11 (mínimo) | Debian 13 con escritorio (mínimo recomendado) | Valor asignado a la MV |
|---|---|---|---|
| Procesador (núcleos) | | | |
| Memoria RAM | | | |
| Espacio en disco | | | |
| Firmware de arranque | | | |
| Otros (TPM, arranque seguro…) | | | |

Presta atención especial a la fila del firmware. Windows 11 exige un equipo con **UEFI** y puede exigir **TPM 2.0** y **arranque seguro**. Esto condiciona cómo se debe crear la MV (fase 1) y, como verás en la fase 4, también cómo funciona el arranque dual.

### 4.2. Selección del sistema operativo

Responde en el informe, con tus palabras y en un párrafo para cada punto:

1. ¿Qué edición de Windows 11 vas a instalar (Home, Pro…) y por qué? ¿En qué se diferencian las ediciones que te ofrece el instalador?
2. ¿Qué entorno de escritorio vas a elegir en Debian (GNOME, Xfce…) y qué implica en consumo de recursos?
3. ¿Qué ventajas y qué riesgos tiene hacer un arranque dual en una máquina virtual frente a hacerlo en un ordenador real?

### 4.3. Esquema de particiones

El disco virtual tendrá **80 GB**. Windows se instalará primero y ocupará unos **50 GB**; el resto quedará sin asignar para que Debian lo use después. Dibuja o describe un esquema con el orden de las particiones previsto (partición de arranque EFI, partición de Windows, partición raíz de Debian, swap…) y explica **por qué Windows se instala antes que Linux** y no al revés. Pista: piensa en qué hace el instalador de Windows con el gestor de arranque que encuentra en el disco.

### Punto de control 0

- [ ] La tabla de requisitos está completa con fuentes consultadas.
- [ ] Has respondido las tres preguntas de selección.
- [ ] Tienes un esquema de particiones con su justificación.

---

## 5. Fase 1: creación de la MV (UEFI, TPM y disco)

Crea la máquina virtual con *Máquina → Nueva*. La práctica trata de instalar el sistema a mano, de modo que debes **marcar la casilla «Skip Unattended Installation»** (omitir la instalación desatendida). Si no lo haces, VirtualBox instalará Windows por ti y te perderás casi todo lo que se evalúa.

| Parámetro | Valor |
|---|---|
| Nombre | `SOM_DUAL_xxx` |
| Imagen ISO | La de Windows 11 |
| Tipo / versión | Microsoft Windows / Windows 11 (64-bit) |
| Memoria base | 4096 MB |
| Procesadores | 2 |
| Disco duro virtual | 80 GB, formato VDI, **tamaño dinámico** (no marques «Pre-Allocate Full Size») |

Cuando termines el asistente, abre *Configuración* y comprueba tú mismo, sin fiarte de que el asistente lo haya hecho, estos ajustes:

- **Sistema → Placa base:** debe estar activada la opción **EFI**, el **TPM** debe estar en versión **2.0** y, si tu versión de VirtualBox la ofrece, debe estar activado el **arranque seguro** (*Secure Boot*).
- **Pantalla:** memoria de vídeo al máximo permitido (mejora la fluidez del escritorio).
- **Red:** adaptador 1 en modo **NAT**. Es el modo más sencillo y suficiente para que la MV tenga Internet.
- **Almacenamiento:** la ISO de Windows debe estar en la unidad óptica.

### Por qué importa el firmware

Una BIOS clásica y un firmware UEFI arrancan de forma distinta. La BIOS clásica busca un cargador en el primer sector del disco (esquema de particiones MBR); el UEFI busca ficheros de arranque en una partición especial, la **partición de sistema EFI (ESP)**, en un disco con esquema **GPT**. Como crearás la MV con EFI, el disco será GPT y los dos sistemas compartirán esa partición ESP. Guarda esta idea, porque la necesitarás en la fase 4.

### Punto de control 1

- [ ] En la configuración de la MV se ve EFI activado y TPM 2.0 (**captura C1**, con el nombre `SOM_DUAL_xxx` visible).
- [ ] La instalación desatendida está desactivada.

---

## 6. Fase 2: instalación de Windows 11

Arranca la MV. El instalador de Windows puede mostrar durante un instante el mensaje *«Press any key to boot from CD or DVD»*: pulsa una tecla.

Sigue el asistente tomando estas decisiones, que debes anotar para el informe:

1. **Idioma, formato de hora y teclado:** español (España).
2. **Clave de producto:** elige **«No tengo clave de producto»**. No uses claves de procedencia dudosa.
3. **Edición:** la que hayas decidido en la fase 0.
4. **Tipo de instalación:** *Personalizada: instalar solo Windows (avanzado)*.
5. **Particionado:** verás un único bloque de 80 GB sin asignar. Pulsa **Nuevo** y escribe un tamaño de **51200 MB** (50 GB). Windows avisará de que puede crear particiones adicionales para los archivos del sistema; acepta. Instala en la partición principal que se haya creado, **no** en el espacio restante. Haz la **captura C2** de esta pantalla antes de continuar.
6. **Configuración inicial (OOBE):** nombre del equipo `WIN11-xxx` y usuario `som_xxx`. Si el asistente se empeña en pedirte una cuenta Microsoft, consulta el apartado 11.

Los reinicios durante la instalación son normales. Si tras alguno vuelve a aparecer el mensaje de «pulsar una tecla», **no pulses nada** y deja que arranque desde el disco.

### Tras la instalación

Con el escritorio ya disponible:

1. **Guest Additions:** en el menú de la MV, *Dispositivos → Insertar imagen de CD de las Guest Additions*. Abre la unidad desde el Explorador, ejecuta `VBoxWindowsAdditions.exe` y reinicia. Esto mejora la resolución, el portapapeles y el rendimiento gráfico.
2. **Actualizaciones:** abre *Windows Update*, instala las pendientes y reinicia las veces necesarias (**captura C6** con el resultado «Estás al día» o equivalente).
3. **Comprobaciones:**
   - Ejecuta `winver` (**captura C3**, con `verificacion.txt` abierto o el comando `type verificacion.txt` en una consola, y el nombre del equipo visible).
   - Ejecuta `msinfo32` y localiza «Modo de BIOS» y «Estado de arranque seguro» (**captura C4**).
   - Ejecuta `diskmgmt.msc` y comprueba que quedan unos 30 GB **sin asignar** al final del disco (**captura C5**).
4. **Apaga** la MV por completo (no la suspendas) y **toma una instantánea** llamada `01_Windows_instalado`.

### Punto de control 2

- [ ] Windows arranca sin errores y muestra tu nombre de equipo.
- [ ] `msinfo32` indica modo UEFI.
- [ ] Queda espacio sin asignar en el disco.
- [ ] Existe la instantánea `01_Windows_instalado`.

---

## 7. Fase 3: instalación de Debian 13 en el espacio libre

Con la MV apagada, en *Configuración → Almacenamiento* sustituye la ISO de Windows por la de Debian (haz clic en el disco de la unidad óptica y elige el fichero). **No crees una MV nueva**: Debian se instala en el mismo disco, junto a Windows.

Arranca la MV. Debería iniciarse el menú del instalador de Debian. Si arranca Windows en su lugar, consulta el apartado 11.

Elige *Graphical install* y ve tomando estas decisiones:

1. **Idioma, país y teclado:** español, España.
2. **Nombre de equipo:** `deb13-xxx`. Deja el dominio en blanco.
3. **Contraseña de root:** **déjala en blanco**. Con esto se desactiva la cuenta de superusuario y tu usuario normal usará `sudo` para tareas administrativas, que es la práctica recomendada. Explica en el informe qué ventaja de seguridad tiene.
4. **Usuario:** nombre completo (el tuyo), nombre de usuario `som_xxx` y una contraseña.
5. **Zona horaria:** la correspondiente a España peninsular.
6. **Particionado:** elige **«Guiado: usar el mayor espacio libre contiguo»** y, después, «Todos los ficheros en una partición». El instalador te mostrará una tabla con las particiones de Windows (que **no debes tocar**) y las nuevas de Debian (raíz en ext4 y swap). Comprueba que reutiliza la partición EFI existente y haz la **captura C7** *antes* de aceptar «Finalizar el particionado y escribir los cambios en el disco». Fíjate bien: este es el paso con más riesgo de borrar Windows por error si eliges el disco completo en vez del espacio libre.
7. **Gestor de paquetes:** réplica en España (`deb.debian.org` funciona bien). Sin proxy.
8. **Selección de software:** deja marcados *Entorno de escritorio Debian*, el escritorio que hayas elegido y *Utilidades estándar del sistema*. Haz la **captura C8**.
9. **GRUB:** acepta instalar el cargador de arranque; en UEFI se instala en la partición EFI.

Cuando termine, reinicia. VirtualBox suele expulsar la ISO automáticamente; si te vuelve a arrancar el instalador, extráela manualmente desde *Dispositivos → Unidades ópticas*.

### Tras la instalación

Inicia sesión en Debian y abre una terminal. Haz las siguientes comprobaciones y **actualiza el sistema**:

```bash
cat /etc/os-release
hostname
lsblk -f
sudo apt update
sudo apt full-upgrade
```

Crea `verificacion.txt` con tu nombre y la fecha y muéstralo con `cat verificacion.txt`. La **captura C10** debe incluir la salida de `cat /etc/os-release`, `hostname` y `lsblk -f` en la misma terminal. La **captura C12** muestra el resultado de la actualización (por ejemplo, `apt list --upgradable` sin paquetes pendientes tras terminar).

### Punto de control 3

- [ ] Debian arranca con tu nombre de equipo y tu usuario.
- [ ] `lsblk -f` muestra las particiones de Windows y las de Debian en el mismo disco.
- [ ] El sistema está actualizado.

---

## 8. Fase 4: comprobación del arranque dual

Apaga la MV por completo y vuelve a encenderla. Debes ver el **menú de GRUB**, en el que aparecen, como mínimo, *Debian GNU/Linux* y *Windows Boot Manager*. Haz la **captura C9** de ese menú. Arranca después cada sistema, uno cada vez, y comprueba que funcionan.

Ahora explica en el informe, con tus palabras, qué has hecho. Estas preguntas te guían:

1. ¿Qué programa muestra el menú al encender la MV y dónde está instalado físicamente?
2. ¿Qué papel juega la partición EFI en el arranque de los dos sistemas? ¿Por qué es compartida?
3. ¿Qué ocurriría si Windows se reinstalase más adelante? ¿Y si se borrase la partición de Debian?

Para respaldar tus respuestas, en Debian ejecuta estos comandos y haz la **captura C11**:

```bash
sudo apt install efibootmgr
sudo efibootmgr -v
ls /boot/efi/EFI
```

Fíjate en cuántas entradas de arranque aparecen y en la carpeta de cada sistema dentro de `EFI`.

**Una comprobación extra que suele dar sorpresas:** compara la hora que muestra cada sistema. Si no coinciden, no es un fallo de la MV: investiga por qué (pista: los sistemas no interpretan igual el reloj de la placa base) y anota la causa y la solución como una incidencia en la fase 5.

### Punto de control 4

- [ ] GRUB muestra las dos entradas al arrancar.
- [ ] Los dos sistemas arrancan desde GRUB.
- [ ] Has respondido las tres preguntas.

Toma una instantánea final llamada `02_Dual_completo`.

---

## 9. Fase 5: registro de incidencias y actualizaciones

Durante la práctica habrás encontrado errores, avisos o decisiones dudosas. Reúnelas en una tabla en el informe. Es tan importante como la instalación en sí: un técnico que documenta sus problemas y sus soluciones ahorra tiempo al siguiente.

| N.º | Fase | Síntoma (qué pasó) | Causa | Solución aplicada | Fuente consultada |
|---|---|---|---|---|---|

Debes incluir **al menos dos incidencias**. Si de verdad no has tenido ninguna, elige dos de la guía del apartado 11, descríbelas con tus palabras y explica cómo las habrías resuelto. Añade también una breve conclusión sobre el proceso de actualización de cada sistema: cómo se actualiza Windows, cómo se actualiza Debian y qué diferencias has observado.

---

## 10. Reflexión sobre licencias

Responde en el informe, con un párrafo breve por pregunta:

1. Tu Windows no está activado. ¿Qué limitaciones tiene un Windows 11 sin activar y por qué no es adecuado, por ejemplo, para uso empresarial?
2. ¿Qué diferencias hay entre una licencia comercial (*retail*), una OEM y una de volumen? ¿Cuál se usaría en un aula con 30 equipos?
3. ¿Bajo qué tipo de licencia se distribuye Debian? ¿Qué te permite hacer con ese software que no puedes hacer con Windows?

---

## 11. Guía de resolución de problemas

Antes de pedir ayuda, busca aquí tu síntoma. Si la solución no aparece o no funciona, consulta las fuentes oficiales y documenta lo que hiciste.

| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| Windows indica «Este equipo no puede ejecutar Windows 11» | La MV no tiene EFI, TPM 2.0 o arranque seguro | Apaga la MV, revisa *Sistema → Placa base* y repite el arranque. Solo como último recurso y documentándolo, existe un método para omitir las comprobaciones durante la instalación: busca «LabConfig BypassTPMCheck» |
| El instalador de Windows obliga a usar una cuenta Microsoft o a conectarse a Internet | Comportamiento del asistente inicial de Windows 11, que cambia según la versión | Opciones: desconectar temporalmente el cable de red en *Configuración → Red → Avanzado → Cable conectado*; usar el comando `OOBE\BYPASSNRO` desde una consola abierta con `Mayús+F10` (no funciona en todas las versiones); o usar una cuenta Microsoft personal. Busca información actualizada y anota qué método funcionó |
| Al reiniciar, la MV vuelve al instalador de Windows | La ISO sigue montada y se pulsó una tecla en «Press any key…» | No pulses ninguna tecla. Si sigue ocurriendo, extrae la ISO desde *Dispositivos → Unidades ópticas* |
| Al arrancar con la ISO de Debian arranca Windows | El firmware EFI prioriza el disco duro | Al encender, pulsa repetidamente `Esc` (o `F2`) para entrar en el menú del firmware, entra en *Boot Manager* y elige la unidad óptica |
| La ISO de Debian no arranca con el arranque seguro activado | Poco frecuente: configuración de claves del firmware virtual | Desactiva temporalmente el arranque seguro, instala y vuelve a activarlo |
| Al terminar Debian, la MV arranca directamente en Windows y no aparece GRUB | El orden de arranque EFI sitúa primero a Windows Boot Manager | Entra en el menú del firmware (`Esc` o `F2`) → *Boot Manager* y arranca la entrada de Debian; desde Debian, usa `efibootmgr` para ajustar el orden |
| GRUB solo muestra Debian y no Windows | GRUB no ha detectado el otro sistema | En Debian: `sudo apt install os-prober`, edita `/etc/default/grub` y añade (o descomenta) la línea `GRUB_DISABLE_OS_PROBER=false`, y ejecuta `sudo update-grub` |
| La hora no coincide entre Windows y Debian | Windows guarda la hora local en el reloj de la placa y Linux espera UTC | Busca «dual boot time difference Windows Linux» y aplica una solución, anotando cuál escogiste |
| El instalador de Debian no ve el espacio libre | Se eligió un modo de particionado equivocado | Vuelve atrás y elige *Guiado: usar el mayor espacio libre contiguo* |
| El instalador de Debian no encuentra la red o falla la descarga de paquetes | Adaptador sin conexión | Comprueba que el adaptador está en NAT y con cable conectado |
| Todo va muy lento | Poca RAM disponible en el equipo real | Cierra aplicaciones en el anfitrión; no asignes más de la mitad de su RAM a la MV |

---

## 12. Documentación que debes entregar

Entregarás **un único informe en PDF** con el nombre `SOM_Apellido_Nombre_MVdual.pdf`. Debe estar redactado por ti, con capturas propias y con la estructura siguiente:

1. **Portada** con tus datos y el nombre de la MV.
2. **Plan de instalación** (fase 0): tabla de requisitos, selección de sistemas y esquema de particiones.
3. **Creación de la MV** (fase 1): parámetros elegidos y justificación.
4. **Instalación de Windows 11** (fase 2): decisiones tomadas en cada paso y resultado.
5. **Instalación de Debian 13** (fase 3): decisiones tomadas en cada paso y resultado.
6. **Arranque dual** (fase 4): descripción del funcionamiento y respuestas a las preguntas.
7. **Registro de incidencias y actualizaciones** (fase 5).
8. **Reflexión sobre licencias** (apartado 10).

### Capturas obligatorias

| Código | Qué debe mostrar |
|---|---|
| C1 | Configuración de la MV: EFI y TPM 2.0 |
| C2 | Instalador de Windows con la partición de 50 GB creada |
| C3 | `winver` y `verificacion.txt` en Windows, con el nombre del equipo |
| C4 | `msinfo32`: modo de BIOS y arranque seguro |
| C5 | Administración de discos con el espacio sin asignar |
| C6 | Windows Update al día |
| C7 | Particionado de Debian antes de escribir los cambios |
| C8 | Selección de software de Debian |
| C9 | Menú de GRUB con las dos entradas |
| C10 | Terminal de Debian: `os-release`, `hostname`, `lsblk -f` y `verificacion.txt` |
| C11 | `efibootmgr -v` y `ls /boot/efi/EFI` |
| C12 | Debian actualizado (`apt full-upgrade` o `apt list --upgradable`) |

Cada captura debe llevar un pie de figura que indique **qué se ve y qué decisión o comprobación demuestra**. Una captura sin explicación vale poco.

---

## 13. Evaluación

| Aspecto | Puntos |
|---|---|
| Plan de instalación y justificación de decisiones (a, b, c) | 1,5 |
| Creación y configuración correcta de la MV | 1,0 |
| Instalación y parámetros de Windows 11 (d) | 1,5 |
| Instalación y parámetros de Debian 13 (d) | 1,5 |
| Arranque dual comprobado y explicado (e) | 1,5 |
| Incidencias y actualización (f, h) | 1,0 |
| Reflexión sobre licencias (g) | 0,5 |
| Calidad de la documentación: claridad, capturas personalizadas, fuentes | 1,5 |
| **Total** | **10** |

Las capturas que no muestren tus nombres personalizados, o las que sean idénticas a las de otra persona, se considerarán no entregadas.

### Lista de autocomprobación final

Antes de entregar, comprueba:

- [ ] Los dos sistemas arrancan desde el menú de GRUB.
- [ ] Todos los nombres (MV, equipos, usuarios) llevan tus iniciales.
- [ ] Las 12 capturas están incluidas y explicadas.
- [ ] Hay al menos dos incidencias documentadas.
- [ ] Has respondido las preguntas de los apartados 4, 8 y 10.
- [ ] Has citado las fuentes que has consultado.
- [ ] No aparece ninguna contraseña en el informe.

---

## 14. Bibliografía y fuentes recomendadas

- Oracle VirtualBox: descargas y manual de usuario. https://www.virtualbox.org
- Microsoft: descarga de la imagen ISO de Windows 11. https://www.microsoft.com/es-es/software-download/windows11
- Microsoft: especificaciones y requisitos de Windows 11. https://www.microsoft.com/es-es/windows/windows-11-specifications
- Debian: imágenes de instalación (netinst). https://www.debian.org/distrib/netinst
- Debian: Guía de instalación de la versión estable. https://www.debian.org/releases/stable/installmanual
- Debian Wiki: documentación sobre GRUB, UEFI y arranque dual. https://wiki.debian.org
