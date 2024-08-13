# Keeping "rootfs", "boot.bin", "system.dtb" and "image.ub" separately on an SD card

## One important advantage of keeping "rootfs" separately on an SD card is that you can retain your changes after power-cycling. This means that if you, for instance, create a file, it will not be lost when you restart your Linux OS. Please follow the steps below to separate "rootfs", "boot.bin", and "image.ub", and then place them on the SD card.

Let's imagin that you have taken all the necessary steps, and you are ready to run the below command. If not, please refer to ["Creating the customized Linux"](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/README.md)

```
petalinux-config --get-hw-description= ../my_design_wrapper_hw_platform_0
```

As soon as you run the above command, the following screen will open. Please follow the steps shown in the images until you exit the sequence of screens.

- 1 

![1](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA1.jpg)


- 2 

![2](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA2.jpg)


- 3 

![3](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA3.jpg)


- 4 

![4](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set1.jpg)


- 5 

![5](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set2.jpg)


- 6 

![6](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set3.jpg)


- 7 

![7](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set4.jpg)


- 8 

-![8](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set5.jpg)


- 9 

![9](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set6.jpg)


- 10 

![10](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set7.jpg)


- 11 

![11](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set8.jpg)


- 12 

![12](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set9.jpg)


- 13 

![13](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set10.jpg)

Once the job reaches this point, you need to run the below commands to get the Linux OS built completely.

```
petalinux-build
```

When the Linux creation got completed, you need to run the below command to generate **Boot.bin**
```
petalinux-package --boot --fsbl <FSBL image> --fpga <FPGA bitstream> --uboot
```

The final stage is copying the generated files to their correct partitions on the SD card. In the previous section, when creating Linux, you only needed to copy **BOOT.BIN** and **image.ub** to the SD card, as there was only one partition and **rootfs** was embedded within **image.ub**. However, in this section, since they are all separated, you need to move them to their correct partitions. To achieve this, you’ll need to create partitions on the SD card. You can use the **gparted** application, which is a graphical tool, instead of using the command line for partitioning.
Install GParted using the command below.

```
sudo apt-get install gparted
```

Then run it using the command below.

```
sudo gparted
```
**Note.** GParted requires **administrative permissions**, so you should run it using **sudo**.

Now follow the steps below to partition your SD card. Note that you will need two partitions: one for storing BOOT.BIN, image.ub, and system.dtb, which should be in FAT32 format and at least 500 MB in size. The second partition should be in ext4 format for storing the rootfs, so you can dedicate the remaining capacity of your SD card to it.

- 1 

![G1](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA6.jpg)


- 2 

![G2](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA7.jpg)


- 3 

![G3](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA8.jpg)


- 4 

![G4](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA9.jpg)


- 5 

![G5](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA10.jpg)


- 6 

![G6](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA11.jpg)


- 7 

![G7](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA12.jpg)

After partitioning the SD card, you need to create directories under **/mnt** named BOOT and rootfs, and then mount the relevant partitions on the SD card to these directories. In my case, the SD card is identified as sdb, with partitions sdb1 and sdb2. The device name may differ on your machine, so you can find the correct one using the following command.

```
lsblk -la
```
Finally, follow the steps below to create and mount them.

![mount](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA13.jpg)

At the end, you can copy the files into the correct partitions as shown below. Note that **rootfs.tar.bz2** is not a single file; it is a compressed archive. Therefore, you need to extract it into the rootfs partition using the tar command, as illustrated in the image.

![copy](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA44.jpg)

Now you can insert the SD card and boot Linux. Sometimes, you may encounter a booti error, which prevents the OS from booting completely. The booti command is intended for Zynq UltraScale, but it may not work for Zynq. If you face this issue, refer to the [Fixing Booti Error](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/booti.md) section for a solution.

