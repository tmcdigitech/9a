---
title: Neopixels
weight: 60
---

```python {linenos=table}
import board
import time
import neopixel

# LED strip
pixels = neopixel.NeoPixel(board.D1, 3, brightness=1,
    auto_write=True, pixel_order=neopixel.GRBW)

while True:
    pixels[0] = (255, 0, 0, 0)
    pixels[1] = (0, 255, 255, 0)
    pixels[2] = (0, 0, 0, 255)
```
