# How to Use Petalinux Project to Create a Custom Linux Image for ZYNQ

### MYIR z-turn v2 Development board
#### August 2024

## Contents

- 1 [Setting up your environment](#Setting-up-your-environment)
    - System requirements for creating the Linux 
    - Installing pcackes
    - Installing Petalinux
- 2 [Creating the customized Linux](#Creating-the-customized-Linux)
    - Creating a simple piece of hardware in Vivado
    - Creating the Linux
- 3 [SD card preparation](#SD-card-preparation)
    - Having a quick look at the generated files
    - Copying the necessary files on the SD card and turning the board on


# Setting up your environment
### System requirements for creating the Linux
    - Hardware
      You can use any board equipped with a ZYNQ VLSI that has an Ethernet port, UART port, and SD card capability.
    - Workstation:
      8 GB RAM (recommended minimum for Xilinx® tools)
      2 GHz CPU clock or equivalent (minimum of eight cores)
      100 GB free HDD space
      Supported OS:
      Red Hat Enterprise Workstation/Server 7.4, 7.5, 7.6, 7.7 (64-bit)
      CentOS Workstation/Server 7.4, 7.5, 7.6, 7.7 (64-bit)
      Ubuntu Linux Workstation/Server 16.04.5, 16.04.6, 18.04.1, 18.04.2, 18.04.3, 18.04.4 (64-bit)

      ** I have used:
         Workstation:
            270 GB HDD space
            8 GB RAM and
            Intel(R) Core(TM) i7-8550U CPU @ 1.80GHz   1.99 GHz
         Software and OS:
            Ubuntu 16.04.5 LTS
            Vivado v2018.3
            Petalinux v2018.3
         Hardware:
            Z-turn V2from MYIR
         