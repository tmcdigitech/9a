---
title: Counters
weight: 2
---

Embedded code like on a Gemma or Micro:bit
often involves going around a main loop
forever. We can't use sleep/wait/delay functions because they'll stop everything else
from happening. We can use counters to make multiple actions seem to happen at once.

Here is an example. In this case, you can see in the flowchart below that we will use
a counter called `n`, and initialise it to 0. Each time around the loop we will check
if `n` has reached 1000 yet. If it has we will reset it to 0. Otherwise, it will
increment `n` (add 1 to it).

```mermaid
flowchart LR
a([Start])
b[Set n = 0]
c[Switch light off]
d{n == 1000?}
e[Set n = 0]
f[Flick switch]
g[Increment n]
a-->b-->c-->d
d--True-->e-->f-->d
d--False-->g-->d
```

Here is the equivalent Python code to run on your Gemma. Note that this loop goes around
1000 times before it flicks the switch each time. Observe how fast the light is flashing;
remember that computers are really, really, really, really fast!

```python {linenos=table}
import board
import digitalio
import time

led = digitalio.DigitalInOut(board.LED)
led.direction = digitalio.Direction.OUTPUT

n = 0
led.value = False
while True:
    if n == 1000:
        n = 0
        led.value = not led.value
    n += 1
```

## A wild example
Here is a crazier example with four counters, one each for the built-in led,
and each of the red, green and blue channels of the dotstar.

Each counter is reset and its respective switch "flicked" after a given
amount of time. Try changing the counter values to make different patterns.

```python {linenos=table}
import board
import digitalio
import adafruit_dotstar as dotstar

led = digitalio.DigitalInOut(board.LED)
led.direction = digitalio.Direction.OUTPUT

dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2)

ledCount = 0
led.value = False

redCount = 0
redValue = 0

greenCount = 0
greenValue = 0

blueCount = 0
blueValue = 0

while True:
    if ledCount == 500:
        ledCount = 0
        led.value = not led.value

    if redCount == 700:
        redCount = 0
        redValue = 255 - redValue

    if greenCount == 900:
        greenCount = 0
        greenValue = 255 - greenValue

    if blueCount == 1100:
        blueCount = 0
        blueValue = 255 - blueValue
    ledCount += 1
    redCount += 1
    greenCount += 1
    blueCount += 1
    dot[0] = (redValue, greenValue, blueValue)
```
