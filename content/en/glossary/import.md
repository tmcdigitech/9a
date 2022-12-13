---
title: import
---

Importing is the process of adding functions from additional libraries to support your program.

Imagine we wish to use the `randint()` function
to choose a random number between 1 and 6, as
though we were throwing a single six-sided die.

The `randint()` function is included in the
`random` library, but there are three ways we
can import it, and each has its attractions.

## import

```python {linenos=table}
import random

num = random.randint(1,6)
print(num)
```

## import as

```python {linenos=table}
import random as ran

num = ran.randint(1,6)
print(num)
```

## import from

```python {linenos=table}
from random import randint

num = randint(1,6)
print(num)
```
