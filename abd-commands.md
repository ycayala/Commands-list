Ir al contenido
Hackpuntes
Menú principal
Listado de comandos ADB más utilizados
19 comentarios / ADB, Android, Herramientas, Sistemas Operativos / Por Javier Olmedo / lunes, 6 mayo, 2019
Android Debug Bridge (ADB) es una herramienta de línea de comandos que viene incluida con el SDK de Android, permite a los desarrolladores comunicarse con un emulador o un dispositivo Android conectado directamente desde la línea de comandos. Esta herramienta podemos encontrarla en el directorio [SDK-PATH]/platform-tools, en Windows por defecto será en C:\Users\[USUARIO]\AppData\Local\Android\Sdk\platform-tools

En esta entrada, vamos a repasar los comandos más utilizados de ADB

Listado de dispositivos
Lo primero que debemos hacer, enumerar los dispositivos conectados.

adb devices
C:\Sdk\platform-tools>adb devices
List of devices attached
192.168.252.102:5555    device
emulator-5554   device
Conectar con dispositivo
adb connect [IP]:[PUERTO] (por defecto el 5555)
C:\Sdk\platform-tools>adb connect 192.168.252.102:5555
already connected to 192.168.252.102:5555
Desconectar el dispositivo
adb disconnect [IP]:[PUERTO]
C:\Sdk\platform-tools>adb disconnect 192.168.252.102:5555
disconnected 192.168.252.102:5555
Copiar un archivo al dispositivo
adb push [RUTA-LOCAL] [RUTA-DISPOSITIVO]
C:\Sdk\platform-tools>adb push miarchivo.txt /sdcard/misarchivos
miarchivo.txt: 1 file pushed.
Descargar un archivo desde el dispositivo
adb pull [RUTA-DISPOSITIVO] [RUTA-LOCAL]
C:\Sdk\platform-tools>adb pull /sdcard/misarchivos/miarchivo.txt
/sdcard/misarchivos/miarchivo.txt: 1 file pulled.
Reiniciar dispositivo
adb reboot
Reiniciar dispositivo (arranque)
adb reboot-bootloader
Instalar APK
adb install [APK]
Reinstalar APK
adb -r install [APK]
Desinstalar APK
adb uninstall [NOMBRE-PAQUETE-APLICACION]
Obtener shell del dispositivo
adb shell
Iniciar una Activity
adb shell am start -n [PAQUETE-APLICACION]/.[ACTIVITY]
C:\Sdk\platform-tools>adb shell am start -n com.hackpuntes.myapplication/.MainActivity
adb shell am start -n [PAQUETE-APLICACION]/[ACTIVITY]
C:\Sdk\platform-tools>adb shell am start -n com.hackpuntes.myapplication / com.hackpuntes.myapplication.MainActivity
Tomar captura de pantalla
adb shell screencap [RUTA-DISPOSITIVO]
C:\Sdk\platform-tools>adb shell screencap /sdcard/micaptura.png
Grabar pantalla del dispositivo
adb shell screenrecord -time-limit [SEGUNDOS] [RUTA-DISPOSITIVO]
C:\Sdk\platform-tools>adb shell screenrecord --time-limit 20 /sdcard/mivideo.mp4
Emular botón encendido
adb shell input keyevent 26
Emular pantalla de desbloqueo
adb shell input keyevent 82
Ver más eventos

Listar paquetes instalados
adb shell pm list packages
C:\Sdk\platform-tools>adb shell pm list packages
package:com.example.android.livecubes
package:com.android.providers.telephony
package:com.android.providers.calendar
package:com.android.providers.media
package:com.google.android.onetimeinitializer
package:com.android.wallpapercropper
Logcat
adb logcat
Filtrar por nivel de prioridad
adb logcat "*:W"
Filtrar por TAG y prioridad
adb logcat -s Mi_TAG:W
Buscar contenido en el buffer
adb logcat -b ejemplo
Borrar el buffer
adb logcat -c
Filtrar con grep
adb logcat | grep "com.hackpuntes"
Volcar datos del sistema en la pantalla
adb shell dumpsys
Volcar datos del sistema a un archivo
adb shell dumpstate -o /sdcard/dump.txt
Volcar datos de un servicio específico
adb shell dumpsys battery
Mostrar información sobre CPU
adb shell cat/proc/cpuinfo
Extraer APK
adb shell pm path [NOMBRE-PAQUETE]
adb pull /data/app/[NOMBRE-PAQUETE]/base.apk
adb shell pm path com.hackpuntes.miaplicacion
adb pull /data/app/com.hackpuntes.miaplicacion/base.apk
Habilitar datos móviles
adb shell svc data enable
Deshabilitar datos móviles
adb shell svc data disable
