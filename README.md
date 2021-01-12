

# ESPHome Based Line Voltage (Baseboard Heating) Thermostat From Wall Switch
I recently wanted to add smart thermostats to my apartment.  However, I was surprised by the lack of inexpensive, line voltage (or baseboard) smart thermostats.  Especially since there's so many cheap smart wall switches, and a line voltage thermostat is just a wall switch with a temperature sensor and some type of UI.  So I decided to make some.  I also set myself a goal of making the entire thing reversible back to a wall switch if I ever moved to a place where I no longer needed line voltage thermostats and I *mostly* suceeded.  I had to desolder the microswitch, but otherwise everything is reversible and it'd be easy enough to resolder if I want to switch back.

## :warning:***Warning***:warning: 
***This project involves line voltage, which can be extremely dangerous and deadly.  I am not an electrician or electrical engineer so proceed at your own risk.  Always turn off the power at the breaker and ~~double~~ triple check the power is disconnected before touching any wires.***

## Parts List ##
1. A ESP based smart wall switch, with accessible GPIO pins.  I used a Laghten smart switch ([Amazon Link](https://www.amazon.com/gp/product/B07VMDS9RJ)), but others will probably work as well.
1. A USB-UART (USB to TTL converter) for flashing 
1. DHT22/AM2302
1. Rotary encoder with push button
1. 128X64 (0.96") SSD1306 OLED display
1. JST battery connectors (optional)
1. A couple 4.7K resistors
1. 4x wire nuts (I reused the ones already in the wall)
1. 2X #6 screws for the switch
1. 3D printed case
1. Hot glue gun
1. 2X #6 x 1" decorative wall plate screws (colored to match your 3D printed case)

## Flashing ##
I recommend flashing the ESP before you start soldering parts onto it.  Unfortunately Tuya Convert no longer seems to work due to the new Tuya firmware, so you'll have to use a USB-UART converter and solder connections.  My smart switch was based on a TYWE3S and I used the Tasmota instructions available [here](https://tasmota.github.io/docs/devices/TYWE3S/) for flashing.

:warning: *Power the ESP from 3.3V on the USB-UART during flashing.* ***Do not connect line power during flashing!*** :warning:

I found it easiest to remove the entire board with the ESP from the switch to flash and solder on components.

<img src="/images/flashing.jpg" width="250px" />

![Flashing](/images/flashing.jpg)

In addition to the thermostat.yaml file, you will also need a font file (I used  [Open Sans](https://fonts.google.com/specimen/Open+Sans#standard-styles) and 4 image files of Material Design Icons:
* [fire](https://materialdesignicons.com/icon/fire)
* [radiator](https://materialdesignicons.com/icon/radiator)
* [radiator-off](https://materialdesignicons.com/icon/radiator-off)
* [thermometer](https://materialdesignicons.com/icon/thermometer)
