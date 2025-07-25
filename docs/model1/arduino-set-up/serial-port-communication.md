# Configure Serial Port Communication

This tutorial shows you how to set up serial communication between your Raspberry Pi EPICS IOC and your Arduino with SCPI firmware, enabling command and data exchange between the systems.

## Prerequisites

- Completed [Flash Arduino with SCPI Firmware](../arduino-scpi-firmware.md)
- Arduino running SCPI firmware and responding to `*IDN?` commands
- EPICS IOC environment set up on Raspberry Pi
- ASYN and StreamDevice modules installed
- USB cable connecting Arduino to Raspberry Pi

## Overview

The communication setup involves:
1. **Physical Connection**: USB cable between Arduino and Raspberry Pi
2. **Serial Port Configuration**: Setting up the Linux serial port
3. **ASYN Driver Setup**: Configuring EPICS ASYN for serial communication
4. **StreamDevice Protocol**: Creating protocol files for SCPI commands
5. **Database Records**: Setting up EPICS database records for device interaction

## Step 1: Identify Serial Port

### Connect Arduino and Find Port
1. **Connect Arduino**: Plug Arduino into Raspberry Pi via USB
2. **Check Available Ports**: 
   ```bash
   ls /dev/tty*
   ```
   Look for devices like `/dev/ttyUSB0`, `/dev/ttyACM0`, or similar
3. **Verify Arduino Connection**:
   ```bash
   dmesg | tail
   ```
   Should show USB device connection messages

### Test Serial Communication
1. **Install Serial Tools** (if not already installed):
   ```bash
   sudo apt-get install screen minicom
   ```
2. **Test Direct Communication**:
   ```bash
   screen /dev/ttyUSB0 9600
   ```
   - Type `*IDN?` and press Enter
   - You should see Arduino's identification response
   - Exit screen with `Ctrl+A` then `K`

## Step 2: Configure EPICS ASYN Serial Port

### Create Serial Port Configuration
In your EPICS IOC startup script (typically `st.cmd`), add the serial port configuration:

```bash
################################################################################
# Serial Port Configuration for Arduino SCPI
################################################################################

# Configure serial port - adjust device path as needed
drvAsynSerialPortConfigure("ARDUINO", "/dev/ttyUSB0", 0, 0, 0)

# Set serial communication parameters
asynSetOption("ARDUINO", -1, "baud", "9600")
asynSetOption("ARDUINO", -1, "bits", "8") 
asynSetOption("ARDUINO", -1, "parity", "none")
asynSetOption("ARDUINO", -1, "stop", "1")
asynSetOption("ARDUINO", -1, "clocal", "Y")
asynSetOption("ARDUINO", -1, "crtscts", "N")

# Set input/output terminators
asynOctetSetInputEos("ARDUINO", -1, "\n")
asynOctetSetOutputEos("ARDUINO", -1, "\n")

# Enable communication tracing (optional - for debugging)
asynSetTraceIOMask("ARDUINO", -1, 0x2)
asynSetTraceMask("ARDUINO", -1, 0x9)
```

### Configuration Parameters Explained
- **Port Name**: `"ARDUINO"` - logical name for your serial port
- **Device Path**: `"/dev/ttyUSB0"` - physical serial device (adjust as needed)
- **Baud Rate**: `"9600"` - must match Arduino firmware settings
- **Data Bits**: `"8"` - standard for most serial communication
- **Parity**: `"none"` - no parity checking
- **Stop Bits**: `"1"` - single stop bit
- **Flow Control**: `"crtscts", "N"` - no hardware flow control
- **Terminators**: `"\n"` - newline characters to mark end of messages

## Step 3: Create StreamDevice Protocol File

### Create Protocol File
Create a file named `arduino_scpi.proto` in your IOC's `db/` directory:

```
################################################################################
# Arduino SCPI Protocol File
# File: arduino_scpi.proto
################################################################################

# Terminator for all commands
Terminator = "\n";

# Get identification string
getIDN {
    out "*IDN?";
    in "%39c";
    ExtraInput = Ignore;
}

# Generic digital output control
setDigitalOut {
    out "OUTP:DIG %d,%d";
    @init { getDigitalOut; }
}

# Read digital output status  
getDigitalOut {
    out "OUTP:DIG? %d";
    in "%d";
    ExtraInput = Ignore;
}

# Set analog output voltage
setAnalogOut {
    out "SOUR:VOLT %f,%d";
    @init { getAnalogOut; }
}

# Read analog output voltage
getAnalogOut {
    out "SOUR:VOLT? %d";
    in "%f";
    ExtraInput = Ignore;
}

# Read analog input voltage
getAnalogIn {
    out "MEAS:VOLT? %d";
    in "%f";
    ExtraInput = Ignore;
}

# Read digital input status
getDigitalIn {
    out "MEAS:DIG? %d";
    in "%d";
    ExtraInput = Ignore;
}

# System reset
systemReset {
    out "*RST";
}

# System status
getSystemStatus {
    out "*STB?";
    in "%d";
    ExtraInput = Ignore;
}
```

### Protocol File Notes
- **Terminator**: Defines message ending character
- **ExtraInput = Ignore**: Handles any extra characters from device
- **@init**: Executes initialization commands when record starts
- **Format Specifiers**: `%d` for integers, `%f` for floats, `%c` for characters

## Step 4: Create EPICS Database Records

### Create Database File
Create `arduino_scpi.db` in your IOC's `db/` directory:

```
################################################################################
# Arduino SCPI Database Records
# File: arduino_scpi.db
################################################################################

# Device identification
record(waveform, "$(P)$(R)IDN_RBV") {
    field(DESC, "Device identification")
    field(DTYP, "stream")
    field(INP,  "@arduino_scpi.proto getIDN $(PORT)")
    field(FTVL, "CHAR")
    field(NELM, "40")
    field(PINI, "YES")
}

# Digital Output Control (Pin 13 - LED)
record(bo, "$(P)$(R)LED") {
    field(DESC, "Arduino LED Control")
    field(DTYP, "stream") 
    field(OUT,  "@arduino_scpi.proto setDigitalOut(13) $(PORT)")
    field(ZNAM, "OFF")
    field(ONAM, "ON")
}

record(bi, "$(P)$(R)LED_RBV") {
    field(DESC, "Arduino LED Status")
    field(DTYP, "stream")
    field(INP,  "@arduino_scpi.proto getDigitalOut(13) $(PORT)")
    field(ZNAM, "OFF")
    field(ONAM, "ON")
    field(SCAN, "2 second")
}

# Analog Input Reading (A0)
record(ai, "$(P)$(R)AIN0") {
    field(DESC, "Analog Input 0")
    field(DTYP, "stream")
    field(INP,  "@arduino_scpi.proto getAnalogIn(0) $(PORT)")
    field(EGU,  "V")
    field(PREC, "3")
    field(SCAN, "1 second")
}

# Analog Output Control (if available)
record(ao, "$(P)$(R)AOUT0") {
    field(DESC, "Analog Output 0") 
    field(DTYP, "stream")
    field(OUT,  "@arduino_scpi.proto setAnalogOut(0) $(PORT)")
    field(EGU,  "V")
    field(PREC, "3")
    field(DRVL, "0")
    field(DRVH, "5")
}

record(ai, "$(P)$(R)AOUT0_RBV") {
    field(DESC, "Analog Output 0 Readback")
    field(DTYP, "stream") 
    field(INP,  "@arduino_scpi.proto getAnalogOut(0) $(PORT)")
    field(EGU,  "V")
    field(PREC, "3")
}

# System reset command
record(bo, "$(P)$(R)RESET") {
    field(DESC, "System Reset")
    field(DTYP, "stream")
    field(OUT,  "@arduino_scpi.proto systemReset $(PORT)")
}
```

## Step 5: Update IOC Startup Script

### Modify st.cmd File
Add these sections to your IOC startup script:

```bash
################################################################################
# Load protocol file path
################################################################################
epicsEnvSet("STREAM_PROTOCOL_PATH", "$(TOP)/db")

################################################################################
# Load Arduino database
################################################################################
dbLoadRecords("db/arduino_scpi.db", "P=ARDUINO:,R=DEV1:,PORT=ARDUINO")

################################################################################
# Optional: Load asynRecord for debugging
################################################################################
dbLoadRecords("$(ASYN)/db/asynRecord.db", "P=ARDUINO:,R=ASYN,PORT=ARDUINO,ADDR=0,OMAX=80,IMAX=80")
```

## Step 6: Test the Configuration

### Start the IOC
1. **Navigate to IOC directory**:
   ```bash
   cd /path/to/your/ioc/iocBoot/iocYourIOC
   ```
2. **Start IOC**:
   ```bash
   ./st.cmd
   ```
3. **Look for successful initialization messages**:
   - Serial port configuration
   - Database loading
   - Arduino identification response

### Test Communication
From the IOC console, test basic commands:

```bash
# Check device identification
dbpr ARDUINO:DEV1:IDN_RBV

# Control LED
caput ARDUINO:DEV1:LED 1    # Turn on
caput ARDUINO:DEV1:LED 0    # Turn off

# Read analog input
caget ARDUINO:DEV1:AIN0

# Check LED status
caget ARDUINO:DEV1:LED_RBV
```

## Step 7: Troubleshooting

### Serial Communication Issues
- **Port not found**: Check `/dev/tty*` devices and adjust path
- **Permission denied**: Add user to dialout group: `sudo usermod -a -G dialout $USER`
- **No response**: Verify baud rate matches Arduino firmware
- **Garbled output**: Check terminator settings and flow control

### EPICS Configuration Issues
- **Protocol not found**: Verify `STREAM_PROTOCOL_PATH` setting
- **Record errors**: Check protocol file syntax and record field names
- **Database loading fails**: Verify file paths and macro substitutions

### Debugging Tools
1. **Enable ASYN tracing** (in st.cmd):
   ```bash
   asynSetTraceMask("ARDUINO", -1, 0x11)    # Error + Flow
   asynSetTraceIOMask("ARDUINO", -1, 0x6)   # Read + Write
   ```

2. **Use asynRecord screen** for manual testing:
   ```bash
   caget -S ARDUINO:ASYN.AINP    # View last input
   caput ARDUINO:ASYN.AOUT "*IDN?"  # Send manual command
   ```

## Success Verification

Your serial communication is working when:
- IOC starts without serial port errors
- `*IDN?` returns Arduino identification
- LED control works from EPICS commands
- Analog readings update automatically
- No timeout or communication errors in IOC log

## Next Steps

With serial communication established between your EPICS IOC and Arduino, you're ready to understand how this fits into the larger system architecture:

**Next tutorial:** [Architecture of Sidekick Model 1](../model1-architecture.md) - Learn how your Arduino/EPICS setup integrates into the complete distributed control system

This will show you how your Arduino SCPI device works as part of the broader Sidekick demonstration system with multiple components, computers, and network communication working together through EPICS.