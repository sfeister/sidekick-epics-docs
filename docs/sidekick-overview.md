# Overview of the Sidekick System

The goal of this system is to model some of the challenges of control systems for a real-world high-intensity laser system.

This sidekick system was created by Dr. Scott Feister and undergraduates Keily Valdez Sereno and Emiko Ito at California State University Channel Islands.

## Introduction
High-repetition-rate, high-power lasers will result in orders of magnitude more digital data than our field is accustomed to managing. All members of the high-intensity laser-plasma physics community are stakeholders in data and control systems for the next generation of higher-repetition-rate experiments.

To meet the needs of our wide range of stakeholders, we are testing the viability of a distributed control system architecture used in many physics facilities throughout the world: EPICS. Our approach to learning EPICS at California State University Channel Islands (CSUCI) is to start small, fail fast, and build up. Our goal is to get a head start on addressing challenges of distributed feedback control loops, synchronous data collection, and pre-programmable shot sequences. 

## Centralized vs Distributed Control Systems
Centralized data systems are common at high-intensity laser facilities and have permitted great science with small-scale data. A single computer manages data acquisition, analysis, storage, and visualization for each of its instruments. Unfortunately, centralized systems will struggle to scale to higher data rates and heavier data analysis for synchronous acquisitions across many instruments.
![image](https://user-images.githubusercontent.com/7269185/155596717-cf409000-c993-4136-91ae-369ce32a26a1.png)

Distributed data systems permit data to be acquired, analyzed, and stored at different locations throughout a laboratory. Adding and removing components in a distributed data system does not require central coordination. This makes the distributed data approach ideal for collaborations of scientists in our community, where scientific instruments and techniques travel between facilities. However, building a performant, maintainable distributed data system with experimental physics skillsets can be daunting!

## EPICS: Distributed Control for Scientists
[EPICS](https://epics-controls.org/) is a distributed control system architecture with a large user community in experimental physics. It is entirely open source and has workshops, active development, and active community support. EPICS is used at over a hundred worldwide physics facilities including LIGO, ITER, and SLAC. It is clearly performant, and has the necessary community support – but is the learning curve too steep for staff and students at our smaller university-scale laser facilities? We set out to demonstrate a simple control system feedback loop in EPICS that still maintains levels of relevance to laser laboratories. We nicknamed this the "sidekick system".

## Elements of the Sidekick System
Our "sidekick system" EPICS demo consists of:
* Light source (six LEDs)
* Optical detector (a phototransistor)
* Shutter (a servo motor which swings an object to block light)
* Several Raspberry Pi computers
* Several Arduino microcontrollers
* Laptops
* A wired local area network

All components work together thanks to EPICS, which runs on all the computers in the system. The workload of control, acquisition, analysis, and visualization is distributed.

## Analogy between Sidekick Elements and Laser Laboratory

#### Trigger Signals for Lasers and Diagnostics

In high-intensity laser laboratories, trigger cables fan out from a pulse generator (or several pulse generators) to all elements of the laser system and the experimental diagnostics. Correct trigger timing is essential for everything from flashing the laser diodes to opening the electronic shutter of a detector. Many of these system elements require independent timing signals; for example, we want the laser amplifier delay to be different from the camera trigger delay.

We've attempted to replicate this general idea in the sidekick system. We have programmed an Arduino to serve as a low-quality, USB-controlled trigger pulse generator for the other elements of the sidekick system. Just like in a real laser laboratory, this Arduino pulse generator outputs up to eight independently delayed trigger signals over BNC cables.

| Feature      | Arduino Pulse Generator in the Sidekick System | BNC Model 575 Pulse Generator in a Laser Lab |
| ----------- | ----------- | ----------- | 
| Pulse and Delay Resolution: | ~ 1 ms | ~ 250 ps |
| Typical TTL pulse width | 100 us | 1 us |
| Trigger Outputs | 8x Independent BNC Outputs | 8x Independent BNC Outputs |
| System Control | USB via Serial Commands | Ethernet or USB via Serial Commands |
| Price | ~$20 | ~$5000 |

#### Pulsed Light Source

High-intensity lasers are created through a series of amplification stages. Each stage has controls and idiosynchrosies which affect the final laser parameters -- such as energy, spectrum, and duration -- in a non-linear fashion. The amplification stages rely on timing signals from the pulse generator.

In the sidekick system, we've attempted to capture some small element of this complexity. We've created a light source that consists of six separate pulsed LEDs. Each LED has an independent delay and and independent pulse duration. The LED system is triggered from a BNC cable running from the pulse generator.

| Feature      | Arduino Triggered LEDs in the Sidekick System | Triggered Laser Source in a Laser Lab |
| ----------- | ----------- | ----------- | 
| Light Source | 6X independently timed and delayed LED flashes | Amplified Laser Beam |
| Example Pulse Duration | 5 ms | 500 fs |
| Pulse Duration | Controllable | Controllable |
| Trigger Inputs | BNC Cables from Pulse Generator | BNC Cables from Pulse Generator |
| System Control | USB controlled via Serial Commands | Varies; Ethernet and USB via Serial Commands |
| Acquisition Cost | ~$20 | $1 million - $100 million |
| Footprint | Postcard | Multiple rooms |

#### Triggered Experimental Diagnostics

Triggered Phototransistor Diagnostic in the Sidekick System
Signal Responds to Light Source Configuration (allows for closed-loop operation)
Controlled via Ethernet or USB Serial Commands
Data is retrieved via Ethernet or USB on a shot-by-shot basis

Triggered Experimental Diagnostic in a Laser Lab
Signal Responds to Light Source Configuration (allows for closed-loop operation)
Controlled via Ethernet or USB Serial Commands
Data is retrieved via Ethernet or USB on a shot-by-shot basis

## Next Steps
This sidekick system could be very useful to small groups looking to explore using EPICS for machine learning feedback loops. We plan to create and ship several of these to collaborators.

## What are you qualifications to build this?
Scott Feister has worked with and made additions to several control systems at high-intensity laser facilities. He has watched what works and what doesn't work in high-repetition-rate data acquisition at these facilities, and learned from his own mistakes there as well.

## Acknowledgments
This work is supported by Lawrence Livermore National Laboratory, LLC under Subcontract No. B645313, and LDRD 21-ERD-015 and DOE Early Career SCW1651. LLNL is under Prime Contract No. DE-AC52-07NA27344 with the DOE/NNSA.
