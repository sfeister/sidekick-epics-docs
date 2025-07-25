# Create and Run a Simple EPICS IOC

This tutorial will guide you through creating your first EPICS Input/Output Controller (IOC) on your Raspberry Pi. An IOC is the core component that hosts process variables and serves data to EPICS clients.

## Step 1: Create IOC Application Directory

First, create a dedicated directory for your IOC application:

```bash
cd ~
mkdir myioc
cd myioc
```

## Step 2: Generate Base App and IOC Skeleton

Use the EPICS makeBaseApp tool to generate the application structure:

```bash
/home/debian/Apps/epics/base-7.0.8/bin/linux-arm/makeBaseApp.pl -t example myioc
```

This creates the basic directory structure and Makefiles needed for an EPICS application.

## Step 3: Compile the Application Source

Navigate to the source directory and compile the application:

```bash
cd myiocApp/src/
make
```

## Step 4: Build the Application & Install Components

Move up one directory level and build the complete application:

```bash
cd ..
make
```

This compiles all components and prepares the IOC for database and boot configuration.

## Step 5: Add the Database File

Create a database file that defines your process variables (PVs):

```bash
mkdir -p ~/myioc/db  # Create db directory if it doesn't exist
cd ~/myioc/db
nano myioc.db
```

Add the following content to define two test records:

```
record(ai, "test:example1") {
  field(DESC, "Test input 1")
  field(VAL, "42")
}

record(ai, "test:example2") {
  field(DESC, "Test input 2")
  field(VAL, "13")
}
```

After saving the database file, rebuild the application:

```bash
cd ~/myioc/
make
```

## Step 6: Generate the IOC Boot Directory

Create the IOC boot configuration:

```bash
/home/debian/Apps/epics/base-7.0.8/bin/linux-arm/makeBaseApp.pl -i -t example myioc
```

When prompted for the application name, simply press Enter to use the default (myioc).

## Step 7: Manually Create envPaths File

The envPaths file sets up environment variables for your IOC:

```bash
cd ~/myioc/iocBoot/myioc
nano envPaths
```

Add the following content:

```bash
epicsEnvSet("TOP", "/home/debian/myioc")
epicsEnvSet("IOC", "myioc")
epicsEnvSet("ARCH", "linux-arm")
```

Make the file readable:

```bash
chmod +r envPaths
```

## Step 8: Edit st.cmd

The startup command file (st.cmd) configures and starts your IOC:

```bash
nano st.cmd
```

**Note:** There might be prefilled content in `st.cmd`. If needed, remove the existing file and create a new one.

Add the following content:

```bash
#!../../bin/linux-arm/myioc
< envPaths
cd "/home/debian/myioc"

## Register all support components
dbLoadDatabase("dbd/myioc.dbd", 0, 0)
myioc_registerRecordDeviceDriver(pdbbase)

## Load record instances
dbLoadRecords("db/myioc.db", "user=debian")

cd "/home/debian/myioc/iocBoot/myioc"
iocInit
```

Make the file executable:

```bash
chmod +x st.cmd
```

## Step 9: Run the IOC

Start your IOC:

```bash
./st.cmd
```

You should see initialization messages ending with:

```
iocRun: All initialization complete
```

Your IOC is now running and serving the process variables you defined.

## Step 10: Test from Separate Terminal

Open a new SSH session to your Pi and test your IOC:

```bash
caget test:example1
caget test:example2
```

**Expected Output:**
```
test:example1                          42
test:example2                          13
```

## Success!

Congratulations! You have successfully created and run your first EPICS IOC. Your IOC is now:
- Serving two process variables (`test:example1` and `test:example2`)
- Accessible from EPICS clients on your network
- Ready for expansion with additional records and functionality

## Next Steps

With a working IOC confirmed, you're ready to integrate real hardware:

**Next tutorial:** [Flash Arduino SCPI](../arduino-set-up/flash-arduino.md) - Prepare your Arduino device with SCPI communication protocol

This will enable your IOC to communicate with physical hardware devices through serial communication.