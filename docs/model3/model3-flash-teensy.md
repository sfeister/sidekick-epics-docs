---
layout: default
title: Flashing Teensy Firmware
authors:
    - Scott Feister
---

# Flashing Sidekick Firmware to the Teensy Development Boards

We are using [Teensy 4.0 or Teensy 4.1 development boards](https://www.pjrc.com/teensy/index.html) to mimic real laboratory devices. This requires flashing our custom firmware onto these development boards.

You can flash firmware to the Teensys from Windows, Linux, Mac etc. The process is pretty similar to flashing firmware to an Arduino. I’ll walk through here how to flash this specific firmware to a Teensy 4.0 from Windows.

## Download Sidekick v3 Firmware Source Code

From within the [dolphindaq repository on GitHub](https://github.com/sfeister/dolphindaq), you’ll need the entire folder called “Teensy”, as this contains the source code for all the Sidekick v3 firmwares. You will also need the subfolder "proto". Use [git on Windows](https://git-scm.com/download/win) or equivalent to clone the entire dolphindaq repository to a local folder on your computer.

```bash
git clone https://github.com/sfeister/dolphindaq.git
```


## Download and install TeensyLoader

Install [TeensyLoader](https://www.pjrc.com/teensy/loader.html). This will let you flash HEX files to your Teensy, which is the last step after compiling source code. It also may contain some necessary USB drivers for the Teensy (I’m not sure.)

If all you want to do is flash already-compiled firmware, stop here and use TeensyLoader to do what you want. If you want to compile the firmware from source code, you’ll also want to get the Arduino IDE and its integrations for Teensy.

## Download and Install the Arduino IDE

[Download and install the Arduino IDE](https://www.arduino.cc/en/software) (follow the link). I downloaded the “MSI installer” for the latest version, Version 2.3.2. Don’t use any version less than 2.0 as the instructions would be different.


## Install Teensy Board Package for the Arduino IDE

Install Teensy into the Arduino IDE. Documentation below adapted from the source: [Teensyduino](https://www.pjrc.com/teensy/td_download.html)

Open the Arduino IDE v2.0+

Click File > Preferences (on MacOS, click Arduino IDE > Settings).


As shown in the screenshot below: In the text box called "Additional boards manager URLs", paste the following: https://www.pjrc.com/teensy/package_teensy_index.json

![Additional boards manager](https://github.com/user-attachments/assets/752baafc-3120-468b-b8c3-fd5825a7ada4)

Then, click “Ok.”


As shown in the screenshot below: In the main Arduino window, open Boards Manager by clicking the left-side board icon.

![Open Boards Manager](https://github.com/user-attachments/assets/2b74beb4-bdea-421e-bd87-015f9df967d0)

As shown in the screenshot below, within the boards manager, search for "teensy", and click "Install" to install “Teensy by Paul Stroffregon.”

![Teensyduino Install](https://github.com/user-attachments/assets/7f26d13d-0dd6-4518-867a-9a37b68b5a20)

Although the screenshot above shows an older version of Teensy by Paul Stroffregen, I am using the latest version (1.59.0).


## Install Third-Party Libraries (Sidekick v3 Dependencies) into the Arduino IDE

### Third-Party Libraries from Library Manager
As shown in the screen shot below: In the main Arduino window, open Library manager by click the left-side books icon.

![Open Library Manager](https://github.com/user-attachments/assets/385b28ff-4aac-4c73-9645-39d74fa97221)

From the Library Manager, search for and install the following packages:

1. **Chrono **by Thomas O. Fredricks (I had the latest version, 1.2.0 installed)
2. **SCPI_Parser **by Jan Breuer (I had the latest version, 2.2.0 installed)
3. **TeensyTimerTool **by luni64. (I had the latest version, 1.4.1 installed)

### Third-Party Libraries from Source Code

The other sketches may require two other libraries which are not accesible through the library manager, so you'll need to install them yourself by-hand. This involves downloading library folders and copying them into the right local folder.

ADC is the entire repository folder of [https://github.com/pedvide/ADC](https://github.com/pedvide/ADC)

ddaqproto folder is the “ddaqproto” folder in dolphindaq repository at [dolphindaq]/proto/compiled_arduino/

Copy the folders “ddaqproto” and “ADC” to the following libraries folder:

1. Windows: C:\Users\{username}\Documents\Arduino\libraries
2. macOS: /Users/{username}/Documents/Arduino/libraries
3. Linux: /home/{username}/Arduino/libraries

## Compile Firmware for PulseGenerator

We’ll start off by compiling and flashing the firmware that will run the system pulse generator in the Sidekick v3.

As shown in the screenshot below, from the “File → Open” menu of Arduino IDE, navigate into the “Teensy” folder of the dolphindaq repository (which you just cloned to your local PC).

![Teensy Folder on Windows](https://github.com/user-attachments/assets/60307d23-fa4f-4ff6-8ac4-e5686195d6b4)

Then navigate into the firmware subfolder for the device you wish to flash: in our case for this device, we want the PulseGeneratorSerial.

![PulseGeneratorSerial Folder on Windows](https://github.com/user-attachments/assets/13d8242f-5deb-4c43-affb-e38d018464b3)

Select the “PulseGeneratorSerial.ino” file to open the source code in the Arduino IDE, as shown below.

![PulseGeneratorSerial Sketch File](https://github.com/user-attachments/assets/67f9ffb1-5a41-402a-9ab4-4791136faedc)

Your Arduino IDE should pop open and now look something like this:

![PulseGeneratorSerial Open in IDE](https://github.com/user-attachments/assets/7b7e4955-1855-4b41-8b24-6e4dc2df0152)

Notice the tabs to right of PulseGeneratorSerial.ino are the other files in the same PulseGeneratorSerial folder. Those .h and .cpp files are also used in compililng this firmware.

To help with troubleshooting, you may wish to adjust the Arduino IDE settings for verbose output during compiling.

![Verbose Output](https://github.com/user-attachments/assets/81de5d93-5510-4c30-af36-cea968773638)

Plug in the Teensy 4.0/4.1 into your computer. As shown in the screenshot below, you should now be able to select it from the dropdown menu.

![Teensy USB COM Ports](https://github.com/user-attachments/assets/f20083c0-4b83-469d-926f-86428aed2499)

Do a test compile to make sure everything works right. You can compile the code (without flashing it to the Teensy) by clicking “Verify”.

![Verify Button Arduino IDE](https://github.com/user-attachments/assets/3f8f5c6e-828b-4361-b9c6-5da2df40bda4)

A successful compile will take a few minutes and then end with a message such as this:

![Successful Compile Output](https://github.com/user-attachments/assets/19d92129-96f1-433c-9b10-7f5d61b4b1e3)

## Flash Firmware for PulseGenerator
When you are ready to flash the firmware instead of just verifying the compile, select "Run" in the Arduino IDE.

## Compile and Flash Other Sketches
You should now have the toolchain to compile and flash any firmware for the Sidekick Model 3.
