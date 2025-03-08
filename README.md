# DualBootTimeFix

## Corregir la hora en un sistema con arranque dual (Windows y Linux)

Este documento proporciona instrucciones detalladas y fáciles de seguir para corregir la hora en un sistema con arranque dual (Windows y Linux).

### ¿Por qué es necesario esto?
Cuando tienes un sistema con arranque dual, Windows y Linux pueden tener configuraciones diferentes para manejar la hora del sistema, lo que puede causar que la hora se desajuste cada vez que cambias de un sistema operativo a otro. Estas instrucciones te ayudarán a sincronizar ambos sistemas correctamente.

## Modificar el registro de Windows

### Paso 1: Ejecutar el Editor del Registro

1. **Abrir el Editor del Registro:**
   - Presiona las teclas `Win + R` al mismo tiempo para abrir el cuadro de diálogo "Ejecutar".
   - Escribe `regedit` en el cuadro de texto y presiona `Enter`.
   - Si aparece una ventana de Control de Cuentas de Usuario (UAC), haz clic en "Sí" para permitir que la aplicación haga cambios en tu dispositivo.

### Paso 2: Navegar a la clave de registro

2. **Navegar a la siguiente ruta:**
   - En el Editor del Registro, utiliza el panel izquierdo para navegar a la siguiente ruta:
     ```
     HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation
     ```
   - Para hacerlo, haz clic en las flechas junto a cada carpeta hasta llegar a `TimeZoneInformation`.

### Paso 3: Crear un nuevo valor DWORD

3. **Crear un nuevo valor DWORD (32 bits):**
   - Haz clic derecho en un espacio vacío en el panel derecho.
   - Selecciona `Nuevo` -> `Valor DWORD (32 bits)`.
   - Nombra el nuevo valor como `RealTimeIsUniversal`.

### Paso 4: Asignar el valor

4. **Asignar el valor `1`:**
   - Haz doble clic en `RealTimeIsUniversal`.
   - En la ventana que aparece, establece el campo "Información del valor" en `1`.
   - Haz clic en `Aceptar`.

### Paso 5: Deshabilitar el servicio de tiempo de Windows

5. **Ejecutar el siguiente comando en la terminal (como administrador):**
   - Abre el "Símbolo del sistema" como administrador.
   - Escribe el siguiente comando:
     ```powershell
     sc config w32time start= disabled
     ```

### Alternativa usando la línea de comandos

Si prefieres, puedes hacer esto usando la línea de comandos:

1. **Abrir el Símbolo del sistema como administrador:**
   - Presiona las teclas `Win + X` y selecciona `Símbolo del sistema (Administrador)` o `Windows PowerShell (Administrador)`.

2. **Ejecutar el siguiente comando:**
   ```powershell
   reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
   ```

## Ajustar la hora local en Linux

### Paso 1: Abrir la terminal

1. **Abrir la terminal:**
   - Dependiendo de tu distribución de Linux, puedes abrir la terminal presionando `Ctrl + Alt + T` o buscándola en el menú de aplicaciones.

### Paso 2: Ejecutar el comando

2. **Ejecutar el siguiente comando:**
   ```bash
   timedatectl set-local-rtc 1
   ```
   - Este comando configura Linux para que use la hora local en lugar de la hora universal (UTC) en el reloj de hardware.

## Advertencia

Por favor, asegúrate de entender completamente lo que estos comandos hacen antes de ejecutarlos. Modificar el registro de Windows y los servicios de tiempo en Linux puede tener efectos significativos en tu sistema. Si no estás seguro de algún paso, consulta con un experto en sistemas operativos.

---

¡Gracias por usar DualBootTimeFix! Esperamos que estas instrucciones te sean de ayuda para mantener la hora correcta en tu sistema con arranque dual.

