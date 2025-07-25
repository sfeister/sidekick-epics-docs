# Flash Arduino with SCPI Firmware

This tutorial will guide you through flashing your Arduino with SCPI (Standard Commands for Programmable Instruments) firmware, enabling it to communicate with your EPICS IOC through standardized serial commands.

## Prerequisites

- Completed [Create and Run a Simple EPICS IOC](../create-simple-ioc.md)
- Arduino device (Uno, Nano, or compatible)
- USB cable for Arduino connection
- Computer with Arduino IDE capability

## Required Downloads

First, we need to ensure that our Arduino's are flashed with the correct Arduino files and you must have the Arduino IDE downloaded.

### 1. Arduino SCPI Firmware
Download the Arduino SCPI firmware files from the GitHub repository:
- **Repository**: [Link to GitHub repository here]
- **File needed**: `.ino` file containing the SCPI implementation
- Save this file to a known location on your computer

### 2. Arduino IDE
Download and install the Arduino IDE:
- **Official Download**: [Link to Arduino IDE here]
- Choose the version appropriate for your operating system
- Install following the standard installation process

## Step 1: Setup Arduino IDE and Open Firmware

Once those two are downloaded:

1. **Open Arduino IDE**: Launch the Arduino IDE application
2. **Open SCPI Firmware**: 
   - Open the `.ino` file that you downloaded from the GitHub repository
   - Go to `File` → `Open`
   - Navigate to and select the downloaded `.ino` file
   - The SCPI firmware code should now be displayed in the IDE

## Step 2: Configure Arduino Connection

Once you've done that:

1. **Connect Arduino**: Plug in your Arduino to your computer using a USB cable
2. **Select Arduino in IDE**: 
   - Go to `Tools` → `Board` → `Arduino AVR Boards`
   - Select the type of Arduino it is (e.g., "Arduino Uno", "Arduino Nano")
3. **Select Port**:
   - Go to `Tools` → `Port`
   - Select the port showing your Arduino (typically shows as "Arduino Uno" or similar)

## Step 3: Handle Missing Libraries

Once you've done that you can begin to upload the `.ino` file to the Arduino. Please keep in note you may run into a few errors regarding libraries missing. To fix this:

### Method 1: Library Manager (Recommended)
1. Go to `Tools` → `Manage Libraries...`
2. In the Library Manager search box, search for the missing library name
3. Click "Install" on the appropriate library
4. Repeat for any additional missing libraries

### Method 2: Manual Installation
If libraries aren't available through the Library Manager:
1. Download the required library as a ZIP file
2. Go to `Sketch` → `Include Library` → `Add .ZIP Library...`
3. Select the downloaded ZIP file
4. Restart the Arduino IDE

### Common Required Libraries
The SCPI firmware typically requires:
- **Vrekrer_scpi_parser**: For SCPI command parsing
- **SoftwareSerial**: Usually included with Arduino IDE
- Additional libraries specific to your hardware setup

## Step 4: Compile and Upload Firmware

1. **Verify Code**: Click the checkmark icon (✓) to compile and check for errors
2. **Resolve Any Issues**: 
   - If compilation errors occur, install missing libraries as described above
   - Check that board and port selections are correct
3. **Upload Firmware**: Click the arrow icon (→) to upload the firmware to your Arduino
4. **Monitor Upload**: Watch the status bar for upload progress and completion

## Step 5: Verify Successful Flash

### Check Upload Confirmation
- Look for "Done uploading" message in the IDE status area
- The Arduino's built-in LED may blink during upload

### Test Serial Communication
1. **Open Serial Monitor**: 
   - Go to `Tools` → `Serial Monitor`
   - Set baud rate to match your firmware (typically 9600 or 115200)
2. **Test SCPI Commands**:
   - Type `*IDN?` and press Enter
   - You should receive an identification response from the Arduino
   - Try other basic SCPI commands as defined in your firmware

## Troubleshooting

### Upload Fails
- **Port Issues**: Ensure correct port is selected and Arduino is properly connected
- **Driver Problems**: Install Arduino drivers if port doesn't appear
- **Board Selection**: Verify correct Arduino model is selected

### Compilation Errors
- **Missing Libraries**: Install all required libraries through Library Manager
- **Version Conflicts**: Ensure library versions are compatible
- **Code Issues**: Verify you have the correct `.ino` file version

### No Serial Response
- **Baud Rate**: Check serial monitor baud rate matches firmware setting
- **Connection**: Verify USB cable provides data connection, not just power
- **Firmware Issues**: Try re-uploading the firmware

## Success Confirmation

Your Arduino is successfully flashed when:
- Upload completes without errors
- Serial monitor shows response to `*IDN?` command
- Arduino responds to basic SCPI commands
- No error messages in serial communication

## Next Steps

With your Arduino now running SCPI firmware, you're ready to configure serial communication:

**Next tutorial:** [Configure Serial Port Communication](../arduino-set-up/serial-port-communication.md) - Set up serial communication between your Raspberry Pi and Arduino

This will enable your EPICS IOC to send commands to and receive data from your Arduino device through standardized SCPI protocols.