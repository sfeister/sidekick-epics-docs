# First Steps with a Raspberry Pi
First steps you will take configuring your Raspberry Pi to become a compact EPICS server.

## References
1. [Toms Hardware: Raspberry Pi OS Imager Now Comes with Advanced Options](https://www.tomshardware.com/news/raspberry-pi-imager-now-comes-with-advanced-options)

## Pre-requisites
* Familiarity with the method of [SSH remote connection to networked computers](https://www.startutorial.com/articles/view/ssh-basics-part-1-introduction)
* Administrative login to your wireless/wired router login page (for locating IP addresses of network clients)

## Materials
* Raspberry Pi (e.g. this [Raspberry Pi Model 3 B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/))
* Blank MicroSD card (e.g. this [16 GB SanDisk microSD card](https://www.amazon.com/SanDisk-Ultra-SDSQUNS-016G-GN3MN-UHS-I-microSDHC/dp/B074B4P7KD/ref=sr_1_4?dchild=1&keywords=micro+sd+card+16gb&qid=1634232331&s=electronics&sr=1-4)
* MicroSD card USB reader (e.g. this [Anker USB 3.0 microSD card reader](https://www.raspberrypi.com/software/))

## Steps

### Install and configure Raspberry Pi OS Lite on your microSD card

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

### Boot your Raspberry Pi for the first time

1. Insert your finalized microSD card into your Raspberry Pi.
1. Physically connect your Raspberry Pi to your local area network with an Ethernet cable (or see instructions above for connecting via WiFi).
1. Connect power to your Raspberry Pi. It will turn on. Give it a few minutes to complete its first boot initialization.
    
### Find your Pi on the Network
1. You'll need to locate your Raspberry Pi's IP address on your local area network before you can move to the next step.
1. The simplest way to do this is from your [Wireless/Wired Router's administrative login page](https://www.lifewire.com/accessing-your-router-at-home-818205). From that page, you can see connected devices listed, and within that list, you can locate your Raspberry Pi's IP address.
    1. At this point, it might be nice to assign your Raspberry Pi a fixed IP address from within your Wireless/Wired Router administrative panel. Doing so is outside the scope of this tutorial.
1. A more advanced way to do this is to perform a Network Scan. This technique is outside the scope of our tutorial.

### SSH into your Pi
1. Using your preferred SSH tool, such as [PuTTY](https://www.putty.org/) on Windows, connect with your Raspberry Pi. The username is pi, and the password is as you set in the Raspberry Pi OS Imager settings above.
    1. If you are entirely new to SSH, you may want to follow this tutorial: [How to Connect to an SSH Server from Windows, macOS, or Linux](https://www.howtogeek.com/311287/how-to-connect-to-an-ssh-server-from-windows-macos-or-linux/)
    1. For example, in Linux, you might run: `ssh pi@192.168.202.200`, if your Pi's IP address that you found in the last step were 192.168.202.200. Then, when prompted, you would put in your password that you set in the Raspberry Pi OS Imager step above.
1. If your terminal window displays "pi\@epics1$", you are now successfully in a Linux shell running on the Raspberry Pi. You will use this remote shell to modify your Raspberry Pi and install EPICS.

### Bring the OS fully up-to-date

From your SSH terminal window, you'll need to bring the Raspberry Pi Operating System fully up-to-date, and then install some packages relevant to EPICS. The next few steps are an overview how.

1. Ensure your Raspberry Pi has a working internet connection.
1. (Optional) Set your correct timezone under "Localisation" in the `raspi-config` graphical configuration tool.
1. Bring your Raspberry Pi OS up-to-date:
    `sudo apt -y update`
    `sudo apt -y upgrade` (plan for about fifteen minutes of downloading and installing software upgrades)
1. 



