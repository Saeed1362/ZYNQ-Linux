# Fixing Booti Error

There is a header file called **platform-auto.h** located in your project directory under the path **project-spec/meta-plnx-generated/recipes-bsp/u-boot/configs**. After finding it, please open it and scroll to the end of the file until you find the **booti** command, which is one of the Zynq **shell commands**. Replace it with the **bootm** command, and then try to build the Linux image again using the commands below.

![directory](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set11.jpg)

![platform-auto](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA44.jpg)
```
petalinux-build
```

When the Linux creation got completed, you need to run the below command to generate **Boot.bin**
```
petalinux-package --boot --fsbl <FSBL image> --fpga <FPGA bitstream> --uboot
```

The issue should be fixed now!