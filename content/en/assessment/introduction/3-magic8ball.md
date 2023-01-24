---
title: "3: Magic 8-ball"
weight: 30
---
## Purpose
To develop your Computational Thinking skills by implementing a digital solution using the Micro:bit and Python code with branching and iteration.

## Learning behaviours
This task provides the following opportunities to develop and demonstrate the Learner Behaviours:

LB | Description
---|---
Driven | Engages in Python coding challenges with persistence; learns from their mistakes; willingly completes the extension activities.
Curious | Explores and tests ideas by asking questions, researching and through trial and error when learning new skills or developing solutions.
Collaborators | Works in teams to solve problems and create new information. Willingly shares new skills and knowledge and assists others and seeks assistance from peers.
Connected | Connects programming constructs and data structures to real life applications and is able to explore and discuss issues and ethical implications of their solution.
Flexible Thinkers | Applies new knowledge and skills to solve problems and is able to adapt and recognize patterns in other solutions.
Disciplined | Motivated learner who demonstrates initiative by following a project management process to complete a project.

## To be successful
Accurately and independently complete all 5 steps include your code and comments in your OneNote section called *Task 3 Coding a Magic Eight Ball*.
- Include comments with your all Python code
- Use the correct programming structure (selection and iteration)
- Complete core and attempt all parts of Step 5.

## Task description
Using the Microbit, make a Magic 8-ball by following steps 1-5 below.

Ensure your app is working by carrying out testing and modifying your code. Include comments in your code and [hand it in](http://10.124.229.70:8080/) when finished.

The **Magic 8-ball** is a fortune telling toy created by Mattel in the 1950s. The concept is simple. Ask the 8-ball a yes or no question and the 8-ball will reply with answers such as “Yes”, “No”, “Without a doubt” etc. (seemingly able to predict the future). The Magic 8 Ball is made up of 20 responses &mdash; 10 positive, 5 negative and 5 neutral. The 20 answers are: 

- Positive answers
    - It is certain
    - It is decidedly so
    - Without a doubt
    - Yes definitely
    - You may rely on it
    - As I see it, yes
    - Most likely
    - Outlook good
    - Yes
    - Signs point to yes 

- Negative answers
    - Don't count on it
    - My reply is no
    - My sources say no
    - Outlook not so good
    - Very doubtful 

- Neutral answers
    - Reply hazy, try again
    - Ask again later
    - Better not tell you now
    - Cannot predict now
    - Concentrate and ask again 

According to [Wikipedia](http://en.wikipedia.org/wiki/Magic_8-Ball):
> Using the coupon collector's problem in probability theory, it can be shown that it takes, on average, 72 outcomes of the Magic 8 Ball for all 20 of its answers to appear at least once.

### 1: Write an ‘8’ to the screen 
In the Microbit app, write the following code: 
```python
from microbit import *  
import random  

while True:  
    sleep(1000) 
    display.show("8") 
```

Upload the code to the Microbit and run it. What happens when you shake the Microbit? 

### 2: Shake it!
Add the following code to what you have already written, inside the `while True:`.
```python
    if accelerometer.was_gesture("shake"):  
        display.clear() 
        sleep(1000) 
        display.show("!") 
```

Upload the code to the Microbit and run it. What happens when you shake the Microbit?

### 3: Write some responses 
We need to list our responses, and in Python we do that in a list variable. The list is Python's equivalent to other languages' *array*. Write this code before the `while True:`.
```python
answers = ["Yes",  "No", "Maybe", "Yes, definitely"] 
```

### 4: Pick a random response 
To make the Magic 8-Ball pick a random response, we can get it to pick a random answer using `random.choice()`.

```python
        sleep(1000)  
        display.scroll(random.choice(answers)) 
```
 
Include this code so that when you shake the Microbit, the microbit will wait a second and then show a random answer to the question you put to it. 

### 5: Modify and extend your code
1. Modify your list to contain all 20 official responses.

2. Add comments to your code to explain how it works.

3. Modify your code so that it plays a sound when it gives a response.

4. Modify your code so that it counts how many responses and shows an image after 3 responses.
