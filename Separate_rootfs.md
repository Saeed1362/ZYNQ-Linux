# Keeping "rootfs", "boot.bin", and "image.ub" separately on an SD card

## One important advantage of keeping "rootfs" separately on an SD card is that you can retain your changes after power-cycling. This means that if you, for instance, create a file, it will not be lost when you restart your Linux OS. Please follow the steps below to separate "rootfs", "boot.bin", and "image.ub", and then place them on the SD card.

Let's imagin that you have taken all the necessary steps, and you are ready to run the below command. If not, please refer to ["Creating the customized Linux"](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/README.md)

```
petalinux-config --get-hw-description= ../my_design_wrapper_hw_platform_0
```

As soon as you run the above command, the following screen will open. Please follow the steps shown in the images until you exit the sequence of screens.

1-
![1](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA1.jpg)

2-
![2](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA2.jpg)

3-
![3](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_setA3.jpg)

4-
![4](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set1.jpg)

5-
![5](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set2.jpg)

6-
![6](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set3.jpg)

7-
![7](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set4.jpg)

8-
![8](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set5.jpg)

9-
![9](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/images/Linux_set6.jpg)

10-
![10]()