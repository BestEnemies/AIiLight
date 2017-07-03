![](images/ailight_logo.png)

_Since release: **DEV**_

If you prefer to have [Home Assistant](https://home-assistant.io/) set up your Ai-Thinker LED RGBW Light automatically, then follow the steps below. **AiLight** supports Home Assistants' [MQTT Discovery](https://home-assistant.io/docs/mqtt/discovery/) functionality, which avoids any manual configuration in Home Assistant.

### Home Assistant
By default, the MQTT Discovery functionality in Home Assistant is disabled, so first thing to do is enable it. To do that, simply add `discovery: true` to your MQTT configuration. Additionally, you can set the discovery prefix used by Home Assistant. Your configuration should look something like this:

```YAML
mqtt:
  broker: <YOUR_MQTT_SERVER_ADDRESS>
  port: <YOUR_MQTT_PORT>
  client_id: home-assistant // Not required
  username: <YOUR_MQTT_USERNAME>
  password:  <YOUR_MQTT_PASSWORD>
  discovery: true
  discovery_prefix: homeassistant // 'homeassistant' is the default prefix, but can of course be changed
```
  
### AiLight
Next step is telling **AiLight** to use MQTT Discovery:

1. Navigate to the 'Settings' page in the Web UI
2. Enable MQTT Discovery by simply switching it on.
3. If enabled, an input field for the 'Discovery Prefix' setting will appear. If this is the first time enabling it, it is defaulted to 'homeassistant'. If you like to change this, make sure the `discovery_prefix` setting in Home Assistant is the same (see above).
4. Press 'Save'

Once saved, **AiLight** will notify your Home Assistant instance about the new light and your Ai-Thinker LED RGBW Light will appear almost instantaneously in Home Assistant. 

Some notes:
- **AiLight** will remember that your Ai-Thinker LED RGBW Light has been discovered already, so you need to do this configuration only once.
- **AiLight** will 'forget' the discovery if you change the hostname of your Ai-Thinker LED RGBW Light. This is because the hostname is used as the display name in Home Assistant.
- If you disable the MQTT discovery, **AiLight** will 'forget' the discovery, however you will see that in Home Assistant your Ai-Thinker LED RGBW Light is still present. This is because Home Assistant performs the discovery on runtime and currently there is no way to notify Home Assistant a device is no longer needed in the configuration. You will need to restart Home Assistant to have your Ai-Thinker LED RGBW Light removed.