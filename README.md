# ESPHome Based Line Voltage (Baseboard Heating) Thermostat From Wall Switch
A while back, I wanted to add smart thermostats to my apartment.  However, I was surprised by the lack of inexpensive, line voltage (or baseboard) smart thermostats.  Especially since there's so many cheap smart wall switches, and a line voltage thermostat is just a wall switch with a temperature sensor and some type of UI.  So I decided to make some using [ESPHome](esphome.io) and [Home Assistant](home-assistant.io).  At the time, most smart switches used an ESP8266 so I designed a thermostat that could take advantage of the microcontroller that came with the switch.  I've since moved to a house with central heat but has a baseboard heater in the bathroom.  I wanted to be able to run the heater on a timer for showers in the winter so I redesigned the thermostat to use a ESP32 for the increased I/O to add buttons instead of the rotary encoder.

### A couple of notes/warnings:

1. :warning:**Warning**:warning: This project involves line voltage, which can be extremely dangerous and deadly.  I am not an electrician or electrical engineer so proceed at your own risk.  Always turn off the power at the breaker and ~~double~~ triple check the power is disconnected before touching any wires.
1. This project uses inexpensive smart switches.  They are technically rated for 10A but the quality control on the relays is probably not great, so I wouldn't recommend pushing the rating.  If you're worried or your heater is close to the rating, an option would be to replace the relay with something of higher quality.
1. Most smart switches no longer use an ESP as their microcontroller so you may have to replace the whole control board anyway.  [ESPHome](esphome.io) now supports the BK72xx and RTL87xx but I haven't played around with them at all so I have no idea if they could work.  ESPs are inexpensive so my recommendation, even for the rotary encoder version, would be to just replace the control board with your own ESP and save the headache.
1. I designed the covers in a CAD program called [Alibre Atom 3D](https://www.alibre.com/atom3d/).  It's not very widely used (I've never met anyone else who uses it) but it's functional, keeps everything local, and inexpensive.  I've uploaded the CAD files on the off-chance someone else uses Alibre, but .STP and .STL files are available too.

## Instructions Here:

[**Rotary Encoder**](/rotary-encoder/Rotary-Encoder.md) | [**Six Buttons**](/six-buttons/Six-Buttons.md)
:--------------------------------------------------:|:----------------------------------------------------------:
![](/rotary-encoder/images/finished_thermostat.jpg)  |  ![](/six-buttons/images/finished-thermostat-buttons.jpg)








