---
layout: default
title: IOC Administration
authors:
    - Scott Feister
---

# IOC Administration
All IOCs are set up as Linux services (via [systemd-softioc](https://github.com/NSLS-II/systemd-softioc)) on sk1 and sk2. As needed, you may perform administration of the IOCs as needed by SSHing into sk1 or sk2.

## Checking on which IOCs are running on this PC

```bash
manage-iocs status
debian@sk2:~$ manage-iocs status
softioc-ELECTRON.service                Running
softioc-PROTON.service          Running
```

```bash
debian@sk1:~$ manage-iocs status
softioc-PULSEGEN.service                Running
```

## Looking at logs for IOCs

`cat /var/log/softioc/ELECTRON/ELECTRON.log`

Or

`watch tail /var/log/softioc/ELECTRON/ELECTRON.log`

## Logging into an EPICS IOC Shell for troubleshooting
The [EPICS IOC Shell](https://epics.anl.gov/base/R3-14/12-docs/AppDevGuide/node19.html) is extremely useful to know about. Here's how you can access it for troubleshooting.

`manage-iocs report`   (to get port number of the IOC)

`telnet localhost 4051`  (or whatever port number the IOC shows in “manage-iocs report”)

Type "Enter" to get to the EPICS IOC Shell.

To Exit Telnet: Type `Ctrl +]`, then type in `quit`

## EPICS IOC Shell commands:
These particular commands are helpful for troubleshooting. You can read about many other commands in the EPICS IOC Shell documentation in the EPICS Applications Developers Guide.

| Command | Description | Example |
| --- | --- | --- |
| dbl | Lists out all PVs for this IOC |
| dbgf(“....”) | Equivalent of “caget …” |
| dbpf(“....”, 10) | Equivalent of “caput …. 10” |
| streamReload | Reset communication with the device (restarts streamDevice) |
| exit | Reboots the entire IOC (for a systemd-ioc managed IOC) |

## Restarting an IOC

```bash
sudo manage-iocs restart ELECTRON
```
