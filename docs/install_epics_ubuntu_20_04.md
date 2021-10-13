# Installing EPICS-latest on Ubuntu 20.04

Installing EPICS on up-to-date Ubuntu 20.04.2.0 LTS (Desktop, amd64)

# References
1. [EPICS 7 getting started guide](https://docs.epics-controls.org/projects/how-tos/en/latest/getting-started/installation.html)
    
I followed the above tutorial to make this particular guide.

# Steps
1. Bring system fully up-to-date
    `sudo apt -y update`
    `sudo apt -y upgrade`
2. Install basic build tools (the *build-essential* package includes key development tools like gcc and perl)
    `sudo apt -y install build-essential`
3. Install git
    `sudo apt -y install git`
4. (Optional) Install networking tools, including nmap, netstat, and ifconfig
    `sudo apt -y install net-tools`
5. (Optional) Confirm GNU make is of version 3.81 or higher
    `make --version`
6. (Optional) Confirm that perl is version 5.8.1 or higher
    `perl --version`
7. (Optional) Check that "libreadline8" is installed (it is.)
    a. (EPICS installation README mentions using readline)
    `apt search readline`
8. Create an EPICS folder, download the latest repository code, and compile EPICS base from source:
    ```
    mkdir $HOME/EPICS
    cd $HOME/EPICS
    git clone --recursive https://github.com/epics-base/epics-base.git
    cd epics-base
    make
    ```
    (Note: the `make` step took me about twenty minutes.)
9. Add several environment variables to your ~/.bashrc file
    ```
    export EPICS_BASE=${HOME}/EPICS/epics-base
    export EPICS_HOST_ARCH=$(${EPICS_BASE}/startup/EpicsHostArch)
    export PATH=${EPICS_BASE}/bin/${EPICS_HOST_ARCH}:${PATH}
    ```
10. Close and re-open terminal to load changes in ~/.bashrc. Can now build local EPICS databases and use commands like "softIoc" and "caget"!
