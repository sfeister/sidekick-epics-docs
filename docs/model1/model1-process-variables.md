---
layout: default
title: Process Variables
authors:
    - Emiko Ito
    - Scott Feister
---


# Process Variables for Sidekick Model 1

## LEDS
| command                   | description                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------ |
| caget LEDS:info           | Gets information about the LED device                                                |
| caget LEDS:CHN:brig       | Returns and prints the value of brightness of LED N                                  |
| caput LEDS:CHN:brig X     | Allows you to set brightness of X (0-255) of LED N                                   |
| caget LEDS:CHN:dur        | Returns and prints the value of duration (microseconds) of LED N                     |
| caput LEDS:CHN:dur X      | Allows you to set duration of X (nanoseconds) of LED N                               |
| caput LEDS:debug "string" | Debugs the command placed within the string for the LEDS functions                   |
| caget LEDS:debug          | Returns the value that was used within the debug for analysis                        |

## PHOTODETECTOR
| command                    | description                                                                         |
| -------------------------- | ----------------------------------------------------------------------------------- |
| caget PHOTO:info           | Gets information about the Photodetector device                                     |
| caget PHOTO:data           | Gets the data from the Photodetector device in terms of a number value              |
| caget PHOTO:dur            | Gets the current duration of the Photodetector detecting in microseconds            |
| caput PHOTO:dur X          | Allows you to set the duration of the Photodetector detection time in microseconds  |
| caget PHOTO:trigcnt        | Gets the trigger count number                                                       |
| caput PHOTO:trigcnt X      | Manipulates the trigger count value to be X                                         |
| caput PHOTO:debug "string" | Debugs the command placed within the string for the Photodetectors functions        |
| caget PHOTO:debug          | Returns the values that were used in the debug analysis                             |

## PULSE GENERATOR
| command                       | description                                                                      |
| ----------------------------- | -------------------------------------------------------------------------------- |
| caget PULSEGEN:info           | Gets information about the Pulse Generator device                                |
| caput PULSEGEN:reprate X      | Sets the repetition rate as X for all pulse channels                             |
| caget PULSGEN:reprate         | Returns the value of the reprate of the pulses for all channels.                 |
| caput PULSEGEN:CHN:delay X    | Sets channel N to have a delay of X after pulse trigger                          |
| caget PULSGEN:CHN:delay       | Returns the value of the delay from channel N                                    |
| caput PULSEGEN:debug "string" | Debugs the command placed within the string for the Pulse Generator functions    |
| caget PULSEGEN:debug          | Returns the values that was used within the debug for analysis                   |

## SHUTTER
| command                       | description                                                                      |
| ----------------------------- | -------------------------------------------------------------------------------- |
| caget SHUTTER:info            | Gets information about the Shutter  device                                       |
| caget SHUTTER:enable          | Finds out if the shutter is enabled or not.                                      |
| caput SHUTTER:enable X        | Sets the motor enable or not enabled. X is either 1 for on or 0 for off.         |
| caget SHUTTER:dur             | Gets the current duration time of shutter (microseconds)                         |
| caput SHUTTER:dur X           | Allows you to set the duration of the shutter detecting time in X (microseconds) |
| caput SHUTTER:debug "string"  | Debugs the command placed within the string for the shutter functions            |
| caget SHUTTER:debug           | Returns the values that was used within the debug for analysis                   |

