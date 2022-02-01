## Install and configure Raspberry Pi OS Lite on your microSD card (10 minutes)
In this tutorial, you will flash Raspberry Pi OS Lite on your microSD card in such a way that you can remotely connect to the machine via SSH.

## Materials
* Raspberry Pi (e.g. this [Raspberry Pi Model 3 B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/))
* Blank MicroSD card (e.g. this [16 GB SanDisk microSD card](https://www.amazon.com/SanDisk-Ultra-SDSQUNS-016G-GN3MN-UHS-I-microSDHC/dp/B074B4P7KD/ref=sr_1_4?dchild=1&keywords=micro+sd+card+16gb&qid=1634232331&s=electronics&sr=1-4)
* MicroSD card USB reader (e.g. this [Anker USB 3.0 microSD card reader](https://www.raspberrypi.com/software/))

## Steps
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
