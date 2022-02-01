# First boot and SSH into your Raspberry Pi (35 minutes)
You will insert the microSD card you just flashed with Raspberry Pi OS Lite, boot it, SSH into it, and bring it fully up-to-date.

## Pre-requisites
* Completion of the tutorial in which you flashed your microSD card for your Raspberry Pi.
* Familiarity with the method of [SSH remote connection to networked computers](https://www.startutorial.com/articles/view/ssh-basics-part-1-introduction)
* Administrative login to your wireless/wired router login page (for locating IP addresses of network clients)

## Materials
* Raspberry Pi
* Flashed microSD card from prior instructions
* Ethernet cable
* Wired or wireless router

## Steps
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

    a. `sudo apt -y update`

    b. `sudo apt -y upgrade` (plan for about fifteen minutes of downloading and installing software upgrades)
