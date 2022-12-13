---
title: Color cycling
weight: 40
---

The demo program that comes with the Gemma includes a nice function which generates a swirl through the rainbow.
It takes a number from `0`-`255` and returns a color as a list (which you can use directly instead of specific color tuple).

```python
# Helper to give us a nice color swirl
def wheel(pos):
    # Input a value 0 to 255 to get a color value.
    # The colours are a transition r - g - b - back to r.
    if pos < 0:
        return [0, 0, 0]
    if pos > 255:
        return [0, 0, 0]
    if pos < 85:
        return [int(255 - pos*3), int(pos*3), 0]
    elif pos < 170:
        pos -= 85
        return [0, int(255 - (pos*3)), int(pos * 3)]
    else:
        pos -= 170
        return [int(pos*3), 0, int(255 - pos*3)]
```

Here is a complete example of it in action, using the built-in DotStar.

```python
import adafruit_dotstar as dotstar
import board
import time

# One pixel connected internally!
dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2)

# Helper to give us a nice color swirl
def wheel(pos):
    # Input a value 0 to 255 to get a color value.
    # The colours are a transition r - g - b - back to r.
    if pos < 0:
        return [0, 0, 0]
    if pos > 255:
        return [0, 0, 0]
    if pos < 85:
        return [int(255 - pos*3), int(pos*3), 0]
    elif pos < 170:
        pos -= 85
        return [0, int(255 - (pos*3)), int(pos * 3)]
    else:
        pos -= 170
        return [int(pos*3), 0, int(255 - pos*3)]

color = 0
t = 0
while True:
    dot[0] = wheel(color)
    t +=1 
    if t == 10:
        t = 0
        color += 1

    
    if color == 256:
        color = 0
```