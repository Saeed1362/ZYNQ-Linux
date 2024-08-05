# Creating a simple peive of hardware in Vivado to configure the Linux device three based on it

# Follow the below steps to create it

Open Vivado, create a project, and in the "IP INTEGRATOR", click on "Create Block Design", and add a ZYNQ ip into your block design as below.

![IP_Adding](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado1.jpg)

Then click on the "Run Block Automation"

![Run_Automation](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado2.jpg)

If you are using a specific board, make sure that you have checked "Apply Board Preset" to set up the ZYNQ peripherals, and DDR memory. 

![Preset](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado3.jpg)

Then, your ZYNQ IP will be set up based on your TCL file. 

![ZYNQ_final](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado4.jpg)

Now, double click on the ZYNQ IP until you see the IP features as below

![ZYNQ_IP_Features](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado5.jpg)

Make sure that you have selected one of the UARTs that is connected to your board for connecting to the Linux terminal through, one Timer and SD card feature as well.

Now click on OK

![ZYNQ_Completed](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado6.jpg)

You need to create the HDL wrapper, so right-click on your design in the source section, and trigger the "Creat HDL Wrapper".

![HDL_Wrapper](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado7.jpg)

Now click on the "Run Synthesis" to get the design created.

![Synthesis](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado8.jpg)

If the synthesis stage to be completed successfully, you need to continue with "Run Implementation" as below.

![Implementation](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado9.jpg)

As soon as the implementation finishes successfully, the last stage which is "Generation Bitstream" with show up as below.

![Bitstream](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado10.jpg)

When the bitstream generation is done, click on File menu, and choose "Export" and "Export Hardware" respectively.

![Export](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado11.jpg)

Make sure that the "Includ Bitstream" is checked as below.

![Export_HW](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado12.jpg)

Now from the File menu, click on the SDK option, and let it get opened as below.

![SDK](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado13.jpg)

You can see that the design is created successfully in below.

![SDK_done](https://github.com/Saeed1362/ZYNQ7000_Linux/blob/main/images/Vivado14.jpg)