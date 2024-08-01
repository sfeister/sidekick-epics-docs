---
layout: default
title: Repeat on Additional Pis
authors:
    - Scott Feister
---

# Repeat Steps for Additional Pis
One easy way to repeat this process on additional identical Raspberry Pis is to mimick the steps in a much faster way.

## References
1. [Systemd-SoftIOC GitHub Page](https://github.com/NSLS-II/systemd-softioc)

## Pre-requisites
* Internet connection

## Materials
* Raspberry Pi with EPICS, StreamDevice, and systemd-softioc installed

## Steps

### Flash the Pi
Same as before, but this time use a hostname of, say `epics2` instead of `epics1`.

### First Boot
Once again, find the IP on the network and SSH into your new pi.

Then, update the system.

```bash
sudo apt -y update
sudo apt -y upgrade
```

Next, install a variety of dependencies.

```bash
sudo apt -y install build-essential git net-tools libpcre3 libpcre3-dev procserv telnet
```

Copy the binaries from the `home/pi/EPICS/` folder on your first Raspberry Pi into the `/home/pi/EPICS/` folder on your second Rasbperry Pi.

Update your `$HOME/.bashrc`

Create `softioc` user and install `manage-iocs`.

