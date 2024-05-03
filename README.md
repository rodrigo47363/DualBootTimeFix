# DualBootTimeFix
# Corregir la hora en un sistema con arranque dual (Windows y Linux)

Este documento proporciona instrucciones paso a paso para corregir la hora en un sistema con arranque dual (Windows y Linux).

## Modificar el registro de Windows

1. Ejecutar `regedit`.
2. Navegar a la siguiente ruta: `Equipo\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`.
3. Crear un nuevo valor dword 32 bits con el nombre `RealTimeIsUniversal` y asigna el valor `1`.

## Ajustar la hora local en Linux

1. Abrir la terminal.
2. Ejecutar el siguiente comando: `timedatectl set-local-rtc 1`.

## Advertencia

Por favor, asegúrate de entender completamente lo que estos comandos hacen antes de ejecutarlos. Modificar el registro de Windows y los servicios puede tener efectos significativos en tu sistema. Si tienes alguna duda, te recomiendo que consultes con un experto en sistemas operativos.

