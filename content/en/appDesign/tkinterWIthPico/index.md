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
import microcontroller

fan = digitalio.DigitalInOut(board.GP16)
fan.direction = digitalio.Direction.OUTPUT
fan.value = False

buzzer = pwmio.PWMOut(board.GP15, variable_frequency=True)
OFF = 0
ON = 2**15
buzzer.duty_cycle = OFF

while True:
    cmd = input('')
    if(cmd=='f1'):
        fan.value = True
    elif(cmd=='f0'):
        fan.value = False
    elif(cmd=='b2'):
        buzzer.frequency = 880
        buzzer.duty_cycle = ON
    elif(cmd=='b1'):
        buzzer.frequency = 440
        buzzer.duty_cycle = ON
    elif(cmd=='b0'):
        buzzer.duty_cycle = OFF
    print(microcontroller.cpu.temperature)
```

Controller App for tkinter on computer.

```python
import tkinter as tk
import serial
import serial.tools.list_ports

ser = serial.Serial()

# Set up frame on left for choosing which serial connection to use
root = tk.Tk()
portFrame = tk.Frame(root)
portFrame.pack(side='left')

# Set up frame on left for controls
cmdFrame = tk.Frame(root)
cmdFrame.pack(side='right')

def initComPort(index):
    port = str(ports[index])
    comPortVar = str(port.split(' ')[0])
    print(comPortVar)
    ser.port = comPortVar
    ser.baudrate = 9600
    ser.timeout = 0
    ser.open()

# Populate portFrame with available ports
ports = serial.tools.list_ports.comports()
for port in ports:
    btn = tk.Button(portFrame, text=port, command = lambda: initComPort(ports.index(port)))
    btn.grid(column=0)

# Populate cmdFrame with controls
btn = tk.Button(cmdFrame,text="Fan Off",command=lambda: ser.write(b'f0\r\n'))
btn.pack()
btn = tk.Button(cmdFrame,text="Fan On",command=lambda: ser.write(b'f1\r\n'))
btn.pack()
btn = tk.Button(cmdFrame,text="Buzzer Off",command=lambda: ser.write(b'b0\r\n'))
btn.pack()
btn = tk.Button(cmdFrame,text="Buzzer Low",command=lambda: ser.write(b'b1\r\n'))
btn.pack()
btn = tk.Button(cmdFrame,text="Buzzer High",command=lambda: ser.write(b'b2\r\n'))
btn.pack()

while True:
    # update_idletasks and update do job of mainloop,
    # but allows adding extra commands to the main loop
    root.update_idletasks()
    root.update()
    # check serial port traffic
    if ser.is_open:
        s = ser.read(100)
        if len(s) > 0:
            print(bytes.decode(s))
```
