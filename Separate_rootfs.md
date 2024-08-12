# Keeping "rootfs", "boot.bin", and "image.ub" separately on an SD card

# One important advantage of keeping "rootfs" separately on an SD card is that you can retain your changes after power-cycling. This means that if you, for instance, create a file, it will not be lost when you restart your Linux OS. Please follow the steps below to separate "rootfs", "boot.bin", and "image.ub", and then place them on the SD card.

Let's imagin that you have taken all the necessary steps, and you are ready to run the below command. If not, please refer to ["Creating the customized Linux"](https://github.com/Saeed1362/ZYNQ-Linux/blob/main/README.md)

```
petalinux-config --get-hw-description= ../my_design_wrapper_hw_platform_0
```

As soon as you run the above command, the following screen will open. Please follow the steps shown in the images until you exit the sequence of screens.