---
title: type
math: true
---
Computers store all information as sequences of numbers, but different kinds of data are encoded in different ways.
For example, whole numbers and decimal numbers are stored differently.

Some common data types you'll encounter are:

**integers** (`int`)
: Integers are whole numbers, and can be positive or negative.

**floating point numbers (`float` and `double`)**
: Floating point numbers (commonly called floats) are for storing decimal numbers.
The number is stored in scientific notation, with a mantissa and exponent.
$$\overbrace{3.18}^{\text{mantissa}}\times 10^{\overbrace{-7}^{\text{exponent}}}$$

There is a limited number of digits for the mantissa and the exponent. If you need more, a double precision floating point number (or `double` for short) has twice the
space, so can store a more precise mantissa, and a larger exponent.

**characters** (`char`)
: A character is a single letter, digit, punctuation mark,
or piece of whitespace (a space, newline, tab, etc.).

**strings** (`string`)
: Strings are so called because they are 'strings of characters'.
They are usually indicated with double quotes "like this".
In some languages, like Python, strings can be in single quotes
as well, 'like this'.