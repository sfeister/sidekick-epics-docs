# Install EPICS v7 on Raspberry Pi (40 minutes)
By following these instructions, you will build and install EPICS 7 on your Raspberry Pi.

EPICS 7 provides the base infrastructure for EPICS, upon which further EPICS packages like StreamDevice can be built.

## References
1. [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html)

## Pre-requisites
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


Ensure your Raspberry Pi has a working internet connection.

Then, bring your Raspberry Pi OS up-to-date:

```bash
sudo apt -y update
sudo apt -y upgrade
```

Note: The `-y` lets you skip typing "yes" to prompts.

Plan for about fifteen minutes of downloading and installing software upgrades on your first boot.

### Install relevant EPICS dependencies (5 minutes)

Ensure your Raspberry Pi has a working internet connection.

Then, install basic build tools (the *build-essential* package includes key development tools like gcc and perl) and *git* (for package management).

```bash
sudo apt -y install build-essential
sudo apt -y install git
```

#### Optional Checks
(Optional) Install networking tools, including nmap, netstat, and ifconfig:

```bash
sudo apt -y install net-tools
```
    
(Optional) Confirm GNU make is of version 3.81 or higher

```bash
make --version
```
    
What I found installed was "GNU Make 4.2.1" at the time of this tutorial.
    
(Optional) Confirm that perl is version 5.8.1 or higher:

```bash
perl --version
```
    
What I found installed was Perl "v5.28.1" at the time of this tutorial.
    
(Optional) Check that "readline" is installed (it is.)
    
```bash
apt search readline-common
```
    
What I found installed was readline version 7.0-5 at time of writing this tutorial.
    
### Download and install EPICS v7 (30 minutes)
This portion of our instructions are copied nearly directly from the [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html).

#### Download and install
Create an EPICS folder, download the latest repository code, and compile EPICS base from source:
 
```bash
mkdir $HOME/EPICS
cd $HOME/EPICS
git clone --recursive https://github.com/epics-base/epics-base.git
cd epics-base
make -j8
```

(Note: the `make -j8` means to compile EPICS using eight threads, to speed up this step on a multicore machine. A more bulletproof method is to just run `make`, which uses one thread, and may take longer.)

#### Configure your user profile
Append the following environment variable declarations to your the last lines of `.bashrc` file, which is located in your home directory (a.k.a. your `~` directory.) For example, open `~/.bashrc` using the `nano` text editor: `nano ~/.bashrc`, then scroll to the end and add these lines below.

```bash
# EPICS Environment Variables
export EPICS_BASE=${HOME}/EPICS/epics-base
export EPICS_HOST_ARCH=$(${EPICS_BASE}/startup/EpicsHostArch)
export PATH=${EPICS_BASE}/bin/${EPICS_HOST_ARCH}:${PATH}
```
    
The variables aren't yet updated in your system. You have two options to load the variables you just wrote into your `~/.bashrc` file.

1. Option 1: Close the SSH window, and then SSH back into your Pi a second time.
2. Option 2: Run the command `source ~/.bashrc` and skip closing/re-opening your SSH window.

### Step back and tinker!
You can now build local EPICS databases and use commands like "softIoc" and "caget"! Tinker around with these commands for a little while by following the online tutorial ["Test EPICS"](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html#test-epics).

## What's Next?
When you're ready to set up a real device that communicates via USB Serial commands, such as the Arduino setups we've created for the Sidekick System, move along to the next step here! The next step will guide you through installing the EPICS *asyn* and *streamDevice* modules!
