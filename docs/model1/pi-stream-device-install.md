# Build and Install StreamDevice on Raspberry Pi (20 minutes)
By following these instructions, you will build and install StreamDevice, a supplemental package for EPICS. 

StreamDevice will facilitate your serial communication with Ethernet devices and USB devices (such as an Arduino).

## References
1. [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html)
1. [StreamDevice setup guide](https://paulscherrerinstitute.github.io/StreamDevice/setup.html)

## Pre-requisites
* EPICS v7 is already installed on your Raspberry Pi, per prior instructions
* Capability to SSH into your Raspberry Pi
* Working internet connection for your Raspberry Pi

## Materials
* Local area network
* Laptop / computer, connected to local area network
* Raspberry Pi, connected to local area network

## Steps

### SSH into your Raspberry Pi.

Follow the prior instructions to SSH into your Raspberry Pi from your Laptop / Computer.

### Install dependencies for StreamDevice (10 minutes)

##### Install PCRE packages

I'm not actually completely sure this step is still necessary, but:
```bash
sudo apt install -y libpcre2-dev
```

### Compile and install asyn

The *asyn* EPICS support module is another pre-requisite for *streamDevice*.

Navigate into the directory you made to hold EPICS items, into which you cloned the epics-base repository, and create a new folder to hold support items for EPICS base (e.g. additional modules).

```bash
cd $HOME/EPICS
mkdir support
cd support
```

Download asynDriver module source code and navigate into the folder

```bash
git clone https://github.com/epics-modules/asyn.git
cd asyn
```
    
Edit the `configure/RELEASE` file for asyn.

```bash
nano configure/RELEASE
```

```bash
#RELEASE Location of external products

SUPPORT=/home/pi/EPICS/support

#  IPAC is only necessary if support for Greensprings IP488 is required
#  IPAC release V2-7 or later is required.
# IPAC=$(SUPPORT)/ipac-2-15

# SEQ is required for testIPServer
# SNCSEQ=$(SUPPORT)/seq-2-2-5

## For sCalcout support in asynOctet - applications include asynCalc.dbd
# CALC=$(SUPPORT)/calc-3-7-3

# If CALC was built with SSCAN support then SSCAN must be defined for testEpicsApp
# SSCAN=$(SUPPORT)/sscan-2-11-3

#  EPICS_BASE 3.14.6 or later is required
EPICS_BASE=/home/pi/EPICS/epics-base

-include $(TOP)/../RELEASE.local
-include $(TOP)/../RELEASE.$(EPICS_HOST_ARCH).local
-include $(TOP)/configure/RELEASE.local
```

Above, we have edited the file to:

1. Comment out unneeded lines IPAC, SEQ, CALC, SSCAN, etc.

2. Set the SUPPORT and EPICS_BASE variables to point to the right folders for your computer

Save this file and then build the software.

```bash
make -j8
```

(took me about five minutes)

### Compile and install StreamDevice

Navigate back into the directory you made to hold EPICS support items.

```bash
cd $HOME/EPICS/support
```

Download StreamDevice module source code and navigate into the folder

```bash
git clone https://github.com/paulscherrerinstitute/StreamDevice.git
cd StreamDevice
```

Edit the `configure/RELEASE` file for StreamDevice.

```bash
nano configure/RELEASE
```

```bash
#RELEASE Location of external products
# Run "gnumake clean uninstall install" in the application
# top directory each time this file is changed.
#
# NOTE: The build does not check dependencies on files
# external to this application. Thus you should run
# "gnumake clean uninstall install" in the top directory
# each time EPICS_BASE, SNCSEQ, or any other external
# module defined in the RELEASE file is rebuilt.

TEMPLATE_TOP=$(EPICS_BASE)/templates/makeBaseApp/top

# If you don't want to install into $(TOP) then
# define INSTALL_LOCATION_APP here
#INSTALL_LOCATION_APP=<fullpathname>

SUPPORT=$(TOP)/..
-include $(TOP)/../configure/SUPPORT.$(EPICS_HOST_ARCH)

ASYN=$(SUPPORT)/asyn
#CALC=$(SUPPORT)/calc-3-7
#PCRE=$(SUPPORT)/pcre-7-2

# EPICS_BASE usually appears last so other apps can override stuff:
EPICS_BASE=/home/pi/EPICS/epics-base

# These lines allow developers to override these RELEASE settings
# without having to modify this file directly.
-include $(TOP)/../RELEASE.local
-include $(TOP)/../RELEASE.$(EPICS_HOST_ARCH).local
-include $(TOP)/configure/RELEASE.local
```

Above, we have edited the `configure/RELEASE` file such that:

1. Fix the "ASYN" line to match your actual file path from above: `ASYN=$(SUPPORT)/asyn`

1. Comment out the "CALC" and "PCRE" lines

1. Set the EPICS_BASE variable to point to the right folder for your computer (SUPPORT is already set up OK)

After saving that file, run `make` (or `make -j8` for faster results).
