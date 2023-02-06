---
title: Selection
weight: 2
---
*from [The Computing Zone](https://thecomputing.zone/Python/15-Challenges/)*

## File management
You will need to save each of the tasks in this set in its own file, with a simple naming system:
- **9. Advice please** should be in a file named `ex9.py`,
- **10. Darts** should be in a file named `ex10.py`

and so on.

You will be submitting these files to a system which will mark them automatically.
Since they'll be marked by a computer, and computers are terminally stupid, you
will need to make sure that your files are labelled correctly, or the computer
will assume you haven't done that particular exercise. You will also need to
make sure your output exactly matches the examples, down to capitalisation,
spelling, line breaks and spaces.

You need to make sure each of your exercises uses this code layout. Replace
the included example (which is exercise 2 from the sequence section) with your code.

```python
def ex(input,print):
    # your program goes below here
    # vvvvvvvvvvvvvvvvvvvvvvvvvvvv

    print("What is your first name?")
    fname = input("> ")
    print("What is your surname?")
    sname = input("> ")
    print(f"{sname} {fname}")

    # ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    # your program goes above here

if __name__ == "__main__":
    ex(input,print)
```

## 9. Advice please
Write a program that asks the user if they would like some advice. If they enter Y, provide them with an amusing message.

```md
Would you like some advice?
> Y
Always know where your towel is.
```
---
```md
Would you like some advice?
> N
```

## 10. Darts
During a game of darts, the highest score that can be achieved in a single turn is 180. The lowest is 0.
Write a program that will allow a dart player to enter their score. The program should congratulate the player if their score was over 100. If the player scores less than 10 they should be told that some practice is required.

```md
Please enter your score:
> 125
What a great score! Well done.
```
---
```md
Please enter your score:
> 7
That was rubbish. Get practising!
```

## 11. Charity Collection
Three friends have been collecting money for charity. A local company has offered to double the amount of money they collect if they raise over $1000. Write a program that allows the friends to enter their individual amounts. The program should then add the three amounts and store the total. If the total is greater or equal to $1000 the total should be doubled. Finally the total should be displayed.

```md
Enter the first amount raised.
> 398
Enter the second amount raised.
> 193
Enter the third amount raised.
> 478
A total of $1069 was raised.
This will be doubled to $2138.
```

## 12. Solid, Liquid, Gas
At normal atmospheric pressure, water is a solid at or below 0&deg;C, a gas above 100&deg;C, and a liquid in the middle. Write a program that will return *solid*, *liquid* or *gas* to the user depending on the temperature they enter.

```md
Enter the current temperature.
> 78
At 78°C, water will be a liquid.
```
