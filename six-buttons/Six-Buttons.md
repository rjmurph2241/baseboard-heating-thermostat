# Button Thermostat from Smart Switch

## :warning:***Warning***:warning: 
***This project involves line voltage, which can be extremely dangerous and deadly.  I am not an electrician or electrical engineer so proceed at your own risk.  Always turn off the power at the breaker and ~~double~~ triple check the power is disconnected before touching any wires.***

![](/six-buttons/images/finished-thermostat-buttons.jpg)

## Parts List ##
1. A inexpensive smart switch.
1. A ESP32 which fits in the case.  I used a D1 Mini ESP32. ([Amazon Link](https://www.amazon.com/s?k=ESP32+D1+mini))
1. DHT22/AM2302 ([Amazon Link](https://www.amazon.com/gp/product/B01JGNL2LM))
1. 6X 12x12x7.3mm momentary buttons ([Amazon Link](https://www.amazon.com/gp/product/B07CG7VTGD/))
1. Prototypeing PCB Board ([Amazon Link](https://www.amazon.com/s?k=prototype+PCB+board))
1. 128X64 (0.96") SSD1306 OLED display ([Amazon Link](https://www.amazon.com/PEMENOL-Display-0-96inch-Raspberry-Microcontroller/dp/B07F3KY8NF))
1. KF2510 Wire Connectors (Optional) ([Amazon Link](https://www.amazon.com/s?k=KF2510))
1. 4x wire nuts (I reused the ones already in the wall)
1. 2X #6 screws for the switch
1. 3D printed case
1. Hot glue gun
1. 2X #6 x 1" decorative wall plate screws (colored to match your 3D printed case)

## Soldering Components ##

### Case and ESP ###

In order to fit, the wires need to be soldered directly to the ESP without headers.  Then I used some 90<sup>o</sup> headers to connect to the 3.3V, GND, and switch I/O from the smart switch and hot-glued the ESP32 in place.

![](/six-buttons/images/replaced-esp.jpg) 

I connected the buttons, screen, and AM2302 with KF2510 connectors to make everything easy to assemble and take apart.  You could also just solder everything directly but it would probably be unwieldy.

### Buttons ###

I wired the buttons in a pull-up configuration (so they pulled to ground when pressed).  In order to fit the case they need to be soldered on a 0.6 in (15.24 mm) grid, which works out to 7 solder points center to center.

![](/six-buttons/images/button-back.jpg)
![](/six-buttons/images/button-front.jpg)


### OLED Display
In order to get the OLED display to fit into the case, I de-soldered the header pins from the board and just soldered the wires directly onto the back.

![OLED](/six-buttons/images/soldered-screen.jpg)

### Case ###
The case was designed in Alibre Atom 3D.  I've included the [original file](/six-buttons/thermostat_cover_buttons.AD_PRT) as well as the .stl and STEP files (on [Printables](https://www.printables.com/model/1037639-smart-baseboard-heater-thermostat)) if anyone wants to modify them.  I printed mine on my Ender 3 Pro in black PETG.  You can print it either face up or face down.  Face up requires a lot more filament for supports but gives you a better front surface.

![case](/six-buttons/images/six-button-cad.jpg)

## Putting It All Together
I like to try and make things as re-usable as possible so I prefer to use hot glue to hold everything together.  

![](/six-buttons/images/backside.jpg)

Before gluing or closing anything up, it's always good to do a quick test to make sure all your connections are secure.

**:warning: When testing using line voltage, always put wire nuts over any unconnected wires (switched wire) and never touch any exposed connections! :warning:**

### Installing It On The Wall
As I am not an electrician, I don't want to give detailed instructions on how to install the high voltage aspects.  The basics of installing the thermostat are:
1. :warning: Make sure the power is turned off at the breaker :warning:
1. :warning: Check again that the power is turned off :warning:
1. :warning: Use a non-contact voltage tester to make sure theres no power! (Seriously this is important!) :warning:
1. Connect the wires appropriately.
1. Screw in the switch
1. Connect the 3.3V and data cables to the components in the 3D printed case.
1. Screw on the 3D printed case
1. Cross your fingers & turn back on the power

### YAML Configuration

You'll need to set the substitutions at the top of the YAML file before you flash using ESPHome.  You'll also need to set your wifi_ssid, wifi_password, api_encryption (key) and ota_password in your secrets file.  More information on the secrets file is in the [ESPHome documentation](https://esphome.io/guides/faq.html)

## Thermostat Operation
- The thermostat will work even when disconnected from Home Assistant.  
- The large number is the current temperature and the small number is the set-point.
- The thermostat will toggle between the radiator off and radiator on symbol depending on it's state.
- The thermostat will display the flame icon while the heater is running.
- The thermostat will display the clock icon if the timer is running.

There are six buttons, I currently have them set to:

Temperature up (by 0.5 <sup>o</sup>)|Toggle On/Off|30 minute timer
:--:|:--:|:--:
**Temperature down (by 0.5 <sup>o</sup>)** | **Toggle preset (Toggle between 69<sup>o</sup> and 77<sup>o</sup> )** | **1 hour timer**

