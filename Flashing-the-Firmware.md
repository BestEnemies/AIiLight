Having your Ai-Thinker RGBW Light run using the **AiLight** firmware is quite simple and consists only of two parts:
1. Compiling the firmware
2. Flashing (i.e uploading) the firmware.

## Compiling the firmware

1. Clone this **AiLight** repository and change your current directory to where **AiLight** is cloned.
2. Make a copy of the `config.example.h` file in the 'src' folder named `config.h`
3. Depending on your environment, set at least the following values in the `config.h` file:

  - WIFI_SSID `// Your WiFi SSID`
  - WIFI_PSK `// Your WiFi PSK/Password`
  - MQTT_SERVER `// The hostname/IP address of your MQTT broker`
  - MQTT_USER `// The username to connect to your MQTT broker`
  - MQTT_PASSWORD `// The password to connect to your MQTT broker`

  Leaving the WiFi settings blank, will make the **AiLight** start in AP mode (Access Point). From there you can access the   settings screen and enter your WiFi settings.

  Other configuration variables can be left as is, however feel free to adjust as you see fit.

4. Make a copy of the `platformio.example.ini` file name `platformio.ini`. This PlatformIO configuration doesn't require any changes, however it is recommended to change the OTA port number and OTA password when using your Ai-Thinker RGBW Light in production. (In that case don't forget to update the respective variables in your `config.h` file too).

5. In a terminal session (or in PlatformIO), run the command `npm install` (or `yarn install`). This is a required step that will install necessary NodeJS packages for building the UI interface. Make sure you do this in the directory where you cloned **AiLight** (e.g 'AiLight'), otherwise the NodeJS packages will not get installed.

6. Click on the "PlatformIO: Build" icon (or issue a "platformio run" command from the PlatformIO terminal).

That's all it takes, you're ready to go!

## Flashing (i.e uploading) the firmware

If no compilation errors popped up, you can start flashing the firmware to your Ai-Thinker RGBW Light using an FTDI (or alike) programmer. This is a required step of course, since your Ai-Thinker RGBW Light still has the factory firmware.

If the upload of the **AiLight** firmware was successful, it is recommended to restart your Ai-Thinker RGBW Light. This can be done by reconnecting the power of your FTDI programmer.

While connected to your FTDI programmer, check the output on your Serial Monitor. You should see some messages appear that will tell you details of the firmware, the device, hostname and the assigned IP address.

![AiLight](https://www.sachatelgenhof.nl/user/pages/02.blog/ailight/terminal_030.png)

The same information can be seen in the HTML UI (About screen). By default, the Web interface can be accessed via 'http://AiLight-######.local' where '#####' is the unique ID of your Ai-Thinker RGBW Light. If you have changed your hostname, then, of course, the URL is different also.

From this point, you can upload newer versions of the firmware via OTA. Update the `upload_port` variable in your platformio.ini file with the 'hostname' value from the Serial Monitor / HTML UI. Now you can start using OTA to upload any updates of the firmware over the air.