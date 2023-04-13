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

At this point we can make moves. We now need to tackle the various ways in which the game might end. Let's first handle the case of a draw.

## It's a draw

If each square has been used and nobody has yet won, then the game is a draw. There are several ways we could keep track do this, but the easiest is probably to just count the number of moves that have been made, and to declare a draw when that number gets to 9. Alternatively, count how many moves are left and declare a draw when that number reaches 0.

We're not going to do anything fancy when it is a draw. We're just going to reset the board immediately. To do that, we'll need a reset function.

```python{linenos=table,hl_lines=[3,"9-11","13-16"],linenostart=3}
nextMove = 0
players = ['⭕️','❌']
movesLeft = 9
def move(b):
    global nextMove, movesLeft
    b['state'] = 'disabled'
    b['text'] = players[nextMove]
    nextMove = (nextMove+1)%2
    movesLeft -= 1
    if movesLeft == 0:
        reset()

def reset():
    for b in [b1, b2, b3, b4, b5, b6, b7, b8, b9]:
        b['state'] = 'normal'
        b['text'] = '—'
```

Run the program, and check that it resets at the end. But can you find the bug lurking in our reset code?

If you play a second game, the program will not correctly reset at the end of the second game. Why is that?

After line 11, where we decrement `movesLeft`, add a line saying `print(movesLeft)`. This is called a test print. We're not planning to have this line in the finished program, but it is really helpful to see what the program is up to while you're developing and debugging it.

If you watch the moves left now, you'll notice that while the board resets at the end of the first game, the counter continues to count down into negatives. As a result, the counter doesn't reach zero to signal the end of the second game. We will need to reset the counter in our `reset` function.

```python{linenos=table,hl_lines=5,linenostart=15}
def reset():
    for b in [b1, b2, b3, b4, b5, b6, b7, b8, b9]:
        b['state'] = 'normal'
        b['text'] = '—'
        movesLeft = 9
```

Check that you can play multiple games and the counter is resetting correctly. You will notice it is still broken!

You can now safely remove that test print.

## For the win

Again, there are several ways we could try and tackle monitoring a win. Here's what we're going to do this time.
To win you must get 3-in-a-row, which can be done in one of eight ways:
- top row
- middle row
- bottom row
- left column
- centre column
- right column
- forward diagonal
- backward diagonal

If we check after each move if all three of the squares for each of those eight combinations is the same, we'll know that there is a win. Let's write a function to do that:

```python
def winCheck():
    if b1['text'] in players and b1['text'] == b2['text'] and b2['text'] == b3['text']:
        tk.messagebox.showinfo(title='Game over!', message=f"{b1['text']} wins")
        return b1['text']
    if b4['text'] in players and b4['text'] == b5['text'] and b5['text'] == b6['text']:
        tk.messagebox.showinfo(title='Game over!', message=f"{b4['text']} wins")
        return b4['text']
    # and so on
```

Note that we can't chain equals signs together like this:
```python
if b1['text'] == b1['text'] == b1['text']:
```
That has a meaning (so it will run without an error) but it won't do what you want.

The `b1['text'] in players` condition checks to see if the text is one of the player symbols and not blank or the dash we're using when we run `reset()`. Otherwise a blank row or column would trigger the win condition.

Lastly, the `showinfo` function displays a popup box with the set title and message. We will need to import the function in order to do this. Add this line just under the `import tkinter as tk` line:
```python
from tkinter.messagebox import showinfo
```

Finish off this (inelegant) function to handle all eight cases.

So the `winCheck` function will check if there is a winner, pop up a message with the winner, and return the winner to whatever called it, or False if there isn't a winner yet. So we can now run this check each time someone moves, just before we check for a draw (because we want a win on the last move to count as a win, not a draw).

```python{linenos=table,hl_lines="7-8",linenostart=7}
def move(b):
    global nextMove, movesLeft
    b['state']='disabled'
    b['text'] = players[nextMove]
    nextMove = (nextMove+1)%2
    movesLeft -= 1
    if winCheck() is not False:
        reset()
    if movesLeft == 0:
        reset()
```
