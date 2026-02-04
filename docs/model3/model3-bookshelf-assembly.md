---
layout: default
title: Assembly (Bookshelf F.F.)
authors:
    - Scott Feister
---

# Assembly (Bookshelf F.F.)

## Overview

Much of the physical assembly is undocumented. I designed the Bookshelf form-factor to be really quick to assemble - once you know how. reach out to me if you'd like help!

Basically, here are the steps to build the physical setup:

1. Laser cut and 3D print all parts.

1. Build the Enclosure.

1. Build the Physics/Interaction level.

1. Build the Device level.
 
1. Build the Computer level.

1. Build the Networking level.

1. Build the Power level.

1. Power on the system and use!

I will explain each of these steps, one-by-one, in the following several sections.

## Step-by-Step Instructions

### Laser Cut and 3D Print All Parts
See CAD Files page for more details.

1. Laser cut the enclosure.

1. 3D print the black parts.

1. 3D print the white parts.

### Build the Enclosure
Press fit together all the laser cut parts, to create the overall enclosure.

### Build the Physics/Interaction Level

1. Assemble the photodetectors and lasers with their 3D printed holders:

    * Shove the photodiodes into the detector bases. Add a puck on top of the photodetector. Press fit the barrels into the detector base.
  
    * Shove the lasers into the laser holders. Add black shrink wrap over the back of the laser and apply heat, blocking stray light so it doesn't leak out the back of the laser.
  
1. Get a small board (smaller than any bookshelf level) and place all assembled photodetectors and lasers atop of it.

1. Temporarily power the lasers using a 3V power source, and examine the detector output using an voltmeter.

1. Using your voltmeter as feedback of alignment, use super glue to align and super glue the lasers and photodiodes, onto the small board.

1. Disconnect your power supply and voltmeter. Move your assembled small board onto the Physics/Interaction level. This level is now complete.

### Build the Device Level

1. Connect each Teensy board to your laptop, and flash each with correct firmware. (see the "Flashing Teensy Firmware" page for more details.)

1. Move each Teensy onto its own breadboard.

1. Wire the lasers and photodiodes to the Teensies, using appropriate resistors for the lasers and photodiodes. (TODO: Document the electrical wiring! Reach out to Scott Feister for help in the meantime.)

1. (Optional) Test the device level using SCPI commands from your laptop. You can power the Teensies temporarily from your laptop or a USB power bank.

1. Disconnect your laptop and any power banks from the Teensies. Move all the Teensies into the Device Level. The Device Level is now complete.

### Build the Computer Level

1. Connect each SD card to your laptop, and use BalenaEtcher software to flash each with correct Linux image. (Reach out to Scott Feister for the Linux image.)

1. Plug the SD cards into the Beaglebones.

1. Connect the USB hubs to the two Beaglebones.

1. Connect each Teensy to the correct USB hub.

1. The Computer Level is now complete.

### Build the Networking Level

1. Grab your Network switch and ethernet cables.

1. Connect the Beaglebones to the Network switch (using 1.5 ft ethernet cables).

1. Add one more spare Ethernet cable dangling out from the networking switch. You'll use that later to connect your laptop or a gateway device.

1. The Networking Level is now complete.

### Build the Power Level

1. Grab your USB power bank.

1. Power the Beaglebones from the USB power bank.

1. Power the Network switch from the USB power bank (using the USB-to-12V barrel adapter).

1. Dangle the USB power bank's main power plug out of the enclosure.

1. The Power Level is now complete.

### Power on the System and Use!

1. Power the USB power bank from a wall outlet.

1. Connect your own laptop or gateway computer to the Network switch. SSH into your Beaglebones, or use EPICS commands over the network.
