# ESPHome Based Line Voltage (Baseboard Heating) Thermostat From Wall Switch
I recently wanted to add smart thermostats to my apartment.  However, I was surprised by the lack of inexpensive, line voltage (or baseboard) smart thermostats.  Especially since there's so many cheap smart wall switches, and a line voltage thermostat is just a wall switch with a temperature sensor and some type of UI.  So I decided to make some.  I also set myself a goal of making the entire thing reversible back to a wall switch if I ever moved to a place where I no longer needed line voltage thermostats and I *mostly* succeeded.  I had to de-solder the microswitch, but otherwise everything is reversible and it'd be easy enough to re-solder if I want to switch back.

## :warning:***Warning***:warning: 
***This project involves line voltage, which can be extremely dangerous and deadly.  I am not an electrician or electrical engineer so proceed at your own risk.  Always turn off the power at the breaker and ~~double~~ triple check the power is disconnected before touching any wires.***

![](/images/finished_thermostat.jpg)

## Parts List ##
1. A ESP based smart wall switch, with accessible GPIO pins.  I used a Laghten smart switch ([Amazon Link](https://www.amazon.com/gp/product/B07VMDS9RJ)), but others will probably work as well.
1. A USB-UART (USB to TTL converter) for flashing 
1. DHT22/AM2302 ([Amazon Link](https://www.amazon.com/gp/product/B01JGNL2LM))
1. Rotary encoder with push button ([Amazon Link](https://www.amazon.com/gp/product/B08728K3YB))
1. 128X64 (0.96") SSD1306 OLED display ([Amazon Link](https://www.amazon.com/PEMENOL-Display-0-96inch-Raspberry-Microcontroller/dp/B07F3KY8NF))
1. JST battery connectors (optional)
1. A 4.7K resistor
1. 4x wire nuts (I reused the ones already in the wall)
1. 2X #6 screws for the switch
1. 3D printed case
1. Hot glue gun
1. 2X #6 x 1" decorative wall plate screws (colored to match your 3D printed case)

## Flashing ##
I recommend flashing the ESP before you start soldering parts onto it.  Unfortunately Tuya Convert no longer seems to work due to the new Tuya firmware, so you'll have to use a USB-UART converter and solder connections.  My smart switch was based on a TYWE3S and I used the Tasmota instructions available [here](https://tasmota.github.io/docs/devices/TYWE3S/) for flashing.

:warning: *Power the ESP from 3.3V on the USB-UART during flashing.* ***Do not connect line power during flashing!*** :warning:

I found it easiest to remove the entire board with the ESP from the switch to flash and solder on components.

![Flashing](/images/flashing.jpg)

In addition to the thermostat.yaml file, you will also need a font file (I used  [Open Sans](https://fonts.google.com/specimen/Open+Sans#standard-styles)) and 4 image files from Material Design Icons:
* [fire](https://materialdesignicons.com/icon/fire)
* [radiator](https://materialdesignicons.com/icon/radiator)
* [radiator-off](https://materialdesignicons.com/icon/radiator-off)
* [thermometer](https://materialdesignicons.com/icon/thermometer)

The MDI icons and font file will need to be in the same directory as the .yaml file.

## Soldering Components
Here is the pinout I used.  Other configurations would likely work but I know this one worked for me.

![pinout](/images/thermostat_pinout.jpg)

I also used pre-wired JST connectors to make removing the cover easier once all the components were soldered together and I used sharpie to color code the different connections.

![JST Connectors](/images/jst-connectors.jpg)

You also need to de-solder the microswitch or the encoder won't fit.  Save it along with the front plates if you ever want to change it back to a wall switch.

![microswitch](/images/microswitch.jpg)

### OLED Display
In order to get the OLED display to fit into the case, I de-soldered the header pins from the board and just soldered the wires directly onto the back.

![OLED](/images/oled.jpg)

### Temperature Sensor
The AM2302 requires a pull-up resistor on the data line, so that was soldered on first along with the data wire.  Then the power wires were added.

![](/images/am2302-resistor.jpg)
![](/images/am2302-final.jpg)

### Rotary Encoder
The encoder has 2 separate connections.  The encoder and the push button.  For the push button, one connection should be GND and the other connected to an GPIO pin.  For the encoder portion, the center pin should be GND and the other two connected to GPIO pins.  I connected the two GND connections at the encoder and only ran one wire back to the ESP's GND.

![encoder](/images/encoder.jpg)

### Case
The case was designed in Alibre Atom 3D.  I've included the original file as well as the .stl and .step if anyone wants to modify them.  I printed mine on my Monoprice Select Mini Pro in black PETG.  You can print it either face up or face down.  Face up requires a lot more filament for supports but gives you a better front surface.  Face down, you still need supports for where the rotary encoder goes.

![case](/images/cad_front.jpg)

## Putting It All Together
Before gluing or closing anything up, it's always good to do a quick test to make sure all your connections are secure.

**:warning: When testing using line voltage, always put wire nuts over any unconnected wires (switched wire) and never touch any exposed connections! :warning:**

![testing](/images/testing.jpg)

(This image was taken before I realized the microswitch didn't fit.)

I like to try and make things as re-usable as possible so I prefer to use hot glue to hold everything together.  

![](/images/inside-case.jpg)

### Installing It On The Wall
As I am not an electrician, I don't want to give detailed instructions on how to install.  The basics are:
1. :warning: Make sure the power is turned off at the breaker :warning:
1. :warning: Check again that the power is turned off :warning:
1. :warning: Use a non-contact voltage tester to make sure theres no power! (Seriously this is important!) :warning:
1. Connect the wires appropriately.
1. Screw in the switch
	
	![](/images/thermostat_open.jpg)
1. Connect the 3.3V and data cables to the components in the 3D printed case.
1. Screw on the 3D printed case
1. Cross your fingers & turn back on the power

## Thermostat Operation
The thermostat will work even when disconnected from Home Assistant/ ESPHome.  To change the temperature, you short press the rotary encoder and you can adjust the temperature set-point in 0.1<sup>o</sup> increments.  Another short press sets the new set-point.  To toggle the thermostat on or off, simply long press the rotary encoder.
