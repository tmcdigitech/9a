---
title: Tkinter controlling RPi Pico
---

Example code for the Pico (using CircuitPython 8.0.5).
Fan connected to GP16 and PWM controlled buzzer to GP15.

```python
import time
import board
import digitalio
import pwmio


fan = digitalio.DigitalInOut(board.GP16)
fan.direction = digitalio.Direction.OUTPUT
fan.value = False

buzzer = pwmio.PWMOut(board.GP15, frequency=440)
OFF = 0
ON = 2**15
buzzer.duty_cycle = OFF

while True:
    cmd = input('')
    if(cmd=='f1'):
        fan.value = True
    elif(cmd=='f0'):
        fan.value = False
    elif(cmd=='b1'):
        buzzer.duty_cycle = ON
    elif(cmd=='b0'):
        buzzer.duty_cycle = OFF
```

Example code that reads from serial port (not configured to work with above example...).
```python
from serial import *
from Tkinter import *

serialPort = "/dev/ttyACM0"
baudRate = 9600
ser = Serial(serialPort , baudRate, timeout=0, writeTimeout=0) #ensure non-blocking

#make a TkInter Window
root = Tk()
root.wm_title("Reading Serial")

# make a scrollbar
scrollbar = Scrollbar(root)
scrollbar.pack(side=RIGHT, fill=Y)

# make a text box to put the serial output
log = Text ( root, width=30, height=30, takefocus=0)
log.pack()

# attach text box to scrollbar
log.config(yscrollcommand=scrollbar.set)
scrollbar.config(command=log.yview)

#make our own buffer
#useful for parsing commands
#Serial.readline seems unreliable at times too
serBuffer = ""

def readSerial():
    while True:
        c = ser.read() # attempt to read a character from Serial
        
        #was anything read?
        if len(c) == 0:
            break
        
        # get the buffer from outside of this function
        global serBuffer
        
        # check if character is a delimeter
        if c == '\r':
            c = '' # don't want returns. chuck it
            
        if c == '\n':
            serBuffer += "\n" # add the newline to the buffer
            
            #add the line to the TOP of the log
            log.insert('0.0', serBuffer)
            serBuffer = "" # empty the buffer
        else:
            serBuffer += c # add to the buffer
    
    root.after(10, readSerial) # check serial again soon


# after initializing serial, an arduino may need a bit of time to reset
root.after(100, readSerial)

root.mainloop()
```
