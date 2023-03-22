---
title: First app
weight: 10
---

Let's start with a very simple utility that converts temperatures between °F and °C.

To convert from °C to °F and back, here are the steps:
$$°C \to \times 1.8 \to +32 \to °F$$
$$°F \to -32 \to \div 1.8 \to °C$$

## Let's get making
In our new python document, let's import the `tkinter` library, and make our main window.

```python
import tkinter as tk

root = tk.Tk()

root.mainloop()
```

If you run the code now, you'll see a very featureless window. But it works!

## Thinking about what we need
We will need a field to enter the temperature into, and a field to display
the converted temperature. We'll also need variables to hold those two numbers.
We'll need a button to convert to C and a button to convert to F, and each will need
a function that is called when the button is pressed.

For consistency, we'll settle on these names:

name|function
--:|:--
tempIn|variable holding input temperature
inField|field for entering temperature
tempOut|variable holding output temperature
outField|field for displaying output
toCButton|button for converting to °C
toC|function that converts from °F to °C
toFButton|button for converting to °F
toF|function that converts from °C to °F

## Make the UI elements
Let's add the variables and the user interface elements. These have to go above the `root.mainloop()` line,
as that needs to be the very last line in the program.

```python
tempIn = tk.DoubleVar(value=-40)
inField = tk.Entry(textvariable=tempIn)
inField.pack()

tempOut = tk.StringVar(value="-40°C = -40°F")
outField = tk.Label(textvariable=tempOut)
outField.pack()

toCButton = tk.Button(text="to °C")
toCButton.pack()

toFButton = tk.Button(text="to °F")
toFButton.pack()
```

At this point we have all the front panel bits we need — we'll tidy up the layout a bit later!

## Wire up the panel
Now that the front is more or less in place, we can start writing the code which will connect
everything together.

Let's start with the function that converts to °F. Put this up the top of your file, just after
the import lines.

```python
def toF():
    global tempIn
    global tempOut
    
    c = tempIn.get()
    f = c*1.8 + 32
    tempOut.set(f"{c}°C = {f}°F")
```
Tkinter's variables (StringVar, DoubleVar, IntVar and so on) wrap Python's usual types up with
some helper stuff to make the GUI process work nicely.
As a result, we need to extract the actual temperature value from the variable using the `.get()` function.

We can then do the calculation to convert to °F. Finally, we can `.set()` the tempOut variable, which will
be reflected on the GUI.

That takes care of the function, but now we need to make sure it gets called when the button is pressed.

Find the line that defines `toFButton` and change it from this:
```python
toFButton = tk.Button(text="to °F")
```

to this:

```python
toFButton = tk.Button(text="to °F", command=toF)
```

We can now go ahead and repeat the process for converting to °C.

```python
def toC():
    global tempIn
    global tempOut
    
    f = tempIn.get()
    c = (f-32)/1.8
    tempOut.set(f"{f}°F = {c}°C")
```

And similarly, we need to update the `toCButton` definition to call the function when pressed.

```python
toCButton = tk.Button(text="to °C", command=toF)
```

## Code so far

At this point, our code looks like this:

```python
import tkinter as tk

def toF():
    global tempIn
    global tempOut
    
    c = tempIn.get()
    f = c*1.8 + 32
    tempOut.set(f"{c}°C = {f}°F")

def toC():
    global tempIn
    global tempOut
    
    f = tempIn.get()
    c = (f-32)/1.8
    tempOut.set(f"{f}°F = {c}°C")

root = tk.Tk()

tempIn = tk.DoubleVar(value=-40)
inField = tk.Entry(textvariable=tempIn)
inField.pack()

tempOut = tk.StringVar(value="-40°C = -40°F")
outField = tk.Label(textvariable=tempOut)
outField.pack()

toCButton = tk.Button(text="to °C", command=toC)
toCButton.pack()

toFButton = tk.Button(text="to °F", command=toF)
toFButton.pack()

root.mainloop()
```
