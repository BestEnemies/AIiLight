![AiLight](images/ailight_logo.png)

The **AiLight** firmware has a feature that allows you to flash the light (i.e switch it on and off at a particular interval). It can only be used by either sending a specific instruction to the MQTT command topic or using the Home Assistant automation component.

## How to use

### 1. Home Assistant
Using Home Assistant's Automation component, you can have your Ai-Thinker LED RGBW light flash by a specified trigger and certain conditions. For example, why not let your Ai-Thinker LED RGBW light flash if somebody presses the button of your Smart Doorbell:

``` YAML
automation:
  - alias: 'Flash the light when front doorbell pressed'
    initial_state: 'on'
    trigger:
      - platform: state
        entity_id: binary_sensor.doorbell
        from: 'off'
        to: 'on'
    action:
      - service: light.toggle
        data:
          entity_id: light.ailight_office
          flash: long
          color: [255, 0, 0]
```
This will make your Ai-Thinker LED RGBW light flash the colour red for 10 seconds. The 'long' value is a standard Home Assistant value defaults to 10 seconds. There is also a 'short' value which defaults to 5 seconds.

Please check the Home Assistant [Automation](https://home-assistant.io/getting-started/automation/) and [Actions](https://home-assistant.io/docs/automation/action/) documentation pages for more information on how to configure Home Assistant.

### 2. Using MQTT
You can alternatively flash your Ai-Thinker LED RGBW light by publishing an MQTT message to your MQTT broker. To do that, simply send a JSON message to the MQTT Command Topic set for your Ai-Thinker LED RGBW light.

Example:
``` JSON
{"flash":"5", "color": {"r": 255, "g": 0, "b": 0}}
```

`mosquitto_pub -h <your_mqtt_broker> -t <your_ailight_command_topic> -m '{"flash":"5", "color": {"r": 255, "g": 0, "b": 0}}'`

This will make your Ai-Thinker LED RGBW light flash the colour red for 5 seconds.

**Note**: at the moment the light alternates between the specified colour and 'off' with an interval of 500ms. These can only be changed by modifying the source code.
