---
title: Everything together
weight: 200
---
Let's set up a list of colours for the three lights
to cycle through. The first entry in the list will be ignored,
and we'll show cycling rainbows instead, so we'll leave that
dummy entry as black (all zero).

We'll use the light sensor to decide whether to turn the lights on or off, and an available input as a touch sensor to change the colours.

```python {linenos=table, hl_lines=""}
import board
import time
import neopixel
from touchio import TouchIn
from analogio import AnalogIn, AnalogOut

touch = TouchIn(board.A2)

# Analog input on A1
photocell = AnalogIn(board.A1)

# LED strip
pixels = neopixel.NeoPixel(board.D1, 3, brightness=1,
    auto_write=True, pixel_order=neopixel.GRBW)

def wheel(pos):
    # Input a value 0 to 255 to get a color value.
    # The colours are a transition r - g - b - back to r.
    if (pos < 0):
        return [0, 0, 0]
    if (pos > 255):
        return [0, 0, 0]
    if (pos < 85):
        return [int(pos * 3), int(255 - (pos*3)), 0]
    elif (pos < 170):
        pos -= 85
        return [int(255 - pos*3), 0, int(pos*3)]
    else:
        pos -= 170
        return [0, int(pos*3), int(255 - pos*3)]

colors = [
    (0, 0, 0, 0),
    (255, 0, 0, 0),
    (255, 255, 0, 0),
    (0, 255, 0, 0),
    (0, 255, 255, 0),
    (0, 0, 255, 0),
    (255, 0, 255, 0),
    (255, 255, 255, 0),
    (0, 0, 0, 255)
]
colorIndex = 0
pressTime = 0
on = False
i = 0
brightness = photocell.value
while True:
    if touch.value:
        colorIndex = (colorIndex+1) % len(colors)
        while touch.value:
            pass
        
    if i == 0:
        # only check the brightness every 256 loops
        # to avoid weird flashing effect
        brightness = photocell.value
        print(photocell.value)

    if brightness > 300:
        # It's dark. Turn the lights on!
        if colorIndex == 0:
            # Dummy colors. Show rainbow
            pixels.fill(wheel(i))
        else:
            # Show the current colors
            pixels.fill(colors[colorIndex])
    
    if brightness < 150:
        # It's light. Turn the lights off
        pixels.fill((0, 0, 0, 0))
    
    i = (i+1) % 256
```
