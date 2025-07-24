# Módulo LSPosed para Tidal (Simulador de Pantalla)

Este módulo LSPosed está diseñado para permitir que la aplicación Tidal funcione en dispositivos Android que no tienen una pantalla física, como los teléfonos controlados por Laixi. Tidal, al parecer, realiza comprobaciones de la presencia de una pantalla, lo que impide su funcionamiento en entornos "headless". Este módulo intercepta las llamadas a las APIs de detección de pantalla de Android y simula la existencia de una pantalla.

## Cómo funciona

El módulo hookea (intercepta) varios métodos de las clases `android.view.Display` y `android.hardware.display.DisplayManager`. Cuando Tidal intenta consultar el estado o las propiedades de la pantalla, el módulo devuelve valores que indican la presencia de una pantalla activa con una resolución y métricas estándar (por ejemplo, 1920x1080 píxeles, densidad de 320 dpi).

Las APIs hookeadas incluyen:
- `DisplayManager.getDisplays()`: Para asegurar que siempre se reporte al menos una pantalla.
- `Display.getState()`: Para simular que la pantalla está encendida (`Display.STATE_ON`).
- `Display.getSize()` y `Display.getRealSize()`: Para proporcionar una resolución de pantalla simulada.
- `Display.getMetrics()` y `Display.getRealMetrics()`: Para proporcionar métricas de pantalla simuladas.

## Requisitos

- Un dispositivo Android rooteado.
- LSPosed Framework instalado y funcionando en el dispositivo.
- La aplicación Tidal instalada.

## Instalación

1.  **Compilar el módulo:**
    Para compilar el módulo, necesitarás Android Studio y el SDK de Android. Clona este repositorio y abre el proyecto en Android Studio. Luego, construye el proyecto para generar el archivo APK del módulo.
    ```bash
    # En tu máquina de desarrollo (no en el sandbox)
    git clone [URL_DEL_REPOSITORIO] lsposed_tidal_screen_module
    cd lsposed_tidal_screen_module
    ./gradlew assembleRelease
    ```
    El archivo APK compilado se encontrará en `app/build/outputs/apk/release/app-release.apk` (o similar, dependiendo de la configuración de Gradle).

2.  **Instalar el APK en tu dispositivo:**
    Transfiere el archivo APK compilado a tu dispositivo Android e instálalo como una aplicación normal.

3.  **Activar el módulo en LSPosed:**
    - Abre la aplicación LSPosed en tu dispositivo.
    - Ve a la sección "Módulos" (Modules).
    - Busca "Tidal Screen Simulator" en la lista y actívalo.
    - Reinicia tu dispositivo para que los cambios surtan efecto.

## Uso

Una vez que el módulo esté activado y el dispositivo reiniciado, la aplicación Tidal debería detectar una pantalla física y funcionar correctamente. No se requiere ninguna configuración adicional.

## Solución de problemas

- **Tidal sigue sin funcionar:**
    - Asegúrate de que el módulo esté activado en LSPosed y de que hayas reiniciado el dispositivo.
    - Verifica los logs de Xposed (usando una aplicación como CatLog o a través de `adb logcat`) para ver si hay errores relacionados con el módulo o con Tidal.
    - Asegúrate de que la versión de Tidal que estás usando no tenga mecanismos de detección de pantalla inusuales o más avanzados que los que este módulo aborda.
- **Problemas de compilación:**
    - Asegúrate de tener el SDK de Android configurado correctamente en tu entorno de desarrollo.
    - Verifica las dependencias en `build.gradle`.

## Contribuciones

Las contribuciones son bienvenidas. Si encuentras un problema o tienes una mejora, por favor, abre un "issue" o envía un "pull request" en el repositorio de GitHub.

## Licencia

Este proyecto está bajo la licencia MIT. Consulta el archivo `LICENSE` para más detalles.

Test build

Trigger build
