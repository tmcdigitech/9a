---
title: On-off lamp
---
This example shows the basics of a *state machine*, also known by the
more technical term *finite state automaton*. The idea is that the
program is in a particular *state*, and certain *events* will cause
a *transition* to another state.

In our case, our light is either *on* or *off* (the states), and we
will transition between them with a big enough vibration reading.
Here is a *state diagram* of this:

```mermaid
stateDiagram-v2
    direction LR
    [*] --> Off
    Off --> On : if vibration < 0.80 and ready
    On --> Off : if vibration < 0.80 and ready
```

Note the "and ready" condition. Given how fast the computer is,
when we tap the light, the vibration value will be less than 0.80 for
many cycles of the event loop, and without some care our light will
flash on and off rapidly, and be unpredictable.

Here is the complete code with several comments included.
We'll break it down below.

```python {linenos=table}
# Import libraries
import time
import neopixel
import adafruit_dotstar
import pulseio
from analogio import AnalogIn
import board

# Set up neopixel light strip
pixpin = board.D0
numpix = 3
pixels = neopixel.NeoPixel(pixpin, numpix, brightness = 0.5, auto_write=True, pixel_order=neopixel.GRBW)

# Built-in RGB light
dotstar = adafruit_dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1)

vibrationPin = AnalogIn(board.A0)

def get_voltage(pin):
    return (pin.value * 3.3) / 65536

# A list of all the states, each uniquely numbered
# (not important what the numbers are,
# as long as they're unique)
OFF = 0
ON = 1

# Variable to keep track of which state we're in.
state = OFF

# Flag to keep track of whether we're "ready" or not
ready = True

# Counter to keep track of when the ready flag should be set
readyCounter = 0

# Counter to print vibration value
printCounter = 0

# Event loop
while True:
    vibration = get_voltage(vibrationPin)
    # Do code matching the current state, whether OFF or ON
    if state == OFF:
        # ensure light off
        pixels.fill((0, 0, 0, 0))

        # check for events which cause transition from this state
        if vibration < 0.8 and ready:
            # do anything we need to exit this state

            # change state for next iteration of the loop
            state = ON

            # do anything we need to enter new state
            
            # Make us not ready, and set the ready counter
            ready = False
            readyCounter = 100
    
    elif state == ON:
        # ensure light on
        pixels[0] = (255, 0, 0, 0)
        pixels[1] = (0, 255, 0, 0)
        pixels[2] = (0, 0, 255, 0)
    
        # check for events
        if vibration < 0.8 and ready:
            state = OFF
            ready = False
            readyCounter = 100
    
    # Handle the counters
    if readyCounter > 0:
        # Decrement the counter
        readyCounter -= 1

        # If zero, we're "ready"
        if readyCounter == 0:
            ready = True
    
    if printCounter == 0:
        print(state, ready, vibration)
    
    printCounter = (printCounter + 1) % 10
```

