---
title: Tk Tac Toe
weight: 20
---

In this walkthrough we will make a noughts & crosses (tic-tac-toe)
game using a 3x3 grid of buttons.

As we go through this, you might find yourself thinking "there must be a better way to do this". You are probably right; there are some things we will do which could *definitely* be improved on, and we'll come back to them later. For now, we'll keep it simple, if repetitive and clunky.

Let's start with the basics:

```python{linenos=table}
import tkinter as tk

root = tk.Tk()

root.mainloop()
```

## Grid setup
We set up the grid structure, which is three columns with equal weight (width):

```python{linenos=table,hl_lines=["4-6"]}
import tkinter as tk

root = tk.Tk()
root.columnconfigure(0,weight=1)
root.columnconfigure(1,weight=1)
root.columnconfigure(2,weight=1)

root.mainloop()
```

## Button layout
We'll number each of the nine buttons, which will be arranged like this:
```
    Column
     0 1 2
   +------
R 0| 1 2 3
o 1| 4 5 6
w 2| 7 8 9
```

Let's make the buttons. Each button's construction looks like this:
```python
b1 = tk.Button()
b1.config(command=lambda: move(b1))
b1.grid(column=0, row=0)
```
for each of `b1` to `b9`. We need to set the column and row (so `b6` has `column=2, row=1` for example).

The middle line sets the command that should be triggered when the button is pressed. Rather than writing nine separate identical functions (one for each button), we can create one function that they all trigger and just pass in which button was pressed as a parameter. The `command=` part takes the name of a function, so if we want to pass in a parameter as well, we need to use a **lambda function** (a function body without a name). We could also have used a partial function, which we won't describe further here. Because we need to pass our button's variable in as a parameter to the function, we need to have declared it first, which is why we define the command in a separate call to config, and not in the line that creates the button, as we have before.

So go ahead and make nine copies of that, making sure that you replace `b1` with the appropriate button number in the four places it appears, and that you get the columns and rows correct.

Run your function now, and check that you have a grid of nine buttons.

## Starting to move

Let's start making our `move` function. When you move, we want to disable the button, so that nobody can make the same move again.quickly knock up an empty function so we can test things out:

```python{linenos=table,hl_lines=["3-4"]}
import tkinter as tk

def move(b):
    b['state'] = 'disabled'

root = tk.Tk()
root.columnconfigure(0,weight=1)
root.columnconfigure(1,weight=1)
root.columnconfigure(2,weight=1)

b1 = tk.Button()
b1.config(command=lambda: move(b1))
b1.grid(column=0,row=0)

# more buttons here...

b9 = tk.Button()
b9.config(command=lambda: move(b9))
b9.grid(column=2,row=2)

root.mainloop()
```

Let's focus some more on the move command. 
When a button is pressed, we want to mark the button
with a player's token (either ⭕️ or ❌). To do that
we need to keep track of whose move it is and change it
each time someone moves. So we will make a list of the
player tokens, and a variable `nextMove`
to keep track of which one is moving next.

```python{linenos=table,hl_lines=["1-2",4,"6-7"],linenostart=3}
nextMove = 0
players = ['⭕️','❌']
def move(b):
    global nextMove
    b['state']='disabled'
    b['text'] = players[nextMove]
    nextMove = (nextMove+1)%2
```
