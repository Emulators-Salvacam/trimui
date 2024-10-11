
# Trimui Smart PRO
Trimui Smart Pro

## Emulador WOLF3D
Es necesario modificar el core ecwolf, con el core de la tarjeta no he conseguido reproducir el juego Wolfenstein 3d.

No he compilado este core lo he descargado del siguiente repositorio https://github.com/christianhaitian/retroarch-cores


	Pendiente de subir el emulador completo

## Emulador CHIP-8

	Pendiente de subir el emulador completo
	
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
