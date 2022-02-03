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

### Install StreamDevice Module for serial device communication

#### Install dependencies for StreamDevice (10 minutes)

##### Install PCRE packages

1. `sudo apt install -y libpcre3 libpcre3-dev`
    1. Note: libpcre3 (runtime files) is probably already installed, but libpcre3-dev (include files, etc) is probably not.
1. (Optional) Check that "/usr/include/" now contains header files for PCRE, such as "pcre.h", and that "/usr/lib/x86_64-linux-gnu/" now contains files such as "libpcre.so". You can do this in at least two ways:
    1. Option A: Go check out package details for libpcre3 and libpcre3-dev and see where items went (see references for package lists, then go to "list files" under your architecture)
    1. Option B: Call these two commands:
        1. `whereis pcre`, which returns for my system: `pcre: /usr/include/pcre.h /usr/share/man/man3/pcre.3.gz`
        1. `whereis libpcre` which returns for my system: `libpcre: /usr/lib/arm-linux-gnueabihf/libpcre.a /usr/lib/arm-linux-gnueabihf/libpcre32.so /usr/lib/arm-linux-gnueabihf/libpcre.so /usr/lib/arm-linux-gnueabihf/libpcre32.a /usr/lib/arm-linux-gnueabihf/libpcre16.a /usr/lib/arm-linux-gnueabihf/libpcre16.so`


##### Compile and install asynDriver module, which is a pre-requisite for stream
1. Navigate into the directory you made to hold EPICS items, into which you cloned the epics-base repository, and create a new folder to hold support items for EPICS base (e.g. additional modules).
    1. `cd $HOME/EPICS`
    1. `mkdir support`
    1. `cd support`
1. Download asynDriver module source code and navigate into the folder
    1. `git clone https://github.com/epics-modules/asyn.git`
    1. `cd asyn`
1. Set up the RELEASE file
    1. `nano configure/RELEASE`
        1. Comment out unneeded lines IPAC, SEQ, CALC, SSCAN, etc.
        2. Set the SUPPORT and EPICS_BASE variables to point to the right folders for your computer
        3. E.g. make the file look like this:
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
        1. `make` (took me about five minutes)

#### Compile and install StreamDevice
1. Navigate back into the directory you made to hold EPICS support items.
    1. `cd $HOME/EPICS/support`
1. Download StreamDevice module source code and navigate into the folder
    1. `git clone https://github.com/paulscherrerinstitute/StreamDevice.git`
    1. `cd StreamDevice` 
1. Set up the RELEASE file
    1. `nano configure/RELEASE`
        1. Fix the "ASYN" line to match your actual file path from above: `ASYN=$(SUPPORT)/asyn`
        1. Comment out the "CALC" and "PCRE" lines
        1. Set the EPICS_BASE variable to point to the right folder for your computer (SUPPORT is already set up OK)
        1. E.g. make the file look like this:
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
1. Set up the architecture-specific RELEASE file, so that it locates the pcre libraries you installed earlier:
    1. `nano configure/RELEASE.Common.${EPICS_HOST_ARCH}` (This will create a new file to edit)
        1. Based on examining the outputs of `whereis pcre` and `whereis libpcre` (see the earlier step where we were installing the PCRE dependency), we give this new file contents that match the path prefixes for our system:
        ```bash
        PCRE_INCLUDE=/usr/include
        PCRE_LIB=/usr/lib
        ```
1. Run `make` (or `make -j4` for faster results).
    
