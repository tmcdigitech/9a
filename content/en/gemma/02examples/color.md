---
title: A flash of colo(u)r
weight: 30
---

The Gemma has a built-in (DotStar) RGB LED. DotStar LEDs can be chained together, and even
though there is only one on the Gemma, we still refer to it as though it were on a chain,
just a chain of one. [Colors]({{< relref "/glossary/color" >}}) are set with an RGB tuple.
The brightness can be configured between 0 and 1.
Why would you want to lower the brightness? Here are three reasons:
- maximum brightness is almost painfully bright, which is bad if you're up close.
- at night, a little light goes a long way, and you may not need a simple notification to double as a torch.
- the brighter it is, the more power it draws, which is a problem for battery powered projects where you want to maximise battery life.

```python
import adafruit_dotstar as dotstar
import board
import time

# Configure the DotStar LED, and call it "dot"
dot = dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1, brightness=0.2)

while True:
  dot[0] = (255, 0, 0)
  time.sleep(0.5)
  dot[0] = (0, 255, 0)
  time.sleep(0.5)
  dot[0] = (0, 0, 255)
  time.sleep(0.5)
```
