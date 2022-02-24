
# Analogy between Sidekick Elements and Laser Laboratory

## Trigger Signals for Lasers and Diagnostics

In high-intensity laser laboratories, trigger cables fan out from a pulse generator (or several pulse generators) to all elements of the laser system and the experimental diagnostics. Correct trigger timing is essential for everything from flashing the laser diodes to opening the electronic shutter of a detector. Many of these system elements require independent timing signals; for example, we want the laser amplifier delay to be different from the camera trigger delay.

We've attempted to replicate this general idea in the sidekick system. We have programmed an Arduino to serve as a low-quality, USB-controlled trigger pulse generator for the other elements of the sidekick system. Just like in a real laser laboratory, this Arduino pulse generator outputs up to eight independently delayed trigger signals over BNC cables.

| Feature      | Arduino Pulse Generator in the Sidekick System | BNC Model 575 Pulse Generator in a Laser Lab |
| ----------- | ----------- | ----------- | 
| Pulse and Delay Resolution: | ~ 1 ms | ~ 250 ps |
| Typical TTL pulse width | 100 us | 1 us |
| Trigger Outputs | 8x Independent BNC Outputs | 8x Independent BNC Outputs |
| System Control | USB via Serial Commands | Ethernet or USB via Serial Commands |
| Cost | ~$20 | ~$5000 |

## Pulsed Light Source

High-intensity lasers are created through a series of amplification stages. Each stage has controls and idiosynchrosies which affect the final laser parameters -- such as energy, spectrum, and duration -- in a non-linear fashion. The amplification stages rely on timing signals from the pulse generator.

In the sidekick system, we've attempted to capture some small element of this complexity. We've created a light source that consists of six separate pulsed LEDs. Each LED has an independent delay and and independent pulse duration. The LED system is triggered from a BNC cable running from the pulse generator.

| Feature      | Arduino Triggered LEDs in the Sidekick System | Triggered Laser Source in a Laser Lab |
| ----------- | ----------- | ----------- | 
| Light Source | 6X independently timed and delayed LED flashes | Amplified Laser Beam |
| Example Pulse Duration | 5 ms | 500 fs |
| Pulse Duration | Controllable | Controllable |
| Trigger Inputs | BNC Cables from Pulse Generator | BNC Cables from Pulse Generator |
| System Control | USB controlled via Serial Commands | Varies; Ethernet and USB via Serial Commands |
| Acquisition Cost | ~$20 | $1 million - $100 million |
| Footprint | Postcard | Multiple rooms |

## Triggered Diagnostics
Inside the laser amplification stages, the laser itself is characterized with diagnostics such as cameras and photodiodes. After high-intensity lasers interact with matter and create plasmas. Resultant plasmas and particle beams are characterized through experimental diagnostics such as cameras, photodiodes, magnetic field probes, particle spectrometers, etc.

One of just a few major drivers for upgrading our current control systems at real laser facilities, which are often hodgepodge, into a unified platform like EPICS is to enable closing the control loop between the diagnostic data and the control systems. In order to create the possibility of closed loop operation, we included a simple optical diagnostic in the sidekick system.

| Feature      | Triggered Phototransistor Diagnostic in the Sidekick System | Triggered Experimental / Laser Diagnostic in a Laser Lab |
| ----------- | ----------- | ----------- | 
| System Control | USB via Serial Commands | Ethernet or USB via Serial Commands |
| Relevant Controls | Exposure Time | Varies |
| External Trigger | Yes, via BNC input | Yes, via BNC input |
| Data Acquisition | USB via Serial Messages | Ethernet or USB via Serial Messages |
| Data Format | Single-shot data | Single-shot data |
| Closed-Loop Operation Possible? | Yes, signal responds to changes in light source | Yes, signal responds to changes in light source |
| Closed-Loop Complexity | Simple (room for improvement here!) | Very Non-Linear |
| Cost | ~$20 | Varies, $200 - $200K |
