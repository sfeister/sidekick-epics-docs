---
layout: default
title: SSH & Flashing into the PIs
authors:
 - Elias Dandouch
 - Scott Feister
---

# Step 3: SSH and Flash Raspberry Pi Devices (30 minutes per device)

### Part A: Flash the First Pi (15 minutes)

#### Prepare SD Card and Imager
1. Insert microSD card into your computer via USB reader
2. Download and install [Raspberry Pi OS Imager](https://www.raspberrypi.com/software/)
3. Open the imager software

#### Configure OS Settings
1. **Operating System**: Click "CHOOSE OS" → "Raspberry Pi OS (other)" → "Raspberry Pi OS Lite"
2. **Storage**: Click "CHOOSE STORAGE" and select your microSD card
3. **Advanced Options**: Press "CTRL + SHIFT + X" or click the gear icon

#### Advanced Configuration (Required)
Configure these settings in the Advanced Options window:

**Essential Settings:**
- **Hostname**: Set to "epics1.local" (unique identifier)
- **Enable SSH**: Check box and set a secure password
- **Username**: Keep as "pi" or set custom username
- **Set locale settings**: Configure timezone, check "Skip first run wizard"

**Optional WiFi Settings:**
- **WiFi SSID**: Your network name
- **WiFi Password**: Network password
- **WiFi Country**: Your country code

Click "Save" then "Write" to flash the card.

#### Boot and Network Connection
1. Insert flashed SD card into first Raspberry Pi
2. Connect Ethernet cable between Pi and router
3. Connect power cable - Pi will boot automatically
4. Wait 3-5 minutes for initial boot process

### Part B: Establish SSH Connection (10 minutes)

#### Locate Pi on Network
1. Access your router's admin panel
2. Look for "epics1" in connected devices list
3. Note the assigned IP address (e.g., 192.168.1.100)

#### Connect via SSH
**Linux/macOS:**
```bash
ssh pi@192.168.1.100
```

**Windows (PowerShell):**
```bash
ssh pi@192.168.1.100
```

**Windows (PuTTY):**
- Host: 192.168.1.100
- Username: pi
- Password: [your set password]

#### Verify Connection
Successful connection shows:
```bash
pi@epics1:~ $
```

#### Update System
```bash
sudo apt -y update
sudo apt -y upgrade
```
*This process takes 15-20 minutes on first boot.*

### Part C: Repeat for Second Pi (15 minutes)

Follow the same process for your second Pi with these changes:
- **Hostname**: Set to "epics2.local"
- **Different SD Card**: Use your second microSD card
- **Second Ethernet Port**: Connect to different router port
- **Unique IP**: Router will assign different IP address

## Test Communication Between Your Pis

Once both devices are set up and accessible via SSH, verify they can communicate with each other:

**From Pi 1 (epics1), test connection to Pi 2:**
```bash
ssh pi@epics2.local
# Or use the IP address directly:
ssh pi@[EPICS2_IP_ADDRESS]
```

**From Pi 2 (epics2), test connection to Pi 1:**
```bash
ssh pi@epics1.local
# Or use the IP address directly:
ssh pi@[EPICS1_IP_ADDRESS]
```

**Test network connectivity:**
```bash
# From either Pi, ping the other:
ping epics1.local
ping epics2.local
```

When you can successfully SSH between your Pi devices and see successful ping responses, you have achieved the goal of this module: **your Raspberry Pi devices can now communicate with each other**.

## Next Steps

With both Raspberry Pi devices successfully set up with SSH access and inter-Pi communication established, you're ready to proceed with building your EPICS development environment:

**Next tutorial:** [Install EPICS v7](../simple-ioc/pi-epics-install.md) - Install and configure the EPICS framework on both Pi devices

This will transform your networked Pi setup into a functional EPICS distribute