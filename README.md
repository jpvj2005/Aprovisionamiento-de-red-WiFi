# Aprovisionamiento-de-red-WiFi


DESCRIPCION: Solución IoT basada en ESP32 que permite la configuración dinámica de la red WiFi sin necesidad de reprogramar el dispositivo. Incluye un portal cautivo/interfaz web para que el usuario final configure SSID y contraseña de manera sencilla. Desarrollado en Arduino, siguiendo buenas prácticas de ingeniería y validado mediante prototipado.


REQUISITOS DEL SISTEMA


Hardware

- ESP32

- Cable USB para cargar el código y alimentación

Software

- Arduino IDE (versión recomendada 1.8.x o 2.x)

- Plataforma ESP32 instalada en Arduino IDE

  - URL del gestor de tarjetas: https://dl.espressif.com/dl/package_esp32_index.json

- Librerías necesarias (se instalan desde el Gestor de Librerías en Arduino IDE):

    - WiFi.h

    - WebServer.h


3. Instalación y uso

- Clonar este repositorio o descargar el código fuente.

- Abrir el proyecto en Arduino IDE y seleccionar la placa:

  - Herramientas → Placa → ESP32 Dev Module

  - Puerto: seleccionar el correspondiente a tu ESP32

- Cargar el código al ESP32 mediante el cable USB.

- Primer inicio (sin credenciales guardadas):

  - El ESP32 inicia en modo Access Point (AP) y crea una red WiFi (ejemplo: ESP32_Config).

  - Conéctate desde tu celular o PC a esa red.

  - Al abrir el navegador se mostrará el portal cautivo para ingresar SSID y contraseña.

- Conexión automática:

  - Una vez guardadas las credenciales, el ESP32 se reinicia y se conecta automáticamente a la red configurada.

  - En futuros reinicios se conectará directo, sin necesidad de reconfigurar.

- Reconfiguración:

  - Si deseas borrar credenciales y configurar otra red, presiona el botón físico de reset (si está implementado en el código) o accede al endpoint /reset.

4. Funcionamiento técnico

- El ESP32 verifica al inicio si existen credenciales WiFi guardadas en memoria no volátil (Preferences o SPIFFS).

- Si no encuentra credenciales, inicia en modo AP y levanta un portal cautivo con servidor web y DNS local.

- El usuario ingresa el SSID y la contraseña en la interfaz web.

- Los datos se guardan en memoria no volátil y el ESP32 se reinicia automáticamente.

- Al reiniciar, intenta conectarse a la red configurada.

- Si la conexión falla (ejemplo: SSID inexistente o contraseña incorrecta), vuelve al modo AP para reconfiguración.

- Se incluye un mecanismo de reseteo para borrar credenciales y permitir configurar una nueva red WiFi.
