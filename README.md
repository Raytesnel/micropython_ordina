# Micropython Ordina
A nice demo day about micropython with the use of ESP32

due to time the ESP32 that are given by us, are already flashed with Micropython, 
if you want to know more on how to do this and what happened.
[micropython gettings started docs](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html#)

# Hello World:

let's start with a simple excersize with getting the device alive:
the Goal of this excersize is to get the Repl on the device plus blinking a led on the device 

## Requirements Hello World:
Minimum requirements
- ESP32
- Pycharm / VSCode (VSCode is not preferred)
  - micropython plugin (pycharm) / Pymkr (VSCode)
- Micro usb (with data)

## Install Micropython plugin

In pycharm go to settings -> plugins and search for micropython (from JetBrains) install the plugin.
before we can programm in micropython we need to tell the IDE that we are gonna use micropython instead of normal python. to do so
Make a new project in pycharm (if not already done) and go to settings -> languages & Frameworks -> MicroPython. Enebale the 'Enable Micropython support', device type: is ESP8266 and as last enable the Auto-detect device path. press OK/Apply
if you go to a pythong file (like main.py) pycharm will ask you to install the missing packages of micropython, and install them.
'pyserial>=3.5,4.0', 'docopt>=0.6.2,0.7', 'adafruit-ampy>=1.0.5,1.1'

## Connecting to the ESP32

If everything is okay you see a big M logo next to the Terminal. that is the Micropython terminal.
by clicking it you have 3 buttons
- Refresh the connection to the device
- Stop the communication with the device.
- clear(bin icon) clears the terminal screen.

with the refresh button it tries to connect with the ESP device and you should see our trusting python console >> :)
Be aware that this is a python terminal from the device, not from your computer.
from here you can test sensors, actuators. 

for example 
- `import machine` Imports a micropython specific lib for the use of pins, wifi, PWM etc.
- `led_pin = machine.Pin(2, machine.Pin.OUT)` Set the correct pin as a output pin (onboard led pin is 2)
- `led_pin.value(1)` Turn the led off
- `led_pin.value(0)` Turn the led on
Congratz, if everything is correct you have done your first embedded programm with python.

# Write Hello World
to let the device behave as it should when powering on there should be some files writen to the device. 
on the device there are minimal 2 files 
- boot.py
- main.py
boot.py is mostly not used with small projects, boot.py is run when powering on the device / rebooting the device you can handle things here like updates, import stuff stetting some important settings etc, you can see the boot.py as a setup of the device before entering the main programm.
After it completes boot.py it will  automatticly run main.py, you don't have to call main.py from boot.py

lets make a boot.py and main.py file in the root system and write our first programm.
Write a main loop where it prints in the terminal "hello world" and blink the onboard led to notify the user that message is been send.

Good Job, fiddle with it till the next assignment, 
For more information what Pins you can use and what to do with it see picture below.
for example make the onboard led send morse code synchronised with the print statements in the REPL (terminal).

![link to ESP32 D1 mini pin layout](https://www.hobbyelectronica.nl/wp-content/uploads/2021/11/D1_mini_esp32_schema.jpg)


# Car Project

Here we are gonna make 3 different projects (choose one with your group to work on.)
- [Drive Team](/module_drive/README.md#drive-team)
- [Sensor Team](/module_input/README.md#input-team)
- [Feedback Team](/module_feedback/README.md#feedback-team)


# IoT 
What i Personally like from microcontrollers are 2 main things, 

1: fast power down and start up. which is great for battery powered projects. (check for more information [deepsleep](https://docs.micropython.org/en/latest/esp32/quickref.html#deep-sleep-mode)

2: Wifi / BLE capabilities, which you can make sepperate small microcontrollers into a huge complex system.
for now we focus on WiFi and especially on the communication protocol [MQTT - liberary](https://github.com/peterhinch/micropython-mqtt). MQTT is a protocol to subscibe to topics and publish messages to a topic without to much hassle.

for example a temperature sensor publishes `30°C` on topic `/livingroom/temperature` while the radiator is listening also on the same topic, therefore when getting the `30°C` the radiator can turn off the radiator.
![content](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2018/12/MQTT-Diagram.png?w=750&quality=100&strip=all&ssl=1)

for the next assignment we are going to connect with eachother via MQTT.

use the `umqtt.simple` library to log into the MQTT server [umqq.simple github page](https://github.com/micropython/micropython-lib/tree/master/micropython/umqtt.simple)
login address and login password is shared on the screen.

to check if your device is connected, 
a welcome message on the home topic `/home` has been published (retained)

the goal is to get the motor speeding faster or slower with the input of the hand, and visualize the speed with the feedback ledstrips.
Subscribe and publish on topics with each-other, make agreements with eachother, how and what to publish.

Good luck!


# Extra's
## more used MQTT lib -> but more size
[MQTT lib github](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as)
## Importing Mip Packages
[Micropython pip libery](https://github.com/micropython/micropython-lib)

