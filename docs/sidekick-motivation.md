---
layout: default
title: Motivation
authors:
    - Scott Feister
---

# Motivation for the Sidekick System

## Problem: Control Systems, Data Acquisition, and Intense Laser Laboratories
Improvements in data acquisition capacity and autonomous feedback control loops is unlocking a high-repetition-rate, A.I. driven frontier in the fusion energy sciences. However, there is a major bottleneck in the development process of these future systems: existing systems are already doing important science with expensive equipment – this "current science" need becomes in tension with a "future infrastructure" need at existing facilities. The state-of-the-art physics drivers (including [NIF](https://lasers.llnl.gov/about/what-is-nif) and [ITER](https://www.iter.org/mach), but also including multi-million-dollar facilities at university-scale such as those in [LaserNetUS](https://lasernetus.org/facilities)) are not suitable platforms to perform first-effort, wide-ranging, innovative explorations in digital infrastructure and closed-loop control schemes.

[//]: # (High-repetition-rate, high-power lasers will result in orders of magnitude more digital data than our field is accustomed to managing. All members of the high-intensity laser-plasma physics community are stakeholders in data and control systems for the next generation of higher-repetition-rate experiments.)

## Bigger Centralized Systems Aren't the Solution
Centralized data systems are common at high-intensity laser facilities and have permitted great science with small-scale data. A single computer manages data acquisition, analysis, storage, and visualization for each of its instruments. Unfortunately, centralized systems will struggle to scale to higher data rates and heavier data analysis for synchronous acquisitions across many instruments.

![Distributed vs Centralized Control Systems](https://user-images.githubusercontent.com/7269185/155596717-cf409000-c993-4136-91ae-369ce32a26a1.png)

Distributed data systems permit data to be acquired, analyzed, and stored at different locations throughout a laboratory. Adding and removing components in a distributed data system does not require central coordination. This makes the distributed data approach ideal for collaborations of scientists in our community, where scientific instruments and techniques travel between facilities. However, building a performant, maintainable distributed data system with experimental physics skillsets can be daunting!

Read more about approaches taken by the high power laser in a manuscript:

> [**Control systems and data management for high-power laser facilities** (2023)](https://doi.org/10.1017/hpl.2023.49)
> 
> Feister, Scott; Cassou, Kevin; Dann, Stephen; Döpp, Andreas; Gauron, Philippe; Gonsalves, Anthony J; Joglekar, Archis; Marshall, Victoria; Neveu, Olivier; Schlenvoigt, Hans-Peter; Streeter, Matthew J V; Palmer, Charlotte A J
> 
> *High Power Laser Science and Engineering*, 11, e56

## Sidekick Facilities as a Rapid-Prototyping Testbed
We have created small prototyping facilities that contain everything challenging about an intense-laser laboratory (data infrastructure, latencies, networking, software stacks, machine learning and A.I. feedback loops, physical controls) except for the physics. Because the facilities are not the actual facilities, but rather surrogate facilities, we call this new infrastructure “sidekick facilities”. We are using our sidekick facility infrastructure as a prototyping platform to build real-facility digital infrastructure. We have created several complementary models of sidekick facilities (Model 1, Model 2, Model 3,...), and we have documented these models to increase our scientific impact on the community.

## Why EPICS?
There are many viable solutions to implementing next-generation control systems and data pipelines. [EPICS](https://epics-controls.org/) is a distributed control system architecture with a large user community in experimental physics. It is entirely open source and has workshops, active development, and active community support. EPICS is used at over a hundred worldwide physics facilities including LIGO, ITER, and SLAC. Furthermore, EPICS is natively supported by [Bluesky](https://blueskyproject.io/), a data acquisition and experiment orchestration system. While the learning curve for EPICS can be daunting, the work documented here shows that a high-quality scientific control system and data system is not out of reach, even at the smallest of laboratories.
