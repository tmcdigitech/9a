---
title: Photocell
weight: 70
---
```python
from analogio import AnalogIn, AnalogOut
import adafruit_dotstar as dotstar
import board
import time

# One pixel connected internally!
dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2, auto_write=True)

# Analog input on A1
photocell = AnalogIn(board.A1)

while True:
    print(photocell.value)
    time.sleep(0.1)
    if photocell.value > 300:
        dot[0] = (255, 255, 255)
    else:
        dot[0] = (100, 0, 0)
```
