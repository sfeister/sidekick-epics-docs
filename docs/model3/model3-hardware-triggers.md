---
layout: default
title: Hardware Trigger Details
authors:
    - Scott Feister
---

# Hardware Timing Connections and Tolerances for Model 3

The hardware triggers are a 3V 10-microsecond TTL active-high signal sent via BNC cables from the pulse generator to the other devices.

## Connections

| BNC Connection A | BNC Connection B | Description |
|------- |------- | ----- |
| Pulse Generator CH1 | Unused  | |
| Pulse Generator CH2 | Laser Driver | Trigger input for Laser Driver      |
| Pulse Generator CH3 | Electron Detector | Trigger input for Electron detector |
| Pulse Generator CH4 | Proton Detector | Trigger input for Proton detector   |

## Timing Tolerances
Pulse generator: +/- 5 us or so accuracy, sub-microsecond stability
Laser trigger to laser activation: 26 microseconds delay, +/- 2 microsecond stability