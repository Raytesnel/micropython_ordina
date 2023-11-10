# Feedback Team

With this team, we are going to light up some LEDs. The goal is to make a script that waits for input
from e.g. a user to actuate the motor for a specific speed and distance/rotations.

## List of materials

- ~10 individually addressable LEDS

## Explanation Individually Addressable LEDS

On the LEDs there are 4 wires:

- plus (red)
- ground (black)
- signal in (white)

What makes these leds different from normal LEDs?

- The microcontroller will send a list of values to the first LED. These are RGB-values, so e.g. (255, 127, 0)
  corresponds with full red, half green, and no blue (resulting in orange).
- The first LED will take and remove the first value.
- The rest of the values will be passed on to the next LED.
- This will repeat until all LEDs reveived their commands.

With this you can make different fluent motions with the 3 colors combined. More info on a special MicroPython
library and these leds [WS2812 LED](https://docs.micropython.org/en/latest/esp8266/tutorial/neopixel.html)

## Guide

- (bonus) Import logging (see [Importing mip packages](https://github.com/Raytesnel/micropython_ordina/blob/main/README.md#other-libraries))
- Turn all LEDs into one color (255 if full color, 0 is no color for each RGB in the LED)
- Make a looping color change
- Map the LEDs to a 0-100% with some user input
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
