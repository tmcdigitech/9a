---
title: Frame
---
The Frame widget works like a container to arrange the position of other widgets. It uses rectangular areas in the screen to organize the layout and to provide padding of these widgets.

```python
f = tk.Frame( master, option, …)
```

[>> More Details](https://www.tutorialspoint.com/python/tk_frame.htm)

```python
import Tkinter as tk

root = tk.Tk()
frame = tk.Frame(root)
frame.pack()

bottomframe = tk.Frame(root)
bottomframe.pack( side = tk.BOTTOM )

redbutton = tk.Button(frame, text="Red", fg="red")
redbutton.pack( side = tk.LEFT)

greenbutton = tk.Button(frame, text="Brown", fg="brown")
greenbutton.pack( side = tk.LEFT )

bluebutton = tk.Button(frame, text="Blue", fg="blue")
bluebutton.pack( side = tk.LEFT )

blackbutton = tk.Button(bottomframe, text="Black", fg="black")
blackbutton.pack( side = tk.BOTTOM)

root.mainloop()
```
