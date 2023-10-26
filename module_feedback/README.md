# Feedback Team

In this team we are going to light up some LED's .
the goal is to make a script that awaits for input from for example the user to actuate the motor for a specific speed
and distance/rotations.

## Sensor Requirements:

~10 individual addressable LEDS

## Summary Individual Addressable LEDS

on the leds there are 4 wires,

- plus (red)
- ground(black)
- signal in (white)
- signal out (yellow)

what makes these leds different then normal leds?

- The microcontroller will send a list of parameters to the first led.
- It will take the first item (and change is values,)
    - (255,127,0) is corresponding to RGB --> full red, half green, no blue
- The rest of the list will be passed on to the next led
- this will be repeated till all leds has its command received

with this you can make different fluent motions with the 3 colors combined.
more info on a special lib of micropython and these leds
[WS2812 LED](https://docs.micropython.org/en/latest/esp8266/tutorial/neopixel.html)

## Summary Of Steps LEDS:

- (bonus) import logging (see [importing mip packages](#importing-mip-packages) )
- Make all leds turn one color (255 if full color 0 is no color for each RGB in the led)
- Make a looping color change
- Map the leds to a 0-100% with some user input
- Make it nice and colorfull :)

[//]: # (## done? try the servo motor:)

[//]: # ()

[//]: # (we can also show how fast somthing is with servo.)

[//]: # (servos have also 3 wires.)

[//]: # ()

[//]: # (- red -> +)

[//]: # (- brown -> ground)

[//]: # (- yellow -> signal)

[//]: # ()

[//]: # (This small servomotor is controlled using a pulse width modulated &#40;PWM&#41; signal with a frequency of 50 Hz, i.e. one pulse)

[//]: # (every 20ms. The position of the actuator is determined by the duration of the pulses, usually varying between 1ms and)

[//]: # (2ms.)

[//]: # ()

[//]: # (max what this servo can is 180° rotation. so in short, with a freq of 50hz, and full 2.4 ms is 180° while 1ms with 50hz)

[//]: # (is 0° position. min a normal duty cycle is with 1023 &#40;full pwm&#41; so you need to recalculate the `duty` to the correct)

[//]: # (duty.)

[//]: # ()

[//]: # ([PWM micropython]&#40;https://docs.micropython.org/en/latest/esp32/tutorial/pwm.html&#41;)

