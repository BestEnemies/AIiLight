![](images/ailight_logo.png)

_Since release: **DEV**_

If you prefer to have Home Assistant set up your Ai-Thinker LED RGBW Light automatically, then follow the steps below. **AiLight** supports Home Assistants' MQTT Discovery functionality, which avoids any manual configuration in Home Assistant.

### Home Assistant
By default, the MQTT Discovery functionality in Home Assistant is disabled, so first thing is to enable this. To do that, simply add `discovery: true` to your MQTT configuration. Additionally, you can set the discovery prefix used by Home Assistant. Your configuration should look something like this:

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
  