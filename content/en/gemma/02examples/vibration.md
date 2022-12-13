---
title: Vibration Sensor
weight: 80
---
```python
import time
import neopixel
import adafruit_dotstar
import pulseio
from analogio import AnalogIn
import board

def get_voltage(pin):
    return (pin.value * 3.3) / 65536

pixels = neopixel.NeoPixel(board.D1, 3, brightness=1,
    auto_write=True, pixel_order=neopixel.GRBW)

vibrationPin = AnalogIn(board.A0)

while True:
    vibration = get_voltage(vibrationPin)
    print(vibration)
    time.sleep(.1)
    

    if vibration < 0.81:  # the sensor has been tripped, adjust this value
        pixels[0] = (255, 0, 0, 0)
        time.sleep(0.5)
    else:
        pixels[0] = (0, 255, 0, 0)
    pixels.fill(OFF)
```