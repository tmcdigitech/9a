---
title: Respond to input
weight: 20
---

In this example, the light will turn on while you touch pin A2.

```python
from digitalio import DigitalInOut, Direction
from touchio import TouchIn
import board
import time

# Built in red LED
led = DigitalInOut(board.D13)
led.direction = Direction.OUTPUT

# Capacitive touch on A2
touch2 = TouchIn(board.A2)

while True:
    led.value = touch2.value
```