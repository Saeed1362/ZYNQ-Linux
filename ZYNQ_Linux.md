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

### Installing pcackes

    - Install the packages listed below. Ensure that you have administrative privileges. After installing the packages, please revert to a non-privileged user.

     Command:
        apt-get update && sudo apt-get install -y iproute2 gcc g++ net-tools libncurses5-dev zlib1g:i386 libssl-dev flex bison libselinux1 xterm autoconf libtool texinfo zlib1g-dev gcc-multilib build-essential screen pax gawk python3 python3-pexpect python3-pip python3-git python3-jinja2 xz-utils debianutils iputils-ping libegl1-mesa libsdl1.2-dev pylint3 cpio

        Note:
        * To change to Admin:           user:/$ sudo cu
        * To change to Normal user:     user:/$ Exit
    

### Installing Petalinux

    - You can install PetaLinux wherever you want, but if you want to follow the instructions in UG1144, you can follow the steps below. Before installing it, make sure that your system's "/bin/sh" is Bash rather than Dash.

    	-> To check if it is Bash or Dash run the below command:

            ls -l /bin/sh
            
            it should show: ... /bin/sh -> bash - if it shows ... /bin/sh -> dash, run the below command to change it to bash:
            sudo dpkg-reconfigure dash
            You will see a prompt asking, "Install dash as /bin/sh?". Select "No" to change the default shell to bash.

    -Create a directory:
            mkdir -p \opt\pkg\petalinux\2018.3

            if it does not let you create the directory there, you can use chmod 755 for it as below:

            chmode 755 mkdir -p \opt\pkg\petalinux\2018.3

    - Download Petalinux release 2018.3 from the AMD website

    - Go to the directory where the Petalinux is located, and get the tool installed by using the below instruction:

            Warning-> Make sure that you are not installing Petalinux through sudo, otherwise it won't work.

            command:
                ./petalinux-v2018.3-final-installer.run /opt/pkg/petalinux/2018.3

	        Note: You may receive a permission error as below that you can get it addressed via the below commands:

                * message: ERROR: Access Denied: No access permissions to the directory : /opt/pkg/petalinux/2018.3/
                * Solution:  chown -R <username>:<username> /opt/pkg/petalinux
         
# Creating the customized Linux

    - Run the below command to let Petalinux make the environment ready for the commands executions, and its tools in the current shell:
	
        source /opt/pkg/petalinux/2018.3/settings.sh

	    Note. You can check through the below command if the commands, aliases and functions are being added:

		    compgen -c ar

    - Create a new project through the below command:

	    petalinux-create --type project --template zynq --name pzynq

	    * type can be: project, ..

	    * template can be: zynq, microblaze, ultraScale

    - Now, you need to create a piece of hardware design in Vivado. Lets imagine that the name of the exported hardware from Vivado is  desgin_1_wrapper_hw_platform_0, so through the below command, you can configure your target Linux based on this hardware:

	petalinux-config --get-hw-description= ../desgin_1_wrapper_hw_platform_0

        Note: Make sure that you have at least activated one UART and one Timer for ZYNQ in Vivado, otherwise, your Linux will not work after completion of tailoring!

    - After finishing the stage number 3 successfully, you need to run the below command to get your Linux get built.

	    petalinux-build

    - When the Linux creation got completed, you need to run the below command to generate Boot.bin

	    petalinux-package --boot --fsbl <FSBL image> --fpga <FPGA bitstream> --uboot

# SD card preparation