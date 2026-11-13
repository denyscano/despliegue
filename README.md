# Despliegue de Ubuntu en VirtualBox

## Objetivo

Instalar Ubuntu en una máquina virtual, integrar el sistema invitado con el equipo anfitrión y practicar la ampliación y gestión de almacenamiento. Esta memoria resume el proceso y sus evidencias.

## 1. Despliegue y configuración

### Creación y recursos

Se creó una máquina virtual para Ubuntu 25.04 de 64 bits desde una ISO. Se asignaron **6033 MB de RAM**, **3 CPU** y un disco virtual de **101,91 GB**. La interfaz muestra como referencia 16 384 MB de RAM y 12 CPU disponibles; la asignación utiliza aproximadamente el 37 % de la memoria y una cuarta parte de las CPU, dejando recursos para el equipo anfitrión y cubriendo los requisitos minimos de 6 GB mínimo y 25 GB de almacenamiento.

![Selección de Ubuntu y su ISO](<Captura de pantalla 2026-11-06 132408.png>)

![Asignación de RAM, CPU y disco](<Captura de pantalla 2026-11-06 133335.png>)

### Arranque e instalación

La ISO se conectó a la unidad óptica y se colocó primero en el orden de arranque, seguida por el disco duro. Durante la instalación se seleccionaron el idioma español y la distribución de teclado española. La pantalla de instalación desatendida muestra los campos de usuario y contraseña; la contraseña no aparece en la captura.

![Orden de arranque](<Captura de pantalla 2026-11-06 135105.png>)

![ISO conectada](<Captura de pantalla 2026-11-06 135200.png>)

![Idioma español](<Captura de pantalla 2026-11-06 135927.png>)

![Teclado español](<Captura de pantalla 2026-11-06 140107.png>)

![Opciones de instalación desatendida](<Captura de pantalla 2026-11-06 132819.png>)

### Integración con VirtualBox

Se inició la instalación de Guest Additions desde la imagen de CD de VirtualBox. La terminal muestra la compilación de módulos del kernel y la actualización de initramfs, aunque la captura no recoge el resultado final. En los menús de VirtualBox se ve la opción de redimensionado de pantalla y el portapapeles bidireccional seleccionado.

![Inserción de Guest Additions](<Captura de pantalla 2026-11-09 140938.png>)

![Proceso de instalación de Guest Additions](<Captura de pantalla 2026-11-09 142902.png>)

![Opción de redimensionado de pantalla](<Captura de pantalla 2026-11-09 140725.png>)

![Portapapeles bidireccional](<Captura de pantalla 2026-11-09 140816.png>)

### Carpeta compartida

Se configuró una carpeta llamada `hola`, con punto de montaje `/home/vboxuser/Escritorio/hola`. Las opciones de automontaje y configuración permanente aparecen activadas.

![Configuración de carpeta compartida](<Captura de pantalla 2026-11-09 143454.png>)

## 2. Almacenamiento y mantenimiento

### Segundo disco y particiones

Se creó un segundo disco virtual de **14 GB**. En GParted se observa como `/dev/sdb`. La captura final muestra una partición **ext4 de 7,16 GiB** y otra **FAT32 de 5,86 GiB**, con aproximadamente **1000 MiB sin asignar**. Una captura previa muestra operaciones pendientes. Las imágenes no permiten confirmar que se aplicaran los cambios ni que el disco use una tabla GPT.

![Creación del segundo disco de 14 GB](<Captura de pantalla 2026-11-13 120030.png>)

![Disco principal del sistema en GParted](<Captura de pantalla 2026-11-13 120659.png>)

![Particiones preparadas con operaciones pendientes](<Captura de pantalla 2026-11-13 121021.png>)

![Particiones ext4 y FAT32 en GParted](<Captura de pantalla 2026-11-13 121409.png>)

**Ventaja de ext4:** su journaling registra cambios del sistema de archivos antes de aplicarlos. Esto ayuda a recuperar la consistencia tras un apagado inesperado. FAT32 no ofrece ese mecanismo.

### Actualizaciones

Se ejecutó `sudo apt update`. La salida informa de **41 paquetes actualizables**; la captura demuestra la comprobación de los repositorios, pero no que se instalaran las actualizaciones.

![Comprobación de actualizaciones](<Captura de pantalla 2026-11-13 121857.png>)

**Pendiente de documentar:** indicar si se aplicaron las actualizaciones y añadir el resultado del comando correspondiente.

## 3. Registro de incidencias


1. **Problema:** Creamos una partición sin nombre.  
   **Solución:** Eliminamos la participación y la volvimos a crear

2. **Problema:** Se eliminó la carpeta compartida en el ordenador host.  
   **Solución:** Al encender la maquina virtual nos nos mostró un mensaje de error, solucionamos el problema creando de vuelta la carpeta.

## Conclusión

Las capturas documentan la creación y configuración inicial de Ubuntu, opciones de integración con VirtualBox, la preparación de un segundo disco y la comprobación de actualizaciones. 
