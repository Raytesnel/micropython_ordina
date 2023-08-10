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
For more information what Pins you can use and what to do with it. [link to ESP32 D1 mini pin layout](https://www.hobbyelectronica.nl/wp-content/uploads/2021/11/D1_mini_esp32_schema.jpg)
for example make the onboard led send morse code synchronised with the print statements in the REPL (terminal).


# Car Project

Here we are gonna make 3 different projects
- [Actuator Team](#actuator-team)
- [Sensor Team](#sensor-team)
- [Feedback Team](#feedback-team)

# Actuator Team
In this team we are gonna actuate a stepper motor and as bonus asignment a DC motor.
the goal is to make a script that awaits for input from for example the user to actuate the motor for a specific speed and distance/rotations.

## Motor Requirements:
- Stepper motor (nema 17)
- 12 V power adaptor
- stepper driver (TMC2208/TMC2209)
- dupont cables (female - male 5-7x)
or
- DC motor
- 12 V power adaptor
- H-brug module
- dupont cables (female - male 3x)

## Summary Stepper Hardware
for the stepper motor you get a [TMC2209](https://learn.watterott.com/silentstepstick/pinconfig/tmc2209/) module pressed on a developer board for stepperdriveers to make your life now easier.
it works as follows, 
- dir(rection) pin: give a low or high input to rotate left or right.
- step pin: everytime this pin gets a pulse (low,high,low) the motor will do a small step.
- en(able) pin: this makes the motor powered on or off, when the pin is LOW the motor is engaged. (depends on stepper driver if LOW or HIGH)
- VCC(red) pin: this is the logic voltage 3.3 - 5v
- gnd(black) pin: this is the ground pin of the logic voltage

microstepping configuration, where you can switch between full-step(1:1), half-step(1:8) and microstepping(1:16) where every step of a motor is devided by 1,8 of 16 smaller steps.
- ms1: microstepping configuration (LOW or HIGH)
- ms2: microstepping configuration (LOW or HIGH)
we already set this up for you in 1:16

the Stepper motor is a Nema 17 where it as 200 steps per rotation
so with microstepping a full rotation is 200*16 steps.

## Summary Of Steps Stepper Motor :
- (bonus) import logging (see [importing mip packages](#importing-mip-packages) )
- Make motor turn with while/for loop (make it alive)
- Make callback timer to not obstruct the rest of the programm instead of the while loop
- Make a input function to receive input from user (distance & speed)
- Make the timing of the callback timer faster or slower (speeding up or slowing down)
- Make the callback timer stop when certain distance is achieved

Good luck, you can start for your self from here or if you don't know how to continue follow the steps below. 
(hint, as the we changed the led to ON or OFF we changed the pin state to LOW(0) or HIGH(1))

### Stepper Motor Step 1:
hook up the pins from the ESP32 to the stepper module (hint, light green are always safe to use from the [pin layout](https://www.hobbyelectronica.nl/wp-content/uploads/2021/11/D1_mini_esp32_schema.jpg))
example:
`dir_pin = machine.Pin(17, machine.Pin.OUT)`
in the main.py

- Put the `en pin` LOW
- Put the `dir pin` Low or HIGH (left or right)
- Make a while loop that changes state of the `step pin` and a `timer.sleep_ms(10)`

upload to device and see the result

### Stepper Motor Step 2:
we can't use other functions of out main.py while our motor is turning, this is not ideal especialy that we can't receive changes as speeding up or slowing down while the main programming is running the motor.
in the ideal world you want the program to loop as fast as possible over input sensors and handle the acuators with callbacks, in the Machine lib there is a timer handles. every board has some hardware clocks to use the timers on. [Machine.timer class](https://docs.micropython.org/en/latest/esp32/quickref.html?#timers)

in the main.py

- make a callback function that makes a step on the stepper motor
- make a timer that callback to the stepper motor callback function
- make a `while True:` with `pass` make make sure the main.py is alive while the callback is doing it's job

### Stepper Motor Step 3:
### Stepper Motor Step 4:
### Stepper Motor Step 5:

# Actuator Bonus:

## Sensor Team
In this team we are gonna make a sensor to sense the height from the sensor till the hand/object
for this we use a Ultrasonic sensor with a bonus asignment with a TOF(Time-OF-Flight) sensor.

## Sensor Requirements:
## Summary Ultrasoon Hardware
## Summary Of Steps Ultrasoon Sensor:
### Ultrasoon Sensor Step 1:
### Ultrasoon Sensor Step 2:




# Feedback Team

## Sensor Requirements:
## Summary Ultrasoon Hardware
## Summary Of Steps Ultrasoon Sensor:
### Ultrasoon Sensor Step 1:
### Ultrasoon Sensor Step 2:

# IoT 
What i Personally like from microcontrollers are 2 main things, 
1: fast power down and start up. which is great for battery powered projects. (check for more information [deepsleep](https://docs.micropython.org/en/latest/esp32/quickref.html#deep-sleep-mode)
2: Wifi / BLE capabilities, which you can make sepperate small microcontrollers into a huge complex system.
for now we focus on WiFi and especially on the communication protocol [MQTT - liberary](https://github.com/peterhinch/micropython-mqtt). MQTT is a protocol to subscibe to topics and publish messages to a topic without to much hassle.
for example a temperature sensor publishes 30°C on topic /livingroom/temperature while the radiator is listening also on the same topic, therefore when getting the 30°C message it shutsdown the radiator.
![content](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2018/12/MQTT-Diagram.png?w=750&quality=100&strip=all&ssl=1)

for the next assignment we are gonna connect with eachother.

use the `umqtt` liberary to login the MQTT server [umqq.simple github page](https://github.com/micropython/micropython-lib/tree/master/micropython/umqtt.simple)
login adres and login password is shared on the screen.
to check if your device is connected, 
a welcom message on the home topic / is been publish (retained)
the goal is to get the motor speeding faster or slower with the input of the hand, and visualize the speed with the feedback ledstrips.
subscripe and publish on topics with eachother, make agreements with eachother, how and what to publish.

Good luck!


# Extra's
## more used MQTT lib -> but more size
[MQTT lib github](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as)
## Importing Mip Packages
[Micropython pip libery](https://github.com/micropython/micropython-lib)

