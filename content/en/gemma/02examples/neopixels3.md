---
title: Neopixels (Part 3)
weight: 62
---
At the moment, we need to hold down the touch pad to keep the lights on—hardly a useful feature for a lamp! Let's change that so that touching the touch pad changes the light from off to on, and back again.

```python {linenos=table, hl_lines="12 15 17"}
import board
import time
import neopixel
from touchio import TouchIn

touch = TouchIn(board.A2)

# LED strip
pixels = neopixel.NeoPixel(board.D1, 3, brightness=1,
    auto_write=True, pixel_order=neopixel.GRBW)

on = False
while True:
    if touch.value:
        on = not on
    
    if on:
        pixels[0] = (255, 0, 0, 0)
        pixels[1] = (0, 255, 255, 0)
        pixels[2] = (0, 0, 0, 255)
    else:
        pixels.fill((0, 0, 0, 0))
```
