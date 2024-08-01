---
layout: default
title: Process Variables
authors:
    - Scott Feister
---

# Process Variables

## Pulse Generator

| Process Variable Name       | Example Usage                                                              | Description                                       | Record Type |
|-----------------------------|----------------------------------------------------------------------------|---------------------------------------------------|-------------|
| PULSEGEN:info               | caget PULSEGEN:info                                                        | Device identification                             | stringin    |
| PULSEGEN:debug              | Advanced - don’t use right now                                             |                                                   | stringin    |
| PULSEGEN:trigger:count      | caget PULSEGEN:trigger:count                                               | Get global trigger count                          | int64in     |
| PULSEGEN:trigger:count:set  | caput PULSEGEN:trigger:count:set 10                                        | Set global trigger count                          | int64out    |
| PULSEGEN:output:enabled     | caget PULSEGEN:output:enabled                                              | Get whether TTL pulse output is enabled           | bi (bool)   |
| PULSEGEN:output:enabled:set | caput PULSEGEN:output:enabled:set 1 Or caput PULSEGEN:output:enabled:set 0 | Set whether TTL pulse output is enabled           | bo (bool)   |
| PULSEGEN:reprate            | caget PULSEGEN:reprate                                                     | Get repetition rate (Hz) of pulse generator       | ai (float)  |
| PULSEGEN:reprate:set        | caput PULSEGEN:reprate:set 10                                              | Set repetition rate (Hz) of pulse generator       | ao (float)  |
| PULSEGEN:CH1:delay          | caget PULSEGEN:CH1:delay                                                   | Get pulse delay time (microseconds) for Channel 1 | int64in     |
| PULSEGEN:CH1:delay:set      | caput PULSEGEN:CH1:delay:set 220                                           | Set pulse delay time (microseconds) for Channel 1 | int64out    |
| PULSEGEN:CH2:delay          | caget PULSEGEN:CH2:delay                                                   | Get pulse delay time (microseconds) for Channel 2 | int64in     |
| PULSEGEN:CH2:delay:set      | caput PULSEGEN:CH2:delay:set 220                                           | Set pulse delay time (microseconds) for Channel 2 | int64out    |
| PULSEGEN:CH3:delay          | caget PULSEGEN:CH3:delay                                                   | Get pulse delay time (microseconds) for Channel 3 | int64in     |
| PULSEGEN:CH3:delay:set      | caput PULSEGEN:CH3:delay:set 220                                           | Set pulse delay time (microseconds) for Channel 3 | int64out    |
| PULSEGEN:CH4:delay          | caget PULSEGEN:CH4:delay                                                   | Get pulse delay time (microseconds) for Channel 4 | int64in     |
| PULSEGEN:CH4:delay:set      | caput PULSEGEN:CH4:delay:set 220                                           | Set pulse delay time (microseconds) for Channel 4 | int64out    |

## Laser Driver

| Process Variable Name    | Example Usage                                                        | Description                                              | Record Type |
|--------------------------|----------------------------------------------------------------------|----------------------------------------------------------|-------------|
| LASER:info               | caget LASER:info                                                     | Device identification                                    | stringin    |
| LASER:debug              | Advanced - don’t use right now                                       |                                                          | stringin    |
| LASER:trigger:count      | caget LASER:trigger:count                                            | Get global trigger count                                 | int64in     |
| LASER:trigger:count:set  | caput LASER:trigger:count:set 10                                     | Set global trigger count                                 | int64out    |
| LASER:output:enabled     | caget LASER:output:enabled                                           | Get whether laser output is enabled..                    | bi (bool)   |
| LASER:output:enabled:set | caput LASER:output:enabled:set 1 Or caput LASER:output:enabled:set 0 | Set whether laser output is enabled..                    | bo (bool)   |
|     Temporal Shaping:    |                                                                      |                                                          |             |
| LASER:powers:nt          | caget LASER:powers:nt                                                | Get number of timesteps in the laser powers array        | longin      |
| LASER:powers:dt          | caget LASER:powers:dt                                                | Get microseconds between timesteps in laser powers array | longin      |
| LASER:powers:dt:set      | caput LASER:powers:dt:set 100                                        | Set microseconds between timesteps in laser powers array | longout     |
| LASER:powers             | caget LASER:powers                                                   | Get laser powers array values                            | aai (uint8) |
| LASER:powers:set         | caput LASER:powers:set 1,2,3,4,5,6…                                  | Set laser powers array values                            | aao (uint8) |

## Photodetectors (Electrons and Protons)

Below, replace “ELECTRON” with “PROTON” if you wish to access the PROTON IOC instead.

| Process Variable Name      | Example Usage                           | Description                                                                     | Record Type           |
|----------------------------|-----------------------------------------|---------------------------------------------------------------------------------|-----------------------|
| ELECTRON:info              | caget ELECTRON:info                     | Device identification                                                           | stringin              |
| ELECTRON:debug             | Advanced - don’t use right now          |                                                                                 | stringin              |
| ELECTRON:trigger:count     | caget ELECTRON:trigger:count            | Get global trigger count                                                        | int64in               |
| ELECTRON:trigger:count:set | caput ELECTRON:trigger:count:set 125213 | Set global trigger count                                                        | int64out              |
| ELECTRON:dt                | caget ELECTRON:dt                       | Get time (in seconds) between subsequent ADC measurements                       | ai (float)            |
| ELECTRON:dt:set            | caput ELECTRON:dt:set 1e-4              | Set time (in seconds) between subsequent ADC measurements                       | ao (float)            |
| ELECTRON:trace:dt          | caget ELECTRON:trace:dt                 | Get trace metadata: time step  (in seconds). (Matches ELECTRON:dt for now)      | ai (float)            |
| ELECTRON:trace:nt          | caget ELECTRON:trace:nt                 | Get trace metadata: number of time steps                                        | int64in               |
| ELECTRON:trace:ymin        | caget ELECTRON:trace:ymin               | Get trace metadata:  y-minimum, in Volts                                        | ai (float)            |
| ELECTRON:trace:ymax        | caget ELECTRON:trace:ymax               | Get trace metadata: y-maximum, in Volts                                         | ai (float)            |
| ELECTRON:trace:yarr        | caget ELECTRON:trace:yarr               | Get trace data: array of y-values; length of array matches number of time steps | aai (array of floats) |