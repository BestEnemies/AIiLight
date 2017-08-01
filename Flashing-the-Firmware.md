![AiLight](images/ailight_logo.png)

Having your Ai-Thinker LED RGBW light run using the **AiLight** firmware is quite simple and consists only of two parts:
1. Compiling the firmware
2. Flashing (i.e uploading) the firmware.

_Before starting, please make sure you have all that is [[needed|Requirements]]._

## Compiling the firmware

1. Clone this **AiLight** repository (or download a Zip file) and change your current directory to where **AiLight** is cloned (or where you unpacked the Zip file).
2. Make a copy of the `config.example.h` file in the 'src' folder named `config.h`
   Depending on your environment, set at least the following values in the `config.h` file:

  - WIFI_SSID `// Your WiFi SSID`
  - WIFI_PSK `// Your WiFi PSK/Password`
  - MQTT_SERVER `// The hostname/IP address of your MQTT broker`
  - MQTT_USER `// The username to connect to your MQTT broker`
  - MQTT_PASSWORD `// The password to connect to your MQTT broker`

  Leaving the WiFi values blank, will make the **AiLight** start in AP mode (Access Point). From there you can access the settings screen and enter your WiFi settings. (TBD)

  Other configuration variables can be left as is, however, feel free to adjust as you see fit.

3. Make a copy of the `platformio.example.ini` file name `platformio.ini`. This PlatformIO configuration doesn't require any changes, however, it is recommended to change the OTA port number and OTA password when using your Ai-Thinker RGBW Light in production. (In that case, don't forget to update the respective variables in your `config.h` file too).

4. Click on the "PlatformIO: Build" icon or issue a `platformio run` command from the PlatformIO terminal.


## Flashing the firmware for the first time

If no compilation errors popped up, you can start uploading (i.e 'flashing') the firmware to your Ai-Thinker LED RGBW light using an USB/UART (or equivalent) adapter. This is, of course, a required step since your Ai-Thinker LED RGBW light still has the original factory firmware.

1. Connect your USB/UART (or equivalent) adapter or AiLight Jig to your PC using a Micro USB to USB cable.
2. Click on the "PlatformIO: Upload icon" (Arrow pointing to the right) or issue a `platform run --target upload` command from the PlatformIO terminal. Uploading should start automatically as PlatformIO will detect the connected Serial Port itself. Alternatively, you can manually specify in the `platformio.ini` or at the command line which serial port you want use.

_**Note**: If you have trouble making a connection, check if PlatformIO can detect your adapter by clicking "List Serial Ports" in the "PlatformIO" menu. If not, this usually means your cable is not connected or your driver is not properly installed. (You can also see this information from the command terminal by issuing this command: `pio list devices`)_

If the upload of the **AiLight** firmware was successful, it is recommended restarting your Ai-Thinker LED RGBW light. This can be done by reconnecting the power of your USB/UART (or equivalent) adapter.

While connected to your USB/UART (or equivalent) adapter, check the output on your Serial Monitor. You should see some messages appear that will tell you details of the **AiLight** firmware, the device, hostname and the assigned IP address.

![AiLight](https://www.sachatelgenhof.nl/user/pages/02.blog/ailight/terminal_030.png)

Similar information can be seen in the Web UI (About page). By default, the Web UI can be accessed via 'http://AiLight-######.local' where '#####' is the unique identifier of your Ai-Thinker LED RGBW light. If you have changed your hostname, then, of course, the URL is different also.

Your Ai-Thinker LED RGBW light is now ready and runs the **AiLight** firmware! Please go ahead and disconnect the USB/UART (or equivalent) adapter or AiLight Jig and put your Ai-Thinker LED RGBW light in your kitchen light, ceiling light, etc.
