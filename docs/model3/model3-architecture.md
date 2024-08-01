---
layout: default
title: Architecture
authors:
    - Scott Feister
---

# Architecture of Sidekick Model 3

Sidekick Model 3 is designed to be high-performance and **high-repetition-rate** (0.1 Hz to kHz). It is currently the most advanced sidekick system.
 
The mock embedded devices are built from Teensy 4.0 microcontrollers to leverage their high performance (Cortex 32-bit microcontroller with 600 MHz clock speed). The computer controllers incorporate EPICS Channel Access protocol for controls, and EPICS PVAccess protocol for structured data acquisition.

The system allows for variable laser temporal pulse shaping and synthetic diagnostics with high-data-rate, timestamped data. It is designed to help with development of high-repetition-rate data pipelines.

![Sidekick_Model3_Architecture](https://github.com/user-attachments/assets/bdbfb967-eae9-4a14-a657-2dd13c585b13)
