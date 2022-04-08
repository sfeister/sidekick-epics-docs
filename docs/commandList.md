---
layout: default
title: Command Lists
authors:
    - Emiko Ito
---


# Command Lists
## LEDS
| command                   | description                                                        |
| ------------------------- | ------------------------------------------------------------------ |
| caget LEDS:info           | Gets information about the LED device.                             |
| caget LEDS:CHN:brig       | Returns and prints the value of brightness of LED N                |
| caput LEDS:CHN:brig X     | Allows you to set brightness of X (0-255) of LED N                 |
| caget LEDS:CHN:dur        | Returns and prints the value of duration (microseconds) of LED N   |
| caput LEDS:CHN:dur X      | Allows you to set duration of X (nanoseconds) of LED N             |
| caput LEDS:debug "string" | Debugs the command placed within the string for the LEDS functions |
| caget LEDS:debug          | Returns the value that was used within the debug for analysis      |
