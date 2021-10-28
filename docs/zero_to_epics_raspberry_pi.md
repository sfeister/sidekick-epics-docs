# First Steps with a Raspberry Pi

First steps you will take configuring your Raspberry Pi to become a compact EPICS server. I tested this tutorial on the Raspberry Pi Model 3 B+.

## References
1. [Toms Hardware: Raspberry Pi OS Imager Now Comes with Advanced Options](https://www.tomshardware.com/news/raspberry-pi-imager-now-comes-with-advanced-options)
1. [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html)
1. [StreamDevice setup guide](https://paulscherrerinstitute.github.io/StreamDevice/setup.html)

## Pre-requisites
* Familiarity with the method of [SSH remote connection to networked computers](https://www.startutorial.com/articles/view/ssh-basics-part-1-introduction)
* Administrative login to your wireless/wired router login page (for locating IP addresses of network clients)

## Materials
* Raspberry Pi (e.g. this [Raspberry Pi Model 3 B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/))
* Blank MicroSD card (e.g. this [16 GB SanDisk microSD card](https://www.amazon.com/SanDisk-Ultra-SDSQUNS-016G-GN3MN-UHS-I-microSDHC/dp/B074B4P7KD/ref=sr_1_4?dchild=1&keywords=micro+sd+card+16gb&qid=1634232331&s=electronics&sr=1-4)
* MicroSD card USB reader (e.g. this [Anker USB 3.0 microSD card reader](https://www.raspberrypi.com/software/))

## Steps

### Install and configure Raspberry Pi OS Lite on your microSD card (10 minutes)

1. Download and install the [Raspberry Pi OS imager](https://www.raspberrypi.com/software/) onto your laptop. I used v1.6.2.
1. Plug your blank microSD card into your laptop using your USB microSD card reader.
1. Open the Raspberry Pi OS Imager on your laptop.
1. In Raspberry Pi OS Imager:
    1. Click the "Operating System" box, then navigate to "Raspberry Pi OS (other)", and select "Raspberry Pi OS Lite" (a port of Debian with no desktop environment).
        1. I chose the Lite version to increase performance by omitting a desktop environment, but you could use any version.
        1. When I wrote this tutorial, the Raspberry Pi OS Lite version I used was at "2021-05-07". You can use the latest version, which loads by default.
    1. Click the "Storage" box, and select your microSD card.
    1. Do NOT click "Write" yet! Instead, press "CTRL + SHIFT + X" to open the "Advanced options" window.
    1. From the "Advanced options" window:
        1. Check the "Set hostname" box and change from "raspberrypi.local" to "epics1.local" (or another unique hostname of your choosing). This is to avoid all of your pis having the same exact hostname.
        1. Check the "Enable SSH" box and then write a password of your choosing. This will enable us to connect to our Raspberry Pi from a laptop on the local area network, without any display, keyboard, or mouse.
            1. Advanced SSH Users: Alternatively to choosing a password, you can select the public key authorization option and paste in your public key.
        1. Press the "Save" button.
    1. Finally, from the main window, press the "Write" button. Note that this will erase anything already on your microSD card.
    1. Wait for the "Writing" progress bar to complete. A window will pop up letting you know it's safe to remove your microSD card now.
1. Remove your microSD card.
1. If you plan to connect your Pi to the local area network with WiFi rather than Ethernet, you'll need to plug the microSD card back, navigate to the "boot" directory, and create a special file called "wpa_supplicant.conf". You can follow these [instructions for writing and copying the wpa_supplicant.conf file](https://linuxhint.com/rasperberry_pi_wifi_wpa_supplicant/).

### Boot your Raspberry Pi for the first time (10 minutes)

1. Insert your finalized microSD card into your Raspberry Pi.
1. Physically connect your Raspberry Pi to your local area network with an Ethernet cable (or see instructions above for connecting via WiFi).
1. Connect power to your Raspberry Pi. It will turn on. Give it a few minutes to complete its first boot initialization.
    
### Find your Pi on the Network (5 minutes)
1. You'll need to locate your Raspberry Pi's IP address on your local area network before you can move to the next step.
1. The simplest way to do this is from your [Wireless/Wired Router's administrative login page](https://www.lifewire.com/accessing-your-router-at-home-818205). From that page, you can see connected devices listed, and within that list, you can locate your Raspberry Pi's IP address.
    1. At this point, it might be nice to assign your Raspberry Pi a fixed IP address from within your Wireless/Wired Router administrative panel. Doing so is outside the scope of this tutorial.
1. A more advanced way to do this is to perform a Network Scan. This technique is outside the scope of our tutorial.

### SSH into your Pi (5 minutes)
1. Using your preferred SSH tool, such as [PuTTY](https://www.putty.org/) on Windows, connect with your Raspberry Pi. The username is pi, and the password is as you set in the Raspberry Pi OS Imager settings above.
    1. If you are entirely new to SSH, you may want to follow this tutorial: [How to Connect to an SSH Server from Windows, macOS, or Linux](https://www.howtogeek.com/311287/how-to-connect-to-an-ssh-server-from-windows-macos-or-linux/)
    1. For example, in Linux, you might run: `ssh pi@192.168.202.200`, if your Pi's IP address that you found in the last step were 192.168.202.200. Then, when prompted, you would put in your password that you set in the Raspberry Pi OS Imager step above.
1. If your terminal window displays "pi\@epics1$", you are now successfully in a Linux shell running on the Raspberry Pi. You will use this remote shell to modify your Raspberry Pi and install EPICS.

### Bring the OS fully up-to-date (15 minutes)

From your SSH terminal window, bring all software on the Raspberry Pi fully up-to-date. This is best practice before installing required dependencies. Here's how:

1. Ensure your Raspberry Pi has a working internet connection.
1. (Optional) Set your correct timezone under "Localisation" in the `raspi-config` graphical configuration tool.
1. Bring your Raspberry Pi OS up-to-date:
    `sudo apt -y update`
    `sudo apt -y upgrade` (plan for about fifteen minutes of downloading and installing software upgrades)

### Install relevant EPICS dependencies (5 minutes)

1. Ensure your Raspberry Pi has a working internet connection.
1. Install basic build tools (the *build-essential* package includes key development tools like gcc and perl)
    `sudo apt -y install build-essential`
1. Install git
    `sudo apt -y install git`
1. (Optional) Install networking tools, including nmap, netstat, and ifconfig
    `sudo apt -y install net-tools`
1. (Optional) Confirm GNU make is of version 3.81 or higher
    `make --version`
    a. What I found installed was "GNU Make 4.2.1" at the time of this tutorial.
1. (Optional) Confirm that perl is version 5.8.1 or higher
    `perl --version`
    a. What I found installed was Perl "v5.28.1" at the time of this tutorial.
1. (Optional) Check that "readline" is installed (it is.)
    a. (EPICS installation README mentions using readline)
    `apt search readline-common`
    b. What I found installed was readline version 7.0-5 at time of writing this tutorial.
    
### Download and install EPICS v7 (30 minutes)
This portion of our instructions are copied nearly directly from the [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html).

1. Create an EPICS folder, download the latest repository code, and compile EPICS base from source:
    ```
    mkdir $HOME/EPICS
    cd $HOME/EPICS
    git clone --recursive https://github.com/epics-base/epics-base.git
    cd epics-base
    make -j4
    ```
    (Note: the `make -j4` means to compile EPICS using eight threads, to speed up the process. A more bulletproof method is to just run `make`, which uses one thread, and may take longer. I'm not sure if the -j4 helped; this step still took me about thirty minutes on a Raspberry Pi Model 3 B+ and even froze up at one point; I had to restart it.)
1. Append the following environment variable declarations to your the last lines of your ~/.bashrc file. For example, edit this file via `nano ~/.bashrc`, then scroll to the end and add these lines below.
    ```
    # EPICS Environment Variables
    export EPICS_BASE=${HOME}/EPICS/epics-base
    export EPICS_HOST_ARCH=$(${EPICS_BASE}/startup/EpicsHostArch)
    export PATH=${EPICS_BASE}/bin/${EPICS_HOST_ARCH}:${PATH}
    ```
1. The variables aren't yet updated in your system. You have two options to load the variables you just wrote into your ~/.bashrc file.
    1. Option 1: Close the SSH window, and then SSH back into your Pi a second time.
    2. Option 2: Run the command `source ~/.bashrc` and skip closing/re-opening your SSH window.
1. You can now build local EPICS databases and use commands like "softIoc" and "caget"! Tinker around with these commands for a little while by following the online tutorial ["Test EPICS"](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html#test-epics).
1. When you're ready to set up a real device that communicates via USB Serial commands, such as the Arduino setups we've created for the Sidekick System, move along to the next step here! The next step will guide you through installing the EPICS *asyn* and *streamDevice* modules!

### Install StreamDevice Module for serial device communication

#### Install dependencies for StreamDevice (10 minutes)
1. Install PCRE packages
    a. `sudo apt install -y libpcre3 libpcre3-dev`
        i. Note: libpcre3 (runtime files) is probably already installed, but libpcre3-dev (include files, etc) is probably not.
    b. (Optional) Check that "/usr/include/" now contains header files for PCRE, such as "pcre.h", and that "/usr/lib/x86_64-linux-gnu/" now contains files such as "libpcre.so"
        i. Go check out package details for libpcre3 and libpcre3-dev and see where items went (see references for package lists, then go to "list files" under your architecture)
        ii. Or:
            1) `whereis pcre`
                a) Returns: `pcre: /usr/include/pcre.h /usr/share/man/man3/pcre.3.gz`
            2) `whereis libpcre`
                a) Returns: `libpcre: /usr/lib/arm-linux-gnueabihf/libpcre.a /usr/lib/arm-linux-gnueabihf/libpcre32.so /usr/lib/arm-linux-gnueabihf/libpcre.so /usr/lib/arm-linux-gnueabihf/libpcre32.a /usr/lib/arm-linux-gnueabihf/libpcre16.a /usr/lib/arm-linux-gnueabihf/libpcre16.so`
1. Compile and install asynDriver module, which is a pre-requisite for stream
    a. Navigate into the directory you made to hold EPICS items, into which you cloned the epics-base repository, and create a new folder to hold support items for EPICS base (e.g. additional modules).
        i. `cd $HOME/EPICS`
        ii. `mkdir support`
        iii. `cd support`
    b. Download asynDriver module source code and navigate into the folder
        i. `git clone https://github.com/epics-modules/asyn.git`
        ii. `cd asyn`
    c. Set up the RELEASE file
        i. `nano configure/RELEASE`
            1) Comment out unneeded lines IPAC, SEQ, CALC, SSCAN, etc.
            2) Set the SUPPORT and EPICS_BASE variables to point to the right folders for your computer
            3) E.g. make the file look like this:
                ```
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
            4) `make` (took me about five minutes)
#### Compile and install StreamDevice
1. Compile and install StreamDevice module
    a. Navigate back into the directory you made to hold EPICS support items.
        i. `cd $HOME/EPICS/support`
    b. Download StreamDevice module source code and navigate into the folder
        i. `git clone https://github.com/paulscherrerinstitute/StreamDevice.git`
        i. `cd StreamDevice` 
    c. Set up the RELEASE file
        i. `nano configure/RELEASE`
            1) Fix the "ASYN" line to match your actual file path from above: `ASYN=$(SUPPORT)/asyn`
            1) Comment out the "CALC" and "PCRE" lines
            2) Set the EPICS_BASE variable to point to the right folder for your computer (SUPPORT is already set up OK)
            3) E.g. make the file look like this:
                ```
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
    a. Set up the architecture-specific RELEASE file, so that it locates the pcre libraries you installed earlier:
        i. `nano configure/RELEASE.Common.${EPICS_HOST_ARCH}`
            i. Based on the outputs of `whereis pcre` and `whereis libpcre`, we give this new file these contents:
            ```
            PCRE_INCLUDE=/usr/include
            PCRE_LIB=/usr/lib
            ```
    a. Run `make`.
    


