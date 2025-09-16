# UNIDAD 1: Introducción a los sistemas operativos

## 1. EL SISTEMA INFORMÁTICO

Un **sistema informático** es un conjunto de elementos interrelacionados que trabajan de forma coordinada para procesar información de manera automática. Está compuesto por dos elementos fundamentales:

### 1.1 Hardware
Constituye la parte física del sistema informático. Incluye:
- **Unidad Central de Procesamiento (CPU)**: Ejecuta las instrucciones
- **Memoria principal (RAM)**: Almacena temporalmente datos y programas
- **Memoria secundaria**: Dispositivos de almacenamiento permanente (discos duros, SSD)
- **Dispositivos de entrada**: Teclado, ratón, micrófono, etc.
- **Dispositivos de salida**: Monitor, impresora, altavoces, etc.
- **Dispositivos de entrada/salida**: Pantallas táctiles, dispositivos de red, etc.

![Esquema hardware de un sistema informático](/img/ud1_img1.webp "Esquema hardware de un sistema informático")

### 1.2 Software
Es la parte lógica del sistema informático. Se divide en:
- **Software de sistema**: Programas que gestionan el hardware (sistemas operativos, controladores)
- **Software de aplicación**: Programas que resuelven problemas específicos del usuario
- **Software de programación**: Herramientas para crear otros programas

---

## 2. SOFTWARE DE BASE DE UN SISTEMA INFORMÁTICO

El **software de base** o software de sistema es el conjunto de programas que sirven de interfaz entre el hardware y las aplicaciones de usuario. Sus componentes principales son:

### 2.1 Sistema Operativo
Programa principal que gestiona todos los recursos del sistema y proporciona servicios a otros programas.

### 2.2 Controladores (Drivers)
Programas específicos que permiten al sistema operativo comunicarse con cada dispositivo hardware.

### 2.3 Firmware
Software básico almacenado en memoria no volátil que controla el funcionamiento de bajo nivel del hardware.

### 2.4 Utilidades del Sistema
Programas auxiliares para tareas de mantenimiento, diagnóstico y optimización del sistema.

---

## 3. CONCEPTO DE SISTEMA OPERATIVO

### 3.1 Definición
Un **sistema operativo (SO)** es un conjunto de programas que actúa como intermediario entre el usuario y el hardware del ordenador. Su función principal es gestionar de manera eficiente los recursos hardware y proporcionar una interfaz cómoda para el usuario.

### 3.2 Objetivos del Sistema Operativo
- **Comodidad**: Hacer más fácil el uso del ordenador
- **Eficiencia**: Permitir el uso eficiente de los recursos del sistema
- **Capacidad de evolución**: Permitir el desarrollo, prueba e introducción efectiva de nuevas funciones

### 3.3 Elementos de un Sistema Operativo

#### Núcleo o Kernel
Es el componente central del sistema operativo que:
- Gestiona la memoria
- Administra los procesos
- Controla los dispositivos de E/S
- Gestiona el sistema de archivos

#### Intérprete de Comandos (Shell)
Interfaz que permite al usuario comunicarse con el sistema operativo mediante:
- **Interfaz de línea de comandos (CLI)**: Comandos de texto
- **Interfaz gráfica de usuario (GUI)**: Elementos visuales (ventanas, iconos, menús)

#### Programas del Sistema
Utilidades que realizan funciones comunes de gestión como formatear discos, copiar archivos, etc.

### 3.4 Estructura del Sistema Operativo
Los sistemas operativos pueden organizarse según diferentes estructuras:

#### Estructura Monolítica
- Todo el código del SO ejecuta en modo privilegiado
- Rápida comunicación entre componentes
- Difícil mantenimiento y depuración

#### Estructura por Capas
- Organización jerárquica en niveles
- Cada capa utiliza servicios de la capa inferior
- Mayor modularidad pero menor eficiencia

#### Estructura de Microkernel
- Kernel mínimo que proporciona servicios básicos
- Servicios adicionales en espacio de usuario
- Mayor estabilidad y seguridad

---

## 4. CLASIFICACIÓN DE LOS SISTEMAS OPERATIVOS

### 4.1 Por el Número de Usuarios
- **Monousuario**: Un solo usuario puede usar el sistema (MS-DOS, primeras versiones de Windows)
- **Multiusuario**: Varios usuarios pueden usar el sistema simultáneamente (Linux, UNIX, Windows Server)

### 4.2 Por el Número de Procesos
- **Monotarea**: Un solo programa en ejecución (MS-DOS)
- **Multitarea**: Varios programas ejecutándose aparentemente al mismo tiempo

### 4.3 Por el Número de Procesadores
- **Monoprocesador**: Un solo procesador
- **Multiprocesador**: Varios procesadores trabajando coordinadamente

### 4.4 Por el Tipo de Interfaz
- **Línea de comandos**: Interacción mediante texto (Linux terminal, MS-DOS)
- **Interfaz gráfica**: Interacción mediante elementos visuales (Windows, macOS, Linux con entorno gráfico)

### 4.5 Por el Propósito
- **Sistemas de propósito general**: Para uso doméstico y empresarial
- **Sistemas especializados**: Para aplicaciones específicas (sistemas empotrados, tiempo real)

### 4.6 Por la Portabilidad
- **Propietarios**: Diseñados para hardware específico
- **Portables**: Pueden ejecutarse en diferentes tipos de hardware

---

## 5. FUNCIONES DEL SISTEMA OPERATIVO. RECURSOS

### 5.1 Gestión de Procesos
- **Creación y terminación** de procesos
- **Planificación** de la CPU
- **Sincronización** y comunicación entre procesos
- **Gestión de interbloqueos** (deadlocks)

### 5.2 Gestión de Memoria
- **Asignación y liberación** de memoria
- **Control de acceso** a las zonas de memoria
- **Memoria virtual**: Técnica que permite ejecutar programas más grandes que la memoria física disponible

### 5.3 Gestión del Sistema de Archivos
- **Creación y eliminación** de archivos y directorios
- **Control de acceso** a archivos
- **Organización** del almacenamiento en disco
- **Copias de seguridad** y recuperación

### 5.4 Gestión de Entrada/Salida
- **Control de dispositivos** periféricos
- **Gestión de interrupciones**
- **Buffering y caching** para optimizar las operaciones de E/S
- **Gestión de colas** de peticiones de E/S

### 5.5 Recursos del Sistema
Los recursos que gestiona el SO incluyen:
- **Recursos hardware**: CPU, memoria, dispositivos de E/S
- **Recursos software**: Archivos, programas, datos
- **Recursos de red**: Conexiones, ancho de banda

---

## 6. PROCESOS DEL SISTEMA OPERATIVO

### 6.1 Concepto de Proceso
Un **proceso** es un programa en ejecución. Incluye:
- El código del programa
- Los datos del programa
- El contador de programa (PC)
- Los registros del procesador
- La pila del proceso

### 6.2 Estados de los Procesos
Un proceso puede estar en diferentes estados durante su ciclo de vida:

#### Nuevo (New)
El proceso está siendo creado.

#### Preparado (Ready)
El proceso está esperando a ser asignado a un procesador.

#### En Ejecución/Activo (Running)
Las instrucciones del proceso están siendo ejecutadas.

#### En Espera/Bloqueado (Waiting/Blocked)
El proceso está esperando que ocurra algún evento (operación de E/S, señal).

#### Terminado (Terminated)
El proceso ha finalizado su ejecución.

### 6.3 Transiciones entre Estados
- **Nuevo → Preparado**: Admisión del proceso
- **Preparado → En Ejecución**: Planificación (dispatch)
- **En Ejecución → Preparado**: Interrupción (fin de quantum de tiempo)
- **En Ejecución → En Espera**: Solicitud de E/S u otro evento
- **En Espera → Preparado**: Finalización de E/S o evento esperado
- **En Ejecución → Terminado**: Finalización del proceso

![Estados de los procesos](/img/ud1_img2.webp "Estados de los procesos")

### 6.4 Prioridades
Los procesos pueden tener diferentes niveles de prioridad:

#### Tipos de Prioridad
- **Prioridad estática**: Asignada al crear el proceso y no cambia
- **Prioridad dinámica**: Puede cambiar durante la ejecución

#### Niveles de Prioridad (ejemplo típico)
- **Crítica**: Procesos del sistema
- **Alta**: Procesos interactivos
- **Normal**: Procesos de usuario estándar
- **Baja**: Procesos en segundo plano

#### Algoritmos de Planificación
- **FIFO (First In, First Out)**: Orden de llegada
- **SJF (Shortest Job First)**: Proceso más corto primero
- **Round Robin**: Asignación circular con quantum de tiempo
- **Por prioridades**: Los procesos con mayor prioridad se ejecutan primero

---

## 7. SISTEMAS DE ARCHIVOS: TIPOS Y CARACTERÍSTICAS

### 7.1 Concepto de Sistema de Archivos
Un **sistema de archivos** es la forma en que el sistema operativo organiza y gestiona los datos en los dispositivos de almacenamiento.

### 7.2 Funciones de los Sistemas de Archivos
- **Organización** de datos en archivos y directorios
- **Control de acceso** y permisos
- **Gestión del espacio** en disco
- **Integridad** y recuperación de datos
- **Rendimiento** y optimización de accesos

### 7.3 Principales Sistemas de Archivos

#### FAT32 (File Allocation Table 32)
- **Uso**: Dispositivos de almacenamiento extraíbles, compatibilidad
- **Características**: 
  - Tamaño máximo de archivo: 4 GB
  - Tamaño máximo de partición: 8 TB
  - Compatible con casi todos los SO
  - No tiene permisos de archivos

#### NTFS (New Technology File System)
- **Uso**: Windows moderno
- **Características**:
  - Soporte para archivos muy grandes
  - Sistema de permisos avanzado
  - Cifrado de archivos
  - Compresión
  - Recuperación de errores

#### ext4 (Extended File System 4)
- **Uso**: Linux
- **Características**:
  - Excelente rendimiento
  - Soporte para archivos muy grandes
  - Journaling para integridad
  - Permisos avanzados de archivos

#### APFS (Apple File System)
- **Uso**: macOS, iOS
- **Características**:
  - Optimizado para almacenamiento SSD
  - Cifrado nativo
  - Snapshots instantáneos
  - Clones de archivos eficientes

### 7.4 Características Importantes
- **Journaling**: Registro de cambios para recuperación
- **Permisos**: Control de acceso a archivos y carpetas
- **Fragmentación**: Grado de dispersión de archivos en disco
- **Compresión**: Reducción automática del tamaño de archivos
- **Cifrado**: Protección de datos mediante encriptación

---

## 8. TRANSACCIONES. SISTEMAS TRANSACCIONALES

### 8.1 Concepto de Transacción
Una **transacción** es una secuencia de operaciones que se ejecutan como una unidad indivisible. Todas las operaciones de la transacción deben completarse exitosamente o ninguna debe tener efecto.

### 8.2 Propiedades ACID
Las transacciones deben cumplir las propiedades ACID:

#### Atomicidad (Atomicity)
- Una transacción es indivisible
- O se ejecutan todas las operaciones o ninguna

#### Consistencia (Consistency)
- La transacción debe llevar el sistema de un estado válido a otro estado válido

#### Aislamiento (Isolation)
- Las transacciones concurrentes no deben interferir entre sí

#### Durabilidad (Durability)
- Una vez confirmada, la transacción debe persistir ante fallos del sistema

### 8.3 Sistemas Transaccionales
Son sistemas diseñados para gestionar transacciones de manera eficiente y segura:

#### Características
- **Control de concurrencia**: Gestión de múltiples transacciones simultáneas
- **Recuperación ante fallos**: Capacidad de restaurar el sistema tras errores
- **Logging**: Registro de todas las operaciones para recuperación
- **Bloqueos**: Mecanismos para evitar conflictos entre transacciones

#### Ejemplos de Uso
- **Bases de datos**: Sistemas de gestión de bases de datos (SGBD)
- **Sistemas bancarios**: Transferencias de dinero
- **Comercio electrónico**: Procesamiento de pedidos
- **Sistemas de reservas**: Hoteles, vuelos, entradas

---

## 9. EVOLUCIÓN DE LOS SISTEMAS OPERATIVOS

### 9.1 Primera Generación (1940-1955)
- **Características**: Sin sistema operativo
- **Programación**: Directa en lenguaje máquina
- **Procesamiento**: Un programa a la vez
- **Ejemplo**: ENIAC, máquinas de válvulas

### 9.2 Segunda Generación (1955-1965)
- **Características**: Sistemas por lotes (batch)
- **Procesamiento**: Grupos de trabajos similares
- **Avances**: Primeros lenguajes de programación
- **Limitaciones**: No interacción directa con el usuario

### 9.3 Tercera Generación (1965-1980)
- **Características**: Multiprogramación y tiempo compartido
- **Avances**: 
  - Varios programas en memoria simultáneamente
  - Interacción directa usuario-computadora
  - Desarrollo de UNIX
- **Ejemplos**: IBM System/360, UNIX

### 9.4 Cuarta Generación (1980-presente)
- **Características**: Computadoras personales e interfaces gráficas
- **Avances**:
  - Interfaces gráficas de usuario (GUI)
  - Redes de computadoras
  - Internet
- **Ejemplos**: MS-DOS, Windows, macOS, Linux

### 9.5 Tendencias Actuales
- **Sistemas móviles**: Android, iOS
- **Computación en la nube**: Virtualización, contenedores
- **Internet de las cosas (IoT)**: Sistemas embebidos
- **Inteligencia artificial**: Optimización automática

---

## 10. SISTEMAS OPERATIVOS ACTUALES

### 10.1 Sistemas Operativos de Escritorio

#### Microsoft Windows
- **Versiones actuales**: Windows 10, Windows 11
- **Características**:
  - Interfaz gráfica intuitiva
  - Gran compatibilidad de software
  - Amplio soporte de hardware
  - Integración con servicios en la nube

#### macOS
- **Desarrollador**: Apple Inc.
- **Características**:
  - Diseño elegante y consistente
  - Integración con ecosistema Apple
  - Excelente para multimedia y diseño
  - Basado en UNIX

#### Linux
- **Distribuciones populares**: Ubuntu, Debian, Fedora, openSUSE
- **Características**:
  - Código abierto y gratuito
  - Alta personalización
  - Excelente seguridad
  - Múltiples entornos gráficos

### 10.2 Sistemas Operativos Móviles

#### Android
- **Desarrollador**: Google
- **Características**:
  - Basado en Linux
  - Mayor cuota de mercado mundial
  - Gran variedad de dispositivos
  - Tienda Google Play

#### iOS
- **Desarrollador**: Apple
- **Características**:
  - Exclusivo para dispositivos Apple
  - Excelente rendimiento y seguridad
  - Ecosistema cerrado pero integrado
  - App Store

### 10.3 Sistemas Operativos de Servidor

#### Windows Server
- **Características**:
  - Integración con entorno Windows
  - Active Directory
  - Herramientas de administración gráficas

#### Linux (distribuciones servidor)
- **Ejemplos**: Ubuntu Server, Red Hat Enterprise Linux, CentOS
- **Características**:
  - Estabilidad y rendimiento
  - Menor consumo de recursos
  - Administración principalmente por línea de comandos

#### UNIX
- **Variantes**: AIX, Solaris, HP-UX
- **Características**:
  - Sistemas empresariales de alta gama
  - Excelente estabilidad
  - Soporte para hardware específico

### 10.4 Tendencias y Tecnologías Emergentes

#### Virtualización
- **VMware**, **Hyper-V**, **VirtualBox**
- Permite ejecutar múltiples SO en un mismo hardware

#### Contenedores
- **Docker**, **Kubernetes**
- Virtualización a nivel de aplicación

#### Computación en la Nube
- **Amazon AWS**, **Microsoft Azure**, **Google Cloud**
- Sistemas operativos optimizados para servicios en la nube

#### Internet de las Cosas (IoT)
- **Sistemas embebidos** con SO específicos
- **Tiempo real** y bajo consumo energético

---

## RESUMEN DE CONCEPTOS CLAVE

- **Sistema informático**: Hardware + Software
- **Sistema operativo**: Interfaz entre usuario y hardware
- **Funciones principales**: Gestión de procesos, memoria, archivos y E/S
- **Estados de proceso**: Nuevo, Preparado, Ejecución, Espera, Terminado
- **Sistemas de archivos**: Formas de organizar datos (FAT32, NTFS, ext4, APFS)
- **Transacciones**: Operaciones que cumplen propiedades ACID
- **Evolución**: De sistemas por lotes a interfaces gráficas y móviles
- **SO actuales**: Windows, macOS, Linux (escritorio), Android, iOS (móvil)

---

## ACTIVIDADES DE AUTOEVALUACIÓN

1. Explica las diferencias entre hardware y software en un sistema informático.

2. Define qué es un sistema operativo y menciona sus tres funciones principales.

3. Describe los cinco estados por los que puede pasar un proceso.

4. Compara las características de FAT32 y NTFS.

5. Explica las propiedades ACID de las transacciones.

6. Menciona tres sistemas operativos actuales para escritorio y sus principales características.

7. ¿Qué ventajas ofrece la multiprogramación frente a la monotarea?

8. Describe la diferencia entre prioridad estática y dinámica en procesos.
