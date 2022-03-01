# Install and configure Raspberry Pi OS Lite on your microSD card (10 minutes)
In this tutorial, you will flash Raspberry Pi OS Lite on your microSD card in such a way that you can remotely connect to the machine via SSH. This tutorial assumes you will connect the Raspberry Pi to your local network using an Ethernet cable. Instructions for connecting via wifi are linked to, but not described in detail, towards the end.

## Why Pi OS Lite?
We chose Raspberry Pi OS Lite because it has lower installation size than the Raspberry Pi OS. Since we won't be using any of the Desktop elements of our Raspberry Pi, but will be connecting remotely, we don't need the "extras". This makes it a nice, clean foundation for our EPICS goals.

## References
1. [Toms Hardware: Raspberry Pi OS Imager Now Comes with Advanced Options](https://www.tomshardware.com/news/raspberry-pi-imager-now-comes-with-advanced-options)

## Materials
* Raspberry Pi (e.g. this [Raspberry Pi Model 3 B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/))
* Blank MicroSD card (e.g. this [16 GB SanDisk microSD card](https://www.amazon.com/SanDisk-Ultra-SDSQUNS-016G-GN3MN-UHS-I-microSDHC/dp/B074B4P7KD/ref=sr_1_4?dchild=1&keywords=micro+sd+card+16gb&qid=1634232331&s=electronics&sr=1-4)
* MicroSD card USB reader (e.g. this [Anker USB 3.0 microSD card reader](https://www.raspberrypi.com/software/))
* Personal computer

## Steps
### Plug in your SD Card
Plug your blank microSD card into your personal computer using your USB microSD card reader.
 
### Download and Open Raspberry Pi OS Imager
Download the installer for the [Raspberry Pi OS imager](https://www.raspberrypi.com/software/) onto your laptop.

I used v1.7.1. Once it's downloaded, install the software.

### Configure Basic Settings
Open the Raspberry Pi OS Imager software on your personal computer. You will complete the next several steps from within Raspberry Pi OS Imager.

From within the Raspberry Pi OS Imager software, click the "Operating System / CHOOSE OS" box, then navigate to "Raspberry Pi OS (other)", and select "Raspberry Pi OS Lite" (a port of Debian with no desktop environment).

![image](https://user-images.githubusercontent.com/7269185/156225778-221f98dd-bbf5-41b3-9d06-3780e2b0556e.png)

Notes:

1. I chose the Lite version to increase performance by omitting a desktop environment, but you could use any version.
1. When I wrote this tutorial, the Raspberry Pi OS Lite version I used was at "2021-05-07". You can use the latest version, which loads by default.

Back at the main screen of the Raspberry Pi OS imager software, click the "Storage / CHOOSE STORAGE" box, and select your microSD card.

![image](https://user-images.githubusercontent.com/7269185/156225884-8cfe6c37-75a6-4db5-8647-c71a3342bc47.png)

Do NOT click "Write" yet! Instead, press "CTRL + SHIFT + X" or click the gears icon to open the "Advanced options" window.

![image](https://user-images.githubusercontent.com/7269185/156225956-4622466f-6a61-42c9-b482-58f3e0b8418e.png)

### Configure Advanced Options (Required)
From the "Advanced options" window that opened when you pressed "CTRL + SHIFT + X" or pressed the gears icon, configure the following. (Note, you will need to scroll down in the Advanced Options window or resize the window in order to see all these settings.)

Check the "Set hostname" box and change from "raspberrypi.local" to "epics1.local" (or another unique hostname of your choosing). This is to avoid all of your pis having the same exact hostname.

Check the "Enable SSH" box and then write a password of your choosing. This will enable us to connect to our Raspberry Pi from a laptop on the local area network, without any display, keyboard, or mouse.
    1. Advanced SSH Users: Alternatively to choosing a password, you can select the public key authorization option and paste in your public key.

Optionally, configure your wifi network settings.

![image](https://user-images.githubusercontent.com/7269185/156226766-8c914875-aa89-4ba0-bbaf-2ccd396521b5.png)

Now that you've configured your advanced options, press the "Save" button.

### Write the SD Card
Finally, from the main window, press the "Write" button. Note that this will erase anything already on your microSD card.

Wait for the "Writing" progress bar to complete. A window will pop up letting you know it's safe to remove your microSD card now.

### Remove SD Card
Remove your microSD card.

### Connecting via WiFi? Extra Note
If you plan to connect your Pi to the local area network with WiFi rather than Ethernet, you can configure those settings prior to writing your SD card, from the same "Advanced Options" menu. Or alternatively, you can to plug the microSD card back after writing, navigate to the "boot" directory, and create a special file called "wpa_supplicant.conf". You can follow these [instructions for writing and copying the wpa_supplicant.conf file](https://linuxhint.com/rasperberry_pi_wifi_wpa_supplicant/).
