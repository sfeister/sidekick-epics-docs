---
layout: default
title: CAD Files (Bookshelf F.F.)
authors:
    - Scott Feister
---

# CAD Files (Bookshelf F.F.)

## Laser-Cut Elements

The enclosure was created in [Boxes.py (online tool for designing laser-cut boxes)](https://boxes.hackerspace-bamberg.de/). That tool creates an SVG, which was then downloaded and customized in [Inkscape](https://inkscape.org/).

The final [SVG File for Laser-Cutting the Enclosure of Model 3 (Bookshelf F.F.)](https://raw.githubusercontent.com/sfeister/dolphindaq/refs/heads/main/CNC/Sidekick%20Model%203%20-%20Bookshelf%20FF/Enclosure.svg) is hosted at the dolphindaq repository.

You can download that SVG, then import it into your laser-cutter's software. It's designed to be cut on 1/8" basswoood (having tweaked the interlocking gaps on Boxes.py for a nice press-fit). Before you do the cuts, make note of instructions within the SVG about which layers must be scored, and which layers must be cut through.

## 3D-Printed Elements

There are a few beam enclosures that the lasers and photodiode fit into, that are 3D printed. CAD files from which the Model 3 (Bookshelf Form Factor) were built are on Fusion360. I've exported them to STL files. Reach out to me if you get confused on how these pieces fit together.

The [STL files are all together in the dolphindaq repository](https://github.com/sfeister/dolphindaq/tree/main/CNC/Sidekick%20Model%203%20-%20Bookshelf%20FF).

You will need to print out:

* Three "Extra Collimated Laser Holder" (print in white). The extra-collimated version is nice for safety purposes, as it blocks unwanted angles of emission.

* Three "Detector Base" (print one in white, two in black). These hold the photodetectors.

* Three "Regular Pinhole Detector Barrel" (print one in white, two in black). These press into the Detector Bases, holding in the photodetectors / diffusing pucks and collimating the incoming light.

* (Optional) Three "Diffusing Puck" (print in white). These sit directly on top of the photodetectors.