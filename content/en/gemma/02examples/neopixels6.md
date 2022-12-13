---
title: Neopixels (Part 6)
weight: 65
---
If you hold your finger down while the lights are on,
the rainbow stops cycling. This is slightly disappointing.
Let's fix that, and at the same time prepare ourselves so
we can have short presses and long presses.

```python {linenos=table, hl_lines="28 32-39"}
import board
import time
import neopixel
from touchio import TouchIn

touch = TouchIn(board.A2)

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

pressTime = 0
on = False
i = 0
while True:
    if touch.value and pressTime == 0:
        pressTime = time.monotonic()
    
    if not touch.value and pressTime != 0:
        holdTime = time.monotonic()-pressTime
        pressTime = 0
        if holdTime > 1:
            on = not on
    
    if on:
        pixels[0] = wheel(i)
        pixels[1] = (0, 255, 255, 0)
        pixels[2] = (0, 0, 0, 255)
    else:
        pixels.fill((0, 0, 0, 0))
    
    i = (i+1) % 256
```
