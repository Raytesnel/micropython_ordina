## Input Team

With this team, we are going to make a sensor to measure the distance from the sensor to a hand/object. We will use an
ultrasonic sensor for this.

## List of Materials

- Ultrasonic sensor

## Explanation Ultrasonic Sensor

The sensor is based on a pretty simple concept: the sensor pulses sound waves (in the ultrasonic frequencies). This signal
will bounce back if it hits an object. The sensor tries to receive this echo, and measure the time between sending the
signal and receiving its echo. The difference in time is used to calculate the distance from the sensor to the object.

![img.png](img.png)

The distance from the sensor to an object equals $( speed * time ) / 2$, where $speed$ is the speed of sound in air,
which is about 343.2 m/s.

The pins on the board are:

- vcc -> + (5v or 3.3v)
- trig -> trigger to transmit the signal (`high` is sending wave, `low` is stop sending wave)
- echo -> input pin, that will go from `low` to `high` when it receives something
- GND -> Ground

## Guide

- (bonus) Import logging, see [Importing mip packages](https://github.com/Raytesnel/micropython_ordina/blob/main/README.md#other-libraries)
- Setup all pins and be able to send a sound wave (10ms or so)
- Setup a timer that will start when you start transmitting and stop when the pin goes to high. See: (time
  pulse)[https://docs.micropython.org/en/latest/library/machine.html#machine.time_pulse_us]
- Calculate the distance and return it (check if you have a `time out`, for wrong distances)
