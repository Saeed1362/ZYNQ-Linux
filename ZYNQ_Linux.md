# How to Use Petalinux Project to Create a Custom Linux Image for ZYNQ

### MYIR z-turn v2 Development board
#### August 2024

## Contents

- 1 [Setting up your environment](#Setting-up-your-environment)
    - System requirements for creating the Linux 
    - Installing pcackes
    - Installing Petalinux
- 2 [Creating the customized Linux](#Creating-the-customized-Linux)
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

Install the packages listed below. Ensure that you have administrative privileges. After installing the packages, please revert to a non-privileged user. Please use the below command.

```    
apt update
apt upgrade
apt-get update && sudo apt-get install -y iproute2 gcc g++ net-tools libncurses5-dev zlib1g:i386 libssl-dev flex bison libselinux1 xterm autoconf libtool texinfo zlib1g-dev gcc-multilib build-essential screen pax gawk python3 python3-pexpect python3-pip python3-git python3-jinja2 xz-utils debianutils iputils-ping libegl1-mesa libsdl1.2-dev pylint3 cpio
```

To change to Admin:           
```
sudo su
```
To change to a non-privileged:     
```
Exit
```
![Package_installation](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/packages.jpg)

### Installing Petalinux

You can install PetaLinux wherever you want, but if you want to follow the instructions in UG1144 document, you can follow the steps below. Before installing it, make sure that your system's "/bin/sh" is Bash rather than Dash.

To check if it is Bash or Dash run the below command:
```
ls -l /bin/sh
```
            
It should show: ... /bin/sh -> bash - if it shows ... /bin/sh -> dash, run the below command to change it to bash.
```
sudo dpkg-reconfigure dash
```
You will see a prompt asking, "Install dash as /bin/sh?". Select "No" to change the default shell to bash.

Create a directory:
```
mkdir -p \opt\pkg\petalinux\2018.3
```

If it does not let you create the directory there, you can use **chmod 755** for it as below:
```
chmode 755 mkdir -p \opt\pkg\petalinux\2018.3
```

Download Petalinux release 2018.3 from the AMD website (https://www.xilinx.com/member/forms/download/xef.html?filename=petalinux-v2018.3-final-installer.run)

Go to the directory where the Petalinux is located, and get the tool installed by using the below instruction:

***Make sure that you are not installing Petalinux through sudo, otherwise it won't work***

```
./petalinux-v2018.3-final-installer.run /opt/pkg/petalinux/2018.3
```
***Note.*** You may receive a permission error like the one shown below, which can be addressed using the following commands.

***Message:*** ERROR: Access Denied: No access permissions to the directory : /opt/pkg/petalinux/2018.3/

```
chown -R <username>:<username> /opt/pkg/petalinux
```
![Installing_PetaLinux](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/installing.jpg)



If PetaLinux is installed successfully, you will receive the message below.

![PetaLinux_Installed](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/installed.jpg)
         
# Creating the customized Linux
### Creating the Linux
Run the following command to let PetaLinux set up the environment for command execution and make its tools available in the current shell.
```
source /opt/pkg/petalinux/2018.3/settings.sh
```

![source_command_execution](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/installed.jpg)

***Note.*** You can use the command below to check if the commands, aliases, and functions are being added correctly.
```
compgen -c ar
```

Create a new project using the command below.
```
petalinux-create --type project --template zynq --name pzynq
```
**type** can be: project, app and module. We select **project**.

**template** can be: zynq, zynqMP, microblaze and versal. For this project, we choose **zynq**.

Now, you need to [create a hardware design in Vivado.](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/ZYNQ_HW.md)


Since the name of the exported hardware from Vivado is **my_design_wrapper_hw_platform_0**, you can configure your target Linux based on this hardware using the command below.

```
petalinux-config --get-hw-description= ../my_design_wrapper_hw_platform_0
```

**Note.** **"../"** points to the location of **my_design_wrapper_hw_platform_0**. Here, it means that it is located in the directory one level above the current one.

**Note.** Make sure that you have at least one **UART** and one **Timer** activated for ZYNQ in Vivado; otherwise, your Linux will not function correctly after tailoring is completed.

After successfully completing stage 3, run the following command to build your Linux system.
```
petalinux-build
```

When the Linux creation got completed, you need to run the below command to generate **Boot.bin**
```
petalinux-package --boot --fsbl <FSBL image> --fpga <FPGA bitstream> --uboot
```

# SD card preparation

### Having a quick look at the generated files

![File](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/File.jpg)
**Boot.bin**: It contains FSBL.
**image.ub**: Kernel image of image.ub contains Linux Kernel, DTB (Device Tree Blob) and RootFS
**rootfs.bin**: It is the raw image of the RootFS that can be used directly/
**rootfs.ex4**: This RootFS is sutable for SD cards, and can be writtend directly to it. 
**rootfs.ex3**: Older version of .ex4 type.
**rootfs.jffs2**: This version of RootFS is suitable for FLASH memories like NAND flashes. 

### Copying the necessary files on the SD card and turning the board on

![Files](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Files.jpg)
To boot your Linux system, navigate to the path indicated in the image above, and copy Boot.bin and image.ub to your SD card. Ensure that the boot pins on your board are configured for the correct memory (in this case, the SD card). Connect the board to a terminal using software like PuTTY and set the baud rate to 115200 bps. Reset the board and let it boot up.


