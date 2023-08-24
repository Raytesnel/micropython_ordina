# Drive Team
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

## Summary Of Steps Stepper Motor (guide not mandatory) :
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


