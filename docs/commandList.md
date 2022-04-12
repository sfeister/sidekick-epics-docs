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
| caget LEDS:info           | Gets information about the LED device                              |
| caget LEDS:CHN:brig       | Returns and prints the value of brightness of LED N                |
| caput LEDS:CHN:brig X     | Allows you to set brightness of X (0-255) of LED N                 |
| caget LEDS:CHN:dur        | Returns and prints the value of duration (microseconds) of LED N   |
| caput LEDS:CHN:dur X      | Allows you to set duration of X (nanoseconds) of LED N             |
| caput LEDS:debug "string" | Debugs the command placed within the string for the LEDS functions |
| caget LEDS:debug          | Returns the value that was used within the debug for analysis      |

## PHOTODETECTOR
| command                    | description                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------- |
| caget PHOTO:info           | Gets information about the Photodetector device                                    |
| caget PHOTO:data           | Gets the data from the Photodetector device in terms of a number value             |
| caget PHOTO:dur            | Gets the current duration of the Photodetector detecting in microseconds           |
| caput PHOTO:dur X          | Allows you to set the duration of the Photodetector detection time in microseconds |
| caget PHOTO:trigcnt        | Gets the trigger count number                                                      |
| caput PHOTO:trigcnt X      | Manipulates the trigger count value to be X                                        |
| caput PHOTO:debug "string" | Debugs the command placed within the string for the Photodetectors functions       |
| caget PHOTO:debug          | Returns the values that were used in the debug analysis                            |

## PULSE GENERATOR
