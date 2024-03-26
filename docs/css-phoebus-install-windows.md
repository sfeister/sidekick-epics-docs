---
layout: default
title: Install CS-Studio (Phoebus) on Windows
authors:
    - Scott Feister
---

# Install CS-Studio (Phoebus) on Windows
Install EPICS-compatible software for creating graphical control panels onto a Windows 7, Windows 10, or Windows 11 PC.

If you use Linux/Mac, find this outdated, or need more help, see the [official installation documentation](https://controlssoftware.sns.ornl.gov/css_phoebus/).

## References
1. [CS-Studio / Phoebus Download](https://controlssoftware.sns.ornl.gov/css_phoebus/)
1. [CS-Studio / Phoebus Documentation](https://control-system-studio.readthedocs.io/en/latest/)
1. [CS-Studio / Phoebus Official Github page (for developers)](https://github.com/ControlSystemStudio/phoebus)
1. [EPICS Tech-talk discussion on CS-Studio vs. CS-Studio Phoebus](https://epics.anl.gov/tech-talk/2021/msg01803.php)
2. [OpenJDK Builds by Microsoft](https://learn.microsoft.com/en-us/java/openjdk/install)

## Background
There are many, many approaches in the EPICS community to making graphical control panel interfaces. After doing some research, I recommend CS-Studio (Phoebus) as a good entry point. It is well-supported in the community and works with both PVAccess (PVA) and Channel Access (CA) protocols.

This tutorial will walk you through installing the CS-Studio (Phoebus) software on Windows. The process is to first installing OpenJDK, then install CS-Studio (Phoebus). The examples here are with Windows 10. Everything here should be very similar for Windows 7 / 10 / 11.

## Steps
### Install OpenJDK 21
CS-Studio (Phoebus) requires JDK, and they recommend OpenJDK. I downloaded the MSI version of OpenJDK 21 from Microsoft.

Download [OpenJDK 21 from Microsoft](https://learn.microsoft.com/en-us/java/openjdk/download). Pick the **MSI version** of the download.

Double-click the downloaded *.msi file to install OpenJDK 21. Default settings are fine; note that the Java binaries folder does need to be added to the PATH variable (which happens by default).

Now that installation is complete, check your work. Open a Powershell window and run `java --version` to confirm that java from OpenJDK 21 is on the PATH variable. If another version of Java is showing here, you'll need to adjust your system environment variables PATH settings to prioritize OpenJDK 21 (which is outside the scope of this tutorial). Here's what I see:

```powershell
PS> java --version

openjdk 21.0.2 2024-01-16 LTS
OpenJDK Runtime Environment Microsoft-8905927 (build 21.0.2+13-LTS)
OpenJDK 64-Bit Server VM Microsoft-8905927 (build 21.0.2+13-LTS, mixed mode, sharing)
```

If you get output similar to the above, you're ready to move onto installing CS-Studio (Phoebus).

### Manually Install CS-Studio (Phoebus)
Unfortunately, CS-Studio (Phoebus) doesn't include an automated installer -- so we'll download a zip file and then put its contents into a proper location ourselves.

#### Download and Transfer the Zip File Contents

Download the zip file for Windows from [CS-Studio / Phoebus Download](https://controlssoftware.sns.ornl.gov/css_phoebus/).

Unzip the contents into a temporary folder on your computer, which for me made a folder called "phoebus-4.7.3-SNAPSHOT". Make note of the CS-Studio (Phoebus) version number - mine was 4.7.3.

Create a new folder in C:\Program Files called "CSS Phoebus 4.7.3".
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/f1750213-6908-427e-8f69-58459fcab785.png" width=50% height=50% />

Cut and paste the full contents of the file folder "phoebus-4.7.3-SNAPSHOT" into this new folder ("C:\Program Files\CSS Phoebus 4.7.3").
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/99a5661c-7b2f-40fc-8431-b5c368f706ab.png" width=50% height=50% />

#### Create Desktop and Start Menu shortcuts
Since we managed our own installation of the zip file contents, we're also on the hook for setting up our Desktop and Start Menu shortcuts.

Right click "phoebus.bat" and create a shortcut for it on your desktop.
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/8a90b012-e908-4876-aa4e-0bd3f3f50e2d.png" width=50% height=50% />

On your desktop, rename the shortcut to "CS-Studio (Phoebus) 4.7.3"
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/8a631d9c-caad-4b73-baa2-c3ee78370745.png" width=25% height=25% />

Do Ctrl + R (Run) and then enter "%AppData%\Microsoft\Windows\Start Menu\Programs". This will open up a folder for you relating to your Start Menu applications.
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/1707ec51-c6a5-420f-9c4d-89a88ea80eec.png" width=50% height=50% />

Copy your desktop shortcut into that folder. This will put it into the Start Menu list.
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/676facc7-b9d7-4f4a-8e66-6b88f4c58ed4.png" width=50% height=50% />

### Check everything works!

You can now start CS-Studio from the start menu.
<br /><img src="https://github.com/sfeister/sidekick-epics-docs/assets/7269185/112dfb31-dd83-4ea4-9c1b-42a3986cc5f6.png" width=25% height=25% />

			
