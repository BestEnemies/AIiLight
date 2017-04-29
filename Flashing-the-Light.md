The AiLight firmware has a feature that allows you to flash the light (i.e switch it on and off at a particular interval). At the moment it can only be activated by sending a specific instruction to the MQTT command topic and works differently than the Home Assistant flash feature.

The instruction to have the light flash is quite simple. Just provide the length in seconds and the colour you like the light to be flashing:

Example:
``` JSON
{"flash":"5", "color": {"r": 255, "g": 0, "b": 0}}
```

This will make your Ai-Thinker RGBW Light flash the colour red for 5 seconds.

**Note**: at the moment the light alternates between the specified colour and 'off' with an interval of 500ms. These can only be changed by modifying the source code. 
