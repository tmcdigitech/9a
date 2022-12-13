---
title: Cycling colours
---

[TIP]
This is a tip!

```python
import time
import neopixel
import adafruit_dotstar
import pulseio
from analogio import AnalogIn
import board

pixpin = board.D0
numpix = 3
pixels = neopixel.NeoPixel(pixpin, numpix, brightness = 0.5, auto_write=True, pixel_order=neopixel.GRBW)

dotstar = adafruit_dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1)

vibrationPin = AnalogIn(board.A0)

def get_voltage(pin):
    return (pin.value * 3.3) / 65536

# Named colours
RED = (255, 0 , 0, 0)
BLUE = (0, 0, 255, 0)
GREEN = (0, 255, 0, 0)
OFF = (0, 0, 0, 0)

# List of colours to cycle through
colours = [RED, GREEN, BLUE, (255,0,255)]

# Index of which colour in the list we're on
coloursIndex = 0

# Timer for when to print the vibration sensor value
printTimer = 0

# Timer to make sure that we wait
# for one vibration to have stopped
# before we check for the next
debounce = 0

# Timer for changing colours if we're on
colourTimer = 0

# Whether the light is on or not
on = False

# Turn lights off to start
pixels.fill((0,0,0,0))
while True:
    dotstar[0] = (0,0,printTimer)
    vibration = get_voltage(vibrationPin)

    # Check the timers and reset them if they've gone off
    if printTimer == 0:
        printTimer = 255
        print(vibration)

    if colourTimer == 0:
        colourTimer = 255
        coloursIndex = (coloursIndex + 1)%len(colours)
        if on:
            pixels.fill(colours[coloursIndex])
        else:
            pixels.fill(OFF)

    if debounce == 0 and vibration < 0.8:
        debounce = 255
        print(vibration)
        on = not on
        if on:
            pixels.fill(colours[coloursIndex])
        else:
            pixels.fill(OFF)


    printTimer -= 1
    colourTimer -= 1
    debounce -= 1
    if debounce < 0:
        debounce = 0
```