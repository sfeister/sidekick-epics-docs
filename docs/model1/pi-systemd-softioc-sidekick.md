---
layout: default
title: Download Sidekick IOCs
authors:
    - Scott Feister
---

# Blend Sidekick Files into the StreamDevice Demo IOCs
You will download the StreamDevice configuration files for the sidekick system from GitHub, and use symbolic links to insert them into the demo IOC for StreamDevice.

You will also create an IOC configuration usable from systemd-softioc, such that you can automatically start the IOCs at first boot, and manage the iocs with `manage-iocs`.

## References
1. [Systemd-SoftIOC GitHub Page](https://github.com/NSLS-II/systemd-softioc)

## Pre-requisites
* Internet connection

## Materials
* Raspberry Pi with EPICS, StreamDevice, and systemd-softioc installed

## Steps

### Download Sidekick EPICS Source Files
Navigate into your EPICS folder, and then download the latest sidekick-epics files from GitHub via `git clone`.

```bash
cd $HOME
git clone https://github.com/sfeister/sidekick-epics.git
```

This will create a folder `sidekick-epics` in your home directory. Inside will be the latest, up-to-date prototype files for StreamDevice. At any time, you can navigate into that directory and call `git pull` to update the files to the latest version.

### Create new IOC folder for systemd-softioc

Note: Follow along here with the instructions at the [Systemd-SoftIOC GitHub Page](https://github.com/NSLS-II/systemd-softioc) for more details about what these settings do!

#### Note down hostname and the next good port.

```
hostname -s
manage-iocs nextport
```

I got as return:
```
epics1
4050
```

Make note of both of these items! You will use them in the config below.

#### Assume the softioc user, create an IOC folder, and edit a config file

Change into the softioc user.
```bash
sudo -s -u softioc
```

Create a unique folder within `/epics/iocs/` for this new IOC.

For example, I am choosing to name my IOC `LEDs`. Then, I would do:

```bash
cd /epics/iocs
mkdir LEDs
cd LEDs
nano config
```

And then I would edit the config file to say:

```
NAME=LEDs
PORT=4050
HOST=epics1
USER=softioc
```

Where I set the `HOST` and `PORT` from what I noted down above.

#### Link in the StreamDevice Demo IOC files

Continue as the `softioc` user for this portion.

From within the same IOC folder, make symbolic links to all the contents of the StreamDevice demo IOC folder.

```
ln -s /home/pi/EPICS/support/StreamDevice/streamApp/* ./
```

This is a cheat to avoid building your own IOC -- we will just basically copy / link in the files from the StreamDevice demo instead!

#### Link in the Sidekick EPICS proto files
Continue as the `softioc` user for this portion.

From within the same IOC folder, make symbolic links to all the contents of the sidekick EPICS StreamDevice folder. This includes prototype files, etc. Since we are linking rather than copying, any updates to our files in the cloned repository will be reflected in our setup down the road.

```bash
ln -s /home/pi/sidekick-epics/streamDevice/* ./
```

#### Configure the startup script

Edit a new `st.cmd` file.

```bash
nano st.cmd
```

And then fill the contents of this new file with:

```bash
export EPICS_BASE=/home/pi/EPICS/epics-base
export EPICS_HOST_ARCH=$(${EPICS_BASE}/startup/EpicsHostArch)
export PATH=${EPICS_BASE}/bin/${EPICS_HOST_ARCH}:${PATH}

bash ./leds.cmd
```

Where the last line, `./leds.cmd`, is whatever startup script you want to run from the sidekick-epics files.

Finally, make your `st.cmd` startup script executable.

```bash
chmod +x st.cmd
```

You can now test it before continuing:

```bash
./st.cmd
```

And then, before closing the process, open another terminal window and check that `caget` is working correctly.

Finally, kill the process and open a new terminal window under the user `pi`.


#### Install the IOC with manage-iocs


Finally, from another terminal window logged in as the `pi` user, install the IOC using `manage-iocs`.

```bash
manage-iocs report
sudo manage-iocs install LEDs
sudo manage-iocs start LEDs
```

When prompted about whether you want to start `LEDs` at boot, say yes. This will start the IOC automatically every time the pi boots up.

If you want to restart the IOC or stop the IOC, here are two more useful commands:

```bash
sudo manage-iocs restart LEDs
sudo manage-iocs stop LEDs
```

If you want to peer in at what's happening with the IOC, try
```
telnet localhost 4050
```

where 4050 is the previously set port value.

### Conclusion
Congratulations! You should be able to manage your IOCs with `manage-iocs` commands and the IOC should now start up every time you boot the computer.

You can adapt the above instructions for the other computers which will be running the other IOCs, like the shutter IOC and the pulse generator IOCs.