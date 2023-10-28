# MicroPython Ordina

A nice demo day about MicroPython with the use of ESP32 boards.

For the sake of time, the ESP32s that are handed to you are already flashed with MicroPython.
If you want to know more on how to do this and what happened, see:
[micropython gettings started docs](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html#)

# Hello World

Let's start with a simple excercise to get the device alive. The goal of this excercise is to
(1) get access to the REPL on the device, and (2) let the LED on the device blink.

## Requirements Hello World

Minimum requirements:

- ESP32 with MicroPython installed (if you want to install your
  own, see [MicroPython docs](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html))
- PyCharm >v2023.1.4 (on newer versions the plugin doesn't work :unamused:) with MicroPython plugin

  or

- VS Code with [RT-Thread MicroPython](https://marketplace.visualstudio.com/items?itemName=RT-Thread.rt-thread-micropython) extension installed 
- Micro-USB (with data wires)

## Installation for PyCharm

### Installing MicroPython plugin

In PyCharm go to file -> settings -> plugins and search for MicroPython (from JetBrains) and install the plugin.
Before we can program with MicroPython we need to tell the IDE that we are gonna use MicroPython instead of normal python.

To do so:

- Make a new project in PyCharm (if not already done).
- Go to file -> settings -> languages & Frameworks -> MicroPython.
- Enable the 'Enable Micropython support'-option, set the device type to ESP8266 and enable 'Auto-detect
  device path' and press OK/Apply.
- Now, if you go to a python file (like main.py) PyCharm will ask you to install the missing packages of
  MicroPython, please install them ('pyserial>=3.5,4.0', 'docopt>=0.6.2,0.7', 'adafruit-ampy>=1.0.5,1.1').
- In file -> settings -> project -> project structure, please exlude all .venv and other folders to exclude.
  Otherwise these will also be uploaded to the device.

### Connecting to the ESP32

If everything is okay, you now see a big "M" next to your integrated terminal. This is the MicroPython terminal.

If you click it you have 3 buttons:

- Refresh the connection to the device.
- Stop the communication with the device.
- Clear the terminal screen (bin icon).

To upload files to your board, the normal run command (play button) will upload your local code to the device.

## Installation for VS Code

### Installing MicroPython extension

VScode --> Extension menu search for Micropython and select the RT-Thread Micropython (I know..)
install it, reload and done.
to start a micropython project you need to make a new micropython project by clicking the plus icon in the left bottom
corner("create micropython project"), follow steps to make and select folder and done.

### Connecting to the ESP32

In the left bottom corner you can (from left to right):

- Create a new micropython project (already done).
- (Dis)connect to device.
- Sync your local working directory with device (1 way uploading to device).
- Run the current file on device (nice debugging tool).
- Code suggestions (don't know what it does).
- Stop the microcontrollers program, (kind of ctrl-C).

After selecting some code, you can right-click it to only run the selected text on the device (really nice).

## MicroPython REPL

One of the nice features is the python REPL on the microcontroller. There we can test code snippets or write code
and communicate with the device. To enter the REPL, connect with the device (PyCharm: refresh, VS Code: connect)
and you will see somthing happening in the terminal. If all went right, you now see our nice `>>` from the
microcontroller. If you see weird stuff, try pressing CTRL-C (maybe the microcontroller was stuck in a program).

Most used key combinations:

- CTRL-C -> stop current program on device
- CTRL-D -> start boot.py and main.py
- CTRL-A -> enter Raw REPL (needed to upload files)

CTRL-C & -D are mostly used during debugging, CTRL-A is mostly used by the plugins.

From the REPL we can already test some sensors and actuators. For example, you can type the following:

- `import machine` -> Imports a MicroPython-specific library for the use of pins, WiFi, PWM etc.
- `led_pin = machine.Pin(2, machine.Pin.OUT)` -> Sets the correct pin as a output pin (onboard led pin is 2).
- `led_pin.value(1)` -> Turns the led off.
- `led_pin.value(0)` -> Turns the led on.

Congratz, if everything is correct you have made the led blink :smile:!

## Write Hello World

To let the device behave as it should when powering on, some files should be writen to the device. There normally are
at least 2 files on the microcontroller:

- boot.py
- main.py

Usually, `boot.py` is not used in small projects. `boot.py` is run when powering on/rebooting the device. You can handle
things here like updates, import packages, setting some important settings/globals etc. You can see `boot.py` as a setup
script for the device before entering the main program. After `boot.py` completes, it will automatically run `main.py`.
(Functions defined in `boot.py` are still available in `main.py`.) You don't have to call `main.py` from `boot.py`.

Let's make `boot.py` and `main.py` files in the project folder (locally) and write our first program. Write a main-loop
that prints "hello world" to the terminal and blinks the onboard LED to notify the user that a message is sent.

Note: if the program finishes (or you stop it with CTRL-C) all variables/object etc. are still in memory and can be used
in the REPL.

For more information what Pins you can use and what to do with them, see the picture below.

After you succeed, fiddle with it until the next assignment. For example, make the onboard LED send morse code.

![NodeMCU-32S-details-3](https://github.com/Raytesnel/micropython_ordina/assets/66633722/1ac5c0e8-ff98-4b04-91a8-1eea7eee7402)

# Car Project

The group will be split in small team, that will work on 3 different projects (choose one to work on):

- [Drive Team](/module_drive/README.md#drive-team)
- [Sensor Team](/module_input/README.md#input-team)
- [Feedback Team](/module_feedback/README.md#feedback-team)

## IoT

Personally, I think the two main strengths of microcontrollers are:

1. Fast start up and power down, which is great for battery-powered projects. (Check
   [deepsleep](https://docs.micropython.org/en/latest/esp32/quickref.html#deep-sleep-mode) for more information.)
2. WiFi / BLE capabilities. You can really use microservices to make a huge system. For now, we focus on WiFi and especially
   on the communication protocol [MQTT library](https://github.com/peterhinch/micropython-mqtt). MQTT is a messaging protocol
   that allows you to subscibe to topics and publish messages to a topic without too much hassle.
   For example, a temperature sensor publishes `30°C` on topic `/livingroom/temperature`, while the radiator is listening on
   the same topic. Therefore, the radiator can switch off when it receives the `30°C`.
   
   ![content](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2018/12/MQTT-Diagram.png?w=750&quality=100&strip=all&ssl=1)

## Assignment

In the car project, we are going to communicate with eachother via MQTT. For this, use the `umqtt.simple` library to log into
the MQTT server [umqq.simple github page](https://github.com/micropython/micropython-lib/tree/master/micropython/umqtt.simple)
The login address and login password are shared on the screen. To check if your device is connected, a welcome message on the
home topic `/home` has been published (retained).

The goal of the assignment is to rotate the motor faster or slower (drive team) depending on the distance of an object to the sensor
(sensor team), and visualize that speed with the LED-strips (feedback team). Subscribe to and publish on topics, make agreements
together about how and what to publish.

Good luck! And I hope you enjoy it :)

# Extra's

## Other libraries

- More used MQTT library, but bigger [MQTT lib github](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as)
- Importing Mip Packages [MicroPython pip library](https://github.com/micropython/micropython-lib)
