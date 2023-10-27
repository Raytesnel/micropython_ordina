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

- ESP32 (with micropython installed, if you want to install your
  own -> [micropython docs](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html))
- Pycharm (v2023.1.4, newer versions plugin doesn't work :unamused: ) or VS code
    - micropython plugin (
      pycharm) / [RT-Thread MicroPython](https://marketplace.visualstudio.com/items?itemName=RT-Thread.rt-thread-micropython) (
      VScode)
- Micro usb (with data wires)

## Install Micropython plugin (pycharm)

In pycharm go to settings -> plugins and search for micropython (from JetBrains) install the plugin.
before we can program in micropython we need to tell the IDE that we are gonna use micropython instead of normal python.
to do so
Make a new project in pycharm (if not already done) and go to settings -> languages & Frameworks -> MicroPython. enable
the 'Enable Micropython support', device type: is ESP8266 and as last enable the Auto-detect device path. press OK/Apply
if you go to a python file (like main.py) pycharm will ask you to install the missing packages of micropython, and
install them.
'pyserial>=3.5,4.0', 'docopt>=0.6.2,0.7', 'adafruit-ampy>=1.0.5,1.1'

In project structure settings of Pycharm, please put all .venv and other folders to exclude otherwise
this will also be uploaded to the device.

### Connecting to the ESP32

If everything is okay you see a big M logo next to the Terminal. that is the Micropython terminal.
by clicking it you have 3 buttons

- Refresh the connection to the device
- Stop the communication with the device.
- clear(bin icon) clears the terminal screen.

to upload files, the normal run command (play button) will upload/replace it to the device

## Install Micropython plugin (VScode)

VScode --> Extension menu search for Micropython and select the RT-Thread Micropython (I know..)
install it, reload and done.
to start a micropython project you need to make a new micropython project by clicking the plus icon in the left bottom
corner("create micropython project"), follow steps to make and select folder and done.

### Connecting to the ESP32

In the left bottom corner you can (from left to right)

- create new micropython project (already done)
- (Dis)connect device
- Sync working directory with device (1 way uploading to device)
- Run current file on device(nice debugging tool)
- Code suggestions (don't know what it does)
- Stop microcontroller program, (kind of ctrl-C)

when selecting a text you can right mouseclick to only run the selected text on the device.(really nice)

## Micropython REPL

One of the nice features is the python REPL on the microcontroller, here we can test code snippets or type and
communicate with the device
to enter the REPL, connect with the device (pycharm refresh, VScode connect) and you will see somthing happening to the
terminal
if all went right you see our nice `>>` from the microcontroller. if you see weird stuff, try pressing CTRL-Cv(maybe it
was stuck in a program)
most used keys

- CTRL-C --> stop current program on device
- CTRL-D --> start boot.py and main.py
- CTRL-A --> enter Raw REPL (needed to upload files)
  CTRL -C & -D is mostly used when debugging, CTRL-A is mostly used by the plugins.

From REPL we can already test some sensors, actuators.
for example if you are in the REPL of the microcontroller you can type:

- `import machine` Imports a micropython specific lib for the use of pins, wifi, PWM etc.
- `led_pin = machine.Pin(2, machine.Pin.OUT)` Set the correct pin as a output pin (onboard led pin is 2)
- `led_pin.value(1)` Turn the led off
- `led_pin.value(0)` Turn the led on

Congratz, if everything is correct you have made the led blink :smile:.

# Write Hello World

To let the device behave as it should when powering on there should be some files writen to the device.
on the device there are minimal 2 files (normally)

- boot.py
- main.py

boot.py is mostly not used with small projects, boot.py is run when powering on the device / rebooting the device you
can handle things here like updates, import stuff stetting some important settings etc, you can see the boot.py as a
setup of the device before entering the main programm.
After it completes boot.py it will automatically run
main.py(and functions of boot.py is still available to main.py), you don't have to call main.py from boot.py

let's make a boot.py and main.py file in the project folder(locally) and write our first program.

Write a main loop where it prints in the terminal "hello world" and blink the onboard led to notify the user that
message is been sent.

note: if the program finishes (or you stop is with CTRL-C) all variables/object etc. are still in memory and can be used
in the REPL

For more information what Pins you can use and what to do with it see picture below.

After you succeeded, fiddle with it till the next assignment,
for example make the onboard led send morse code.

![link to ESP32 nodemcu pin layout](https://www.waveshare.com/img/devkit/accBoard/NodeMCU-32S/NodeMCU-32S-details-3.jpg)

# Car Project

Here we are gonna make 3 different projects (choose one with your group to work on.)

- [Drive Team](/module_drive/README.md#drive-team)
- [Sensor Team](/module_input/README.md#input-team)
- [Feedback Team](/module_feedback/README.md#feedback-team)

# IoT

What I Personally like from microcontrollers are 2 main things,

1: fast power down and start up. which is great for battery powered projects. (check for more
information [deepsleep](https://docs.micropython.org/en/latest/esp32/quickref.html#deep-sleep-mode)

2: Wifi / BLE capabilities, here you can really use microservices to make a huge system.
for now, we focus on Wi-Fi and especially on the communication
protocol [MQTT - liberary](https://github.com/peterhinch/micropython-mqtt). MQTT is a protocol to subscibe to topics and
publish messages to a topic without to much hassle.

for example a temperature sensor publishes `30°C` on topic `/livingroom/temperature` while the radiator is listening
also on the same topic, therefore when getting the `30°C` the radiator can turn off the radiator.
![content](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2018/12/MQTT-Diagram.png?w=750&quality=100&strip=all&ssl=1)

for the next assignment we are going to connect with eachother via MQTT.

use the `umqtt.simple` library to log into the MQTT
server [umqq.simple github page](https://github.com/micropython/micropython-lib/tree/master/micropython/umqtt.simple)
login address and login password is shared on the screen.

to check if your device is connected,
a welcome message on the home topic `/home` has been published (retained)

the goal is to get the motor speeding faster or slower with the input of the hand, and visualize the speed with the
feedback ledstrips.
Subscribe and publish on topics together, make agreements together about how and what to publish.

Good luck! And I hope you enjoyed it :)

# Extra's

## more used MQTT lib -> but more size

[MQTT lib github](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as)

## Importing Mip Packages

[Micropython pip libery](https://github.com/micropython/micropython-lib)

