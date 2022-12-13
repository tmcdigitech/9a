---
title: color/colour
---
In almost all programming, American spellings are used. So as programmers we use **colors**, even though we would normally spell the word **colours**.

Colors are described by the amount of red, green, and blue light to emit, using numbers in the range `0` to `255`. In Python, we list these as a tuple `(red, green, blue)`, such as:

```python
(0, 150, 255)
```
The built-in RGB LED on your Gemma (a DotStar) has these three color components, so we set its color in this way.

The NeoPixel RGB LEDs you will solder onto your Gemma have four components: the usual red, green, and blue and also white.
So you if you wanted the above color on your Neopixel LED strip, you would use:

```python
(0, 150, 255, 0)
```

Unless you want to set a particular LED pixel to be white in color, it is recommended that you set the white value to zero (`0`),
as the white tends to wash out the colors otherwise.

You can use the [Google Color Picker](https://www.google.com/search?q=color+picker) to find different colors, and then copy the RGB value listed.
Don't forget to add a value for the white (probably zero) after the other three numbers, if you are setting NeoPixel colors.