# Drive Team

In this team we are going to actuate a stepper motor.
the goal is to make a script that awaits for input from for example the user to actuate the motor for a specific speed
and distance/rotations.

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

for the stepper motor you get a [TMC2209](https://learn.watterott.com/silentstepstick/pinconfig/tmc2209/) module pressed
on a developer board for stepper-drivers to make your life now easier.
it works as follows,

- dir(rection) pin: give a low or high input to rotate left or right.
- step pin: everytime this pin gets a pulse (low,high,low) the motor will do a small step.
- en(able) pin: this makes the motor powered on or off, when the pin is LOW the motor is engaged. (depends on stepper
  driver if LOW or HIGH)
- VCC(red) pin: this is the logic voltage 3.3 - 5v
- gnd(black) pin: this is the ground pin of the logic voltage

microstepping configuration, where you can switch between full-step(1:1), half-step(1:8) and microstepping(1:16) where
every step of a motor is devided by 1,8 of 16 smaller steps.

- ms1: microstepping configuration (LOW or HIGH)
- ms2: microstepping configuration (LOW or HIGH)
  we already set this up for you in 1:16

the Stepper motor is a Nema 17 where it as 200 steps per rotation
so with microstepping a full rotation is 200*16 steps.

## Summary Of Steps Stepper Motor (guide not mandatory) :

- (bonus) import logging (see [importing mip packages](#importing-mip-packages) )
- Make motor turn with while/for loop (make it alive)
- Make callback timer to not obstruct the rest of the program when sending pulses to the motor
- Make sure you can receive input from a user (distance & speed)
- Make the timing of the callback timer faster or slower (speeding up or slowing down)
- Make the callback timer stop when certain distance is achieved

Good luck, you can start for your self from here
(hint, as we changed the led to ON or OFF in the 'hello world' we changed the pin state to LOW(0) or HIGH(1))


[//]: # (## done? try the DC motor)

[//]: # (DC motor works with a continously current instead of steps for movement. )

[//]: # (put power on the dc and it wil rotate. reverse the + and ground and it will reverse. )

[//]: # (PWM&#40;pulse-width modulation&#41; and it will change speed.)

[//]: # (to make the reversing of the + and ground easier you can use the H-bridge )

[//]: # (to reverse the rotation or stop it in total)
