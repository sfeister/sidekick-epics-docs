# Install EPICS v7 on Raspberry Pi (40 minutes)
By following these instructions, you will build and install EPICS 7 on your Raspberry Pi.

EPICS 7 provides the base infrastructure for EPICS, upon which further EPICS packages like StreamDevice can be built.

## References
1. [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html)

## Pre-requisites
* EPICS v7 is already installed on your Raspberry Pi, per prior instructions
* Capability to SSH into your Raspberry Pi
* Working internet connection for your Raspberry Pi

## Materials
* Local area network
* Laptop / computer, connected to local area network
* Raspberry Pi, connected to local area network

## Steps
### SSH into your Raspberry Pi

Follow the prior instructions for this.

### Bring the OS fully up-to-date (15 minutes)

From your SSH terminal window, bring all software on the Raspberry Pi fully up-to-date. This is best practice before installing required dependencies. Here's how:

1. Ensure your Raspberry Pi has a working internet connection.
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
