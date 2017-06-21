To be able to upload firmware to your Ai-Thinker LED RGBW light, a connection from your PC to the light must be made. The inner PCB of the light has 5 PCB pads labelled 3V3, GND, RX, TX and IO0. These were most likely used at the factory to flash the factory firmware.

How do we then make such a connection? There are two ways:

1. Solder wires to the 5 PCB pads and connect these wires to your FTDI (or equivalent) adapter. Xose Pérez has written an excellent [article](http://tinkerman.cat/ailight-hackable-rgbw-light-bulb/) on his blog how you can make such a connection, and upload your own firmware.

2. Use an [AiLight Jig](https://www.sachatelgenhof.nl/blog/ailight-jig): this jig is designed specifically for the Ai-Thinker LED RGBW light. It allows for uploading custom firmware without soldering any wires to the light’s PCB IO and test contacts. And, if you have more than one Ai-Thinker LED RGBW light, you can use the jig over and over, saving you a lot of hassle!

