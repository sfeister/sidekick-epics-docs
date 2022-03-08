# Installing "manage-iocs" on Raspberry Pi

We will use `manage-iocs` to automatically boot the IOC on startup. Here's how you install and configure manage-iocs in this way on Raspberry Pi OS.

## References
1. [Systemd-SoftIOC GitHub Page, including Installation Instructions](https://github.com/NSLS-II/systemd-softioc)

## Pre-requisites
* 

## Materials
* 

## About systemd-softioc
"manage-iocs" is a tool in the GitHub package "systemd-softioc". It was developed at the Diamond Light Source for easy remote management of IOCs. This tool was recommended by the developer on the EPICS User List.

Features:
* Run multiple iocs automatically on boot
* Concise step-by-step documentation aimed directly at our use case
* Relatively easy configuration and future modification of the configuration
* Remote access to the EPICS shell

Note that systemd-softioc is based on procServ, if that means anything to you!

### Other solutions we considered:
* Procserutils is not well maintained, nor does it have good documentation
* ProcServ is too low level; this wraps around it for easier usage

## Steps
