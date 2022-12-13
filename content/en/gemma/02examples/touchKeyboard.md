---
title: Touch keyboard
weight: 50
---

```python
# Welcome to CircuitPython 5 :)

import usb_hid
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS
from adafruit_hid.keycode import Keycode
from touchio import TouchIn
import board
import time

# Capacitive touch on A2
touch0 = TouchIn(board.A0)
touch1 = TouchIn(board.A1)
touch2 = TouchIn(board.A2)

# The keyboard object! Used if we do HID output, see below
time.sleep(1)  # Sleep for a bit to avoid a race condition on some systems
keyboard = Keyboard(usb_hid.devices)
layout = KeyboardLayoutUS(keyboard)  # We're in the US :)

######################### MAIN LOOP ##############################

while True:
    if touch0.value:
        keyboard.send(Keycode.CTRL, Keycode.N)
        keyboard.send(Keycode.CTRL, Keycode.A)
        layout.write("This is my computer now...")
        time.sleep(1)
        keyboard.send(Keycode.WINDOWS, Keycode.L)
    
    if touch1.value:
        keyboard.send(Keycode.F11)

    if touch2.value:
        keyboard.send(Keycode.NINE)
```
