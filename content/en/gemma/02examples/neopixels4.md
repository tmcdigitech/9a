---
title: Neopixels (Part 4)
weight: 63
---
In part 3 we added a touch switch, but the processor in Gemma is *so fast* compared with our finger movements that it is nearly impossible to reliably turn it on or off. Let's force the processor to wait until we've taken our finger off the touch switch before continuing, thus ensuring each touch registers only once.

```python {linenos=table, hl_lines="16-17"}
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
        while touch.value:
            pass
    
    if on:
        pixels[0] = (255, 0, 0, 0)
        pixels[1] = (0, 255, 255, 0)
        pixels[2] = (0, 0, 0, 255)
    else:
        pixels.fill((0, 0, 0, 0))
```
