---
title: list
---
A list is a data structure for storing a series of related pieces of information.

## Defining a list
You can define a list using square brackets, with the elements separated by commas, like this:

```python
squares = [0, 1, 4, 9, 16, 25, 36]
vowels = ["a", "e", "i", "o", "u"]
```

## Selecting elements
You can pick an element from the list like this: `squares[0]`. Note that counting begins at zero.
Think of the number as "how far from the beginning" the element in the list is.
So `vowels[0]` is the element at the start of the list, and `vowels[3]` is three elements further down the list. So the string `"u"` in that list would be `vowels[4]`.

## Adding elements
You can add elements to the end of a list with the `append()` function.

```python
squares.append(49)
print(squares[7])
# Output: 49
```

## Removing elements
You can remove elements from a list with `remove()` and `pop()`.

```python
friends = ["Nhi", "David", "Hari", "Zahra"]
friends.remove("David")
print(friends)
# Output: ["Nhi, "Hari", "Zahra"]
```
If there are multiple elements in the list with the same value, `remove()` will remove just the first one.

```python
friends = ["Nhi", "David", "Hari", "Zahra"]
exBestie = friends.pop(0)
print(friends)
# Output: ["David", "Hari", "Zahra"]
print(exBestie)
# Output: "Nhi"
```
