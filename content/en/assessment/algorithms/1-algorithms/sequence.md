---
title: Sequence
weight: 1
---
*from [The Computing Zone](https://thecomputing.zone/Python/15-Challenges/)*

## File management
You will need to save each of the tasks in this set in its own file, with a simple naming system:
- **1. Three in, three out** should be in a file named `ex1.py`,
- **2. Name swapper** should be in a file named `ex2.py`

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

## 1. Three in, three out
*Introduces:* [`print()`](https://www.w3schools.com/python/ref_func_print.asp), [`input()`](https://www.w3schools.com/python/ref_func_input.asp), [variables](https://www.w3schools.com/python/python_variables.asp)

Write a program that will allow a user to enter their name (string), their age (integer) and their favourite TV program (string). The program will then display the information entered and some additional text on separate lines. An example of the input and output from the program is shown below.

```md
What is your name?
> Lister
What is your age?
> 39
What is your favourite TV program?
> Red Dwarf
Lister
is
39
years old and likes
Red Dwarf
```

## 2. Name swapper
*Introduces:* [string concatenation](https://www.w3schools.com/python/python_strings_concatenate.asp)

Write a program that will ask the user to type in their first name and surname. The program will then display the two names in reverse order.

```md
What is your first name?
> David
What is your surname?
> Tennant
Tennant David
```

## 3. Three in, three out (formatted)
*Introduces:* [f-strings](https://www.freecodecamp.org/news/python-f-strings-tutorial-how-to-use-f-strings-for-string-formatting/)

Now edit program 1 so that the information entered is displayed differently as shown in the output box below. Note - your output will now have to display variables and text together.

```md
What is your name?
> Lister
What is your age?
> 39
What is your favourite TV program?
> Red Dwarf
Lister 39
Likes watching Red Dwarf
```

## 4. Area of a rectangle
*Introduces:* [data types](https://www.w3schools.com/python/python_datatypes.asp),
[casting](https://www.w3schools.com/python/python_casting.asp), [maths operators](https://www.w3schools.com/python/python_operators.asp)

Ask the user to enter the length and width of a rectangle. Your program should calculate the area of the rectangle (length*width) and display the result with a suitable message.

```md
Please enter the following values in cm.
Please enter the length of the rectangle.
> 12
Please enter the width of the rectangle.
> 6
The area of the rectangle is:
72 square centimetres
```

## 5. Area of a circle
Ask your user to enter the radius of a circle. Your program should use what they have entered to
calculate the area of the circle \\(A = \pi r^2\\) and display the result. 
```md
Please enter the following values in cm.
Please enter the radius of the circle.
> 16
The area of the circle is:
803.84 square centimetres
```

## 6. Number cruncher
Write a program that inputs two individual integers between 0 and 9. The program should then
combine the inputs to form a single number in a third variable. The program should show the equation of multiplying the three numbers together and the result, as shown in the example.

```md
Enter the first number (0-9).
> 2
Enter the second number (0-9).
> 3
2 x 3 x 23 = 138
```

## 7. Address formatter
A program is required to format and store a users address in a single string. The user should be asked these questions:

What is your house number?
What is the name of your street?
What suburb/town do you live in?
What is your postcode?

The program will then combine the user's answers in a single string, formatted as shown in the example. The program will display the string on the screen.

```md
What is your house number?
> 13
What is the name of your street?
> Aberlove Drive
What suburb/town do you live in?
> Buckhaven
What is your postcode?
> 4039
13 Aberlove Drive
BUCKHAVEN 4039

## 8. Super smart name swapper (extension)
Ask the user to enter their full name on one line, and display their name in reverse order.

```md
What is your full name?
> David Tennant
Tennant David
```
