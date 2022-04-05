---
layout: default
title: Overview of the Sidekick System
authors:
    - Scott Feister
---

# Overview of the Sidekick System

The goal of this system is to model some of the challenges of control systems for a real-world high-intensity laser system.

This sidekick system was created by Dr. Scott Feister and undergraduates Keily Valdez Sereno and Emiko Ito at California State University Channel Islands.

![Sidekick Broad View Small](https://user-images.githubusercontent.com/7269185/156228045-ae113b35-8891-4ca8-96da-a0b1969d2df6.JPG)

## Introduction
High-repetition-rate, high-power lasers will result in orders of magnitude more digital data than our field is accustomed to managing. All members of the high-intensity laser-plasma physics community are stakeholders in data and control systems for the next generation of higher-repetition-rate experiments.

To meet the needs of our wide range of stakeholders, we are testing the viability of a distributed control system architecture used in many physics facilities throughout the world: EPICS. Our approach to learning EPICS at California State University Channel Islands (CSUCI) is to start small, fail fast, and build up. Our goal is to get a head start on addressing challenges of distributed feedback control loops, synchronous data collection, and pre-programmable shot sequences. 

## Centralized vs Distributed Control Systems
Centralized data systems are common at high-intensity laser facilities and have permitted great science with small-scale data. A single computer manages data acquisition, analysis, storage, and visualization for each of its instruments. Unfortunately, centralized systems will struggle to scale to higher data rates and heavier data analysis for synchronous acquisitions across many instruments.
![image](https://user-images.githubusercontent.com/7269185/155596717-cf409000-c993-4136-91ae-369ce32a26a1.png)

Distributed data systems permit data to be acquired, analyzed, and stored at different locations throughout a laboratory. Adding and removing components in a distributed data system does not require central coordination. This makes the distributed data approach ideal for collaborations of scientists in our community, where scientific instruments and techniques travel between facilities. However, building a performant, maintainable distributed data system with experimental physics skillsets can be daunting!

## EPICS: Distributed Control for Scientists
[EPICS](https://epics-controls.org/) is a distributed control system architecture with a large user community in experimental physics. It is entirely open source and has workshops, active development, and active community support. EPICS is used at over a hundred worldwide physics facilities including LIGO, ITER, and SLAC. It is clearly performant, and has the necessary community support – but is the learning curve too steep for staff and students at our smaller university-scale laser facilities? We set out to demonstrate a simple control system feedback loop in EPICS that still maintains levels of relevance to laser laboratories. We nicknamed this the "sidekick system".

# Sidekick System
[![](https://mermaid.ink/img/pako:eNqVVU2PmzAU_CuWc00OgUvFVpXagCBS1KAl2wvswTWmoAJGxnQbbfa_95mPQICkSQ6RM_NmsMePl3dMeciwgaOUv9GYCIkOZpAj-NCUlKXJIkR5VqAoSVNjwai-LKXgv5mx0PVuvXpLQhkbWvH3aSQlIqxa6fpBacJppxSPKQWvJBOtOBKfHhKnpJC8O24UafeIy-rnL0GKGJnWj51lIt9kfxLKDAQ_ytemhuXhtNhzXvpiL64k7PtWvWv35W6VlgzZLGeCSH5b5uwHuphLuHLJ6C2V5W433hr5G7h7laaBWJHQct0K1Ge737i27_FIwur-_dTO2sRZu3SG5HrrQYwtDcH19P-Cq5-oT56oj87i7AeHuSuk3VdXRZQmLJdo1zTOYhiRKlj77lHGPDdQcayfe8tOm9hpIzvtAbvvyFdfz_X7MKxrlm23fl6tvpxevG-nNvczqbrzggTgTEIrXnCu3VPQbpecs2_Itqtq0jo4J7XHAaNdZfQ5po5_Hp91anat8MPz1j6157_KnXc9w9VJDCZHl6Wad08jXMU4h4PnLAzpTfDmZtRMHMPKfQYG8zkUvMdweydqyE9x7QquT3HVac3kHcFwSc1QHeNaj-MlzpjISBLCX9G7qguwjFnGAmzAMmQRqVIZ4CD_gNKqCIlkVpjAy4mNiMDgWWJSSe4dc4oNKSrWFZkJgbcha6s-_gFeJSL8)](https://mermaid.live/edit#pako:eNqVVU2PmzAU_CuWc00OgUvFVpXagCBS1KAl2wvswTWmoAJGxnQbbfa_95mPQICkSQ6RM_NmsMePl3dMeciwgaOUv9GYCIkOZpAj-NCUlKXJIkR5VqAoSVNjwai-LKXgv5mx0PVuvXpLQhkbWvH3aSQlIqxa6fpBacJppxSPKQWvJBOtOBKfHhKnpJC8O24UafeIy-rnL0GKGJnWj51lIt9kfxLKDAQ_ytemhuXhtNhzXvpiL64k7PtWvWv35W6VlgzZLGeCSH5b5uwHuphLuHLJ6C2V5W433hr5G7h7laaBWJHQct0K1Ge737i27_FIwur-_dTO2sRZu3SG5HrrQYwtDcH19P-Cq5-oT56oj87i7AeHuSuk3VdXRZQmLJdo1zTOYhiRKlj77lHGPDdQcayfe8tOm9hpIzvtAbvvyFdfz_X7MKxrlm23fl6tvpxevG-nNvczqbrzggTgTEIrXnCu3VPQbpecs2_Itqtq0jo4J7XHAaNdZfQ5po5_Hp91anat8MPz1j6157_KnXc9w9VJDCZHl6Wad08jXMU4h4PnLAzpTfDmZtRMHMPKfQYG8zkUvMdweydqyE9x7QquT3HVac3kHcFwSc1QHeNaj-MlzpjISBLCX9G7qguwjFnGAmzAMmQRqVIZ4CD_gNKqCIlkVpjAy4mNiMDgWWJSSe4dc4oNKSrWFZkJgbcha6s-_gFeJSL8)

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

For more details, see the document on the [Sidekick Analogies](sidekick-analogies.md).

## Next Steps
This sidekick system could be very useful to small groups looking to explore using EPICS for machine learning feedback loops. We plan to create and ship several of these to collaborators.
