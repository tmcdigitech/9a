---
title: Flash a light
weight: 10
---

The first project you do with any new piece of hardware: flash a light.

```python {linenos=table}
from digitalio import DigitalInOut, Direction
import board
import time

# Built in red LED
led = DigitalInOut(board.D13)
led.direction = Direction.OUTPUT

while True:
    led.value = True
    time.sleep(0.5)
    led.value = False
    time.sleep(0.5)
```