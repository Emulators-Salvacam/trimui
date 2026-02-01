
# Trimui Smart PRO
Trimui Smart Pro

## Emulador WOLF3D

Emulador completo en release, es necesario añadir el juego en la carpeta Roms/WOLF3D

### Modiciar core Ecwolf
Fue necesario modificar el core ecwolf, con el core de la tarjeta no he conseguido reproducir el juego Wolfenstein 3d.

No he compilado este core lo he descargado del siguiente repositorio https://github.com/christianhaitian/retroarch-cores


## Emulador CHIP-8

Emulador completo en release, con juegos distribuidos libremente

### Compilar core Jaxe para Trimui Smart PRO

Descargar el sdk desde https://github.com/knulli-cfw/toolchains y descomprimir en /opt/toolchain

añadir en el archivo Makefile.libretro
```
	# TRIMUI SMART PRO
else ifeq ($(platform), trimui)
	TARGET := $(TARGET_NAME)_libretro.so
	fpic := -fPIC
	SHARED := -shared -Wl,-version-script=link.T
	CC = /opt/toolchain/bin/aarch64-buildroot-linux-gnu-gcc
	CFLAGS += -fomit-frame-pointer -ffast-math -march=armv8.1-a -mtune=cortex-a35
```
y compilar con la orden
```
	make -f Makefile.libretro platform=trimui
```
si es necesario recompilar antes limpiar añadiendo la opción clean
 ```
make -f Makefile.libretro platform=trimui clean
```

### R36S
La propia compilación para Trimui vale para la R36S
solo hay que añadir el archivo [jaxe_libreto.so](https://github.com/Emulators-Salvacam/trimui/blob/main/jaxe_libretro.so) a la carpeta root/home/ark/.config/retroarch/config
y añadir el sistema al archivo root/etc/emulationstation/es_systems.cfg
```
	<system>
		<name>chip8</name>
		<fullname>CHIP-8</fullname>
		<path>/roms/chip8/</path>
		<extension>.ch8 .zip .ZIP</extension>
		<command>sudo perfmax %GOVERNOR% %ROM%; nice -n -19 /usr/local/bin/retroarch -L /home/ark/.config/retroarch/cores/jaxe_libretro.so %ROM%; sudo perfnorm</command>
		<platform>chip8</platform>
		<theme>chip8</theme>
		<manufacturer>Joseph Weisbecker</manufacturer>
		<release>1977</release>
		<hardware>computer</hardware>
	</system>
```
Crear la carpeta chip8 en EASYROMS

Según el tema que se este usando es posible que haya que modificar el tema, más info aquí
https://github.com/dov/r36s-programming?tab=readme-ov-file#installing-into-emulationstation

Para el tema nes-box solo he tenido que duplicar la carpeta de un sistema ya existente, y modificar el nombre de la carpeta creada por chip8, y luego modificar las imagenes del interior. Para el tema art-book-3-2 no he tenido que hacer nada.
