---
title: Other things to try
weight: 3
---

## Light sensor
*from [microbit.org](https://microbit.org/projects/make-it-code-it/sunlight-sensor/?editor=python)*

```python
from microbit import *

while True:
    if display.read_light_level() > 100:
        display.show(Image(
        "90909:"
        "09990:"
        "99999:"
        "09990:"
        "90909"))
    else:
        display.clear()
```

## Max/min temperature recorder
*from [microbit.org](https://microbit.org/projects/make-it-code-it/max-min-thermometer/?editor=python)

```python
from microbit import *

currentTemp = temperature()
max = currentTemp
min = currentTemp

while True:
    display.show('.')
    currentTemp = temperature()
    if currentTemp < min:
        min = currentTemp
    if currentTemp > max:
        max = currentTemp
    if button_a.was_pressed():
        display.scroll(min)
    if button_b.was_pressed():
        display.scroll(max)
    sleep(1000)
    display.clear()
    sleep(1000)
```

## Teleporting duck
*from [microbit.org](https://microbit.org/projects/make-it-code-it/teleporting-duck/?editor=python)*

Note: The radio group is a number between 0 and 255. Microbits set to the same group can send and receive messages. Microbits set to different groups can't share messages. In this example the group is set to 23, but you should change this value if someone else is using channel 23.

```python
from microbit import *
import radio
radio.config(group=23)
radio.on()

while True:
    message = radio.receive()
    if message:
        display.show(Image.DUCK)
    if accelerometer.was_gesture('shake'):
        display.clear()
        radio.send('duck')
```

## Compass
For detecting strong magnetic fields, like those from a magnet you might use to stick something to the fridge, you do not need to calibrate the magnetometer (compass sensor). You do need to calibrate it to detect the relatively small magnetic field of the earth. The microbit will ask you to tilt it until all the display leds are lit.

```python
from microbit import *
compass.calibrate()

while True:
    bearing = compass.heading()
    if bearing < 45 or bearing > 315:
        display.show('N')
    else:
        display.show(' ')
```
