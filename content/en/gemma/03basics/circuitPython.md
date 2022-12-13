---
title: CircuitPython
weight: 1
---

Let's get something happening on your Gemma.

All of these examples are complete programs, so make sure you copy them into Mu (or whatever editor you're using)
and run them as you go through this page.

## Flash the built-in LED
The first thing you try to get working on any embedded system is flashing a light. It's amazing how much information
you can convey with just a light if you get a little creative!

```python {linenos=table}
import board
import digitalio
import time

led = digitalio.DigitalInOut(board.LED)
led.direction = digitalio.Direction.OUTPUT

while True:
    led.value = True
    time.sleep(0.5)
    led.value = False
    time.sleep(0.5)

```

Lines 1-3 import various libraries that we will use. All of your Gemma programs will start with one or more of these import lines.

Line 5 gives us a reference to the pin that the built-in LED (the red one) is connected to. We store that reference in a [variable]({{< ref "/glossary/variable" >}}) called `led`.
Line 6 tells the Gemma that we want to use the pin we've called `led` as an output (to drive the red LED).

Lines 8-12 are an infinite loop. We turn the LED on, wait for half a second, turn it off, and wait another half second.
Then we do it all again, and again, and so on.

{{< alert "Check your units" >}}
Note that `time.sleep()` takes values in seconds, rather than milliseconds.
{{< /alert >}}

If you've written this in Mu, it should look like this:

![first program in Mu](https://cdn-learn.adafruit.com/assets/assets/000/105/704/medium800/circuitpython_WtCP_Mu_blink_example.png?1634763853)

## Flash the built-in RGB LED
Now we've got something happening, let's explore the built-in RGB LED. This model of LED is a Dotstar.
The LEDs on the strip we'll be using are a model called Neopixel.

```python {linenos=table}
import board
import adafruit_dotstar as dotstar
import time

dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2)

while True:
    dot[0] = (255, 255, 0)
    time.sleep(0.5)
    dot[0] = (0, 0, 255)
    time.sleep(0.5)
```

Notice that we on line 5 we call the dotstar `dot`, but to use it we say `dot[0]`.
Dotstars and Neopixels are designed to be chained together on a strip with common wires,
so `dot` actually refers to a [list]() of LEDs, not just one.
Counting in computers usually begins at zero, so the LED at the end closest to the signal source is
numbered `dot[0]` and the others numbered `dot[1]`, `dot[2]` and so on.
Since there is only one built-in dotstar, we only use `dot[0]`.

## Respond to the capacitive input

You can use pin A2 as a capacitive input,
meaning it will detect your finger touching it.

```python {linenos=table}
import board
import digitalio
from touchio import TouchIn

touch2 = TouchIn(board.A2)

led = digitalio.DigitalInOut(board.D13)
led.direction = digitalio.Direction.OUTPUT

while True:
    led.value = touch2.value
```

## Capacitive input and the RGB LED

If we want to control the RGB led with with
the touch input, we need to do a bit more work,
and use an `if` statement.

```python {linenos=table}
import board
import adafruit_dotstar as dotstar
from touchio import TouchIn

touch2 = TouchIn(board.A2)

dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2)

while True:
    if touch2.value:
        dot[0] = (255, 255, 0)
    else:
        dot[0] = (0, 0, 255)
```
