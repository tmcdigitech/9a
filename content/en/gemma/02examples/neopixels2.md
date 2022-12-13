---
title: Neopixels (Part 2)
weight: 61
---
Let's improve our code so now the lights respond to touch input.

```python {linenos=table, hl_lines="4 6 13 17-18"}
import board
import time
import neopixel
from touchio import TouchIn

touch = TouchIn(board.A2)

# LED strip
pixels = neopixel.NeoPixel(board.D1, 3, brightness=1,
    auto_write=True, pixel_order=neopixel.GRBW)

while True:
    if touch.value:
        pixels[0] = (255, 0, 0, 0)
        pixels[1] = (0, 255, 255, 0)
        pixels[2] = (0, 0, 0, 255)
    else:
        pixels.fill((0, 0, 0, 0))
```
