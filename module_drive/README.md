# Drive Team

With this team, we are going to actuate a stepper motor. The goal is to make a script that awaits input from e.g. the
user to actuate the motor with a specific speed or a certain distance/number of rotations.

## List of materials:

- Stepper motor (nema 17)
- 12V Power adapter
- Stepper driver (TMC2208/TMC2209)
- Dupont cables (female - male 5-7x)

or

- DC motor
- 12V Power adapter
- H-bridge module
- Dupont cables (female - male 3x)

## Board Stepper Motor

For the stepper motor, you get a [TMC2209](https://learn.watterott.com/silentstepstick/pinconfig/tmc2209/) module
attached to a developer board for stepper-drivers to make your life easier. It works as follows:

- dir(rection) pin: give a low or high input to rotate left or right.
- step pin: everytime this pin gets a pulse (low, high, low) the motor will do a small step.
- en(able) pin: this powers the motor on or off, when the pin is LOW the motor is engaged. (This depends on stepper
  driver if LOW or HIGH.)
- VCC(red) pin: this is the logic voltage 3.3 - 5v.
- gnd(black) pin: this is the ground pin of the logic voltage.

There also is a microstepping configuration, with which you can divide steps into even smaller steps. The options are:
full-step (1:1), half-step (1:8) and microstepping (1:16), where every step of a motor is devided into 1, 8 or 16
smaller steps. We already set this up for you in 1:16. The relevant pins are:

- ms1: microstepping configuration (LOW or HIGH)
- ms2: microstepping configuration (LOW or HIGH)

The stepper motor is a nema 17, which has 200 steps per rotation. So with the pre-set microstepping a full rotation is
200*16=3200 steps.

## Guide Stepper Motor

This guide is not mandatory, but may help you in finishing the task:

- (bonus) Import logging (see [Importing mip packages](https://github.com/Raytesnel/micropython_ordina/blob/main/README.md#other-libraries))
- Make the motor turn with a while/for loop (make it alive)
- Make a callback timer to not obstruct the rest of the program when sending pulses to the motor
- Make sure you can receive input (distance & speed)
- Make the timing of the callback timer faster or slower (speeding up or slowing down)
- Make the callback timer stop when certain distance is achieved

Good luck, you can start for your self from here. (Hint: as we changed the led to ON or OFF in the 'Hello World'-exercise,
we changed the pin state to LOW(0) or HIGH(1).)

[//]: # (## done? try the DC motor)

[//]: # (DC motor works with a continously current instead of steps for movement. )

[//]: # (put power on the dc and it wil rotate. reverse the + and ground and it will reverse. )

[//]: # (PWM&#40;pulse-width modulation&#41; and it will change speed.)

[//]: # (to make the reversing of the + and ground easier you can use the H-bridge )

[//]: # (to reverse the rotation or stop it in total)
