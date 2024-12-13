# Digital VLSI SoC Design and Planning program (December 11 - December 24)-By Srujan Prasad 

## Overview of this repository : 
This repository contains all the necessary details regarding the SoC design and planning that involves executing all the necessary steps starting from understanding the basics such as application softwares,
going all the way to the floor planning,layout generation,timing analsyis and finally knowing about the foundry which is the Google Skywater 130nm technology.

## Installation of Virtual Box and Openlane

![image](https://github.com/user-attachments/assets/050c904a-30ed-4acd-8355-1eb8fc1e5048)

![image](https://github.com/user-attachments/assets/de858cb1-57f3-4ba8-a8b5-3d003cab2ee6)

## DAY-1 - Introduction to the Open Source EDA,OpenLane and Sky 130 PDK (Module-1 and Module-2)

This course starts with giving an introduction the Open Source EDA and most importantly about the Openlane and sky 130 process design kit.

<details>

<summary>Some theory</summary>
- Arduino is the most commonly used Microcontroller for various projects.So the chip that can be fabricrated at the end of all the process can be used in iwatches,arduino microcontrollers and so on.
Below is the image of the arduino microcontroller,

![Arduino board](https://github.com/user-attachments/assets/668dd86c-6969-41f1-b3ab-fbe7b02a31b5)

![4](https://github.com/user-attachments/assets/848aa69c-c590-4fdc-9b2f-ce9ffdb68ed9)

![5](https://github.com/user-attachments/assets/b65bcc02-004f-4279-a055-7f34e3d24ee9)

- System Software is a software that handles the input/output operations,allocates memory and performs the low level system functions.
  * The C code is compiled by a compiler
  * The output of the compiler is passed thorugh an assembler where it is converted into hexadecimal code (assembly code)
  * This is then converted to the binary form so that hardware can understand and perform the desired operation.The steps are shown in the image below : 

![7](https://github.com/user-attachments/assets/6a54ecb3-b89a-47ed-8b69-a4554115409b)

Open Lane Flow : 

![13](https://github.com/user-attachments/assets/11f312e9-c2dd-425f-81d7-08eac95a1a1b)

</details>

## DAY-1 - Getting familiar with Open Lane (Module-3)
- This module involved getting familiar with the open lane tool by first checking the version of the openlane,preparing it for further process and finally running of the synthesis.
- Below are commands that were run to invoke openlane and perform synthesis :

To invoke openlane : 
```
   cd ~/Desktop/work/tools/openlane_working_dir/openlane
   ls -ltr
   docker
   pwd
   ./flow.tcl -interactive
```

To check its version  :

```
  package require openlane 0.9
```
To perform preparation  :
```
prep -design picorv32a

```
Finally to run the synthesis 
```
run_synthesis
```
Below are some of the images : 

![18](https://github.com/user-attachments/assets/8b8fa7f0-0f2c-4ec4-b255-31d125c89429)

Creation of folder : 
![17](https://github.com/user-attachments/assets/2b845c92-7d94-46df-8c80-6212b196b9d9)

![image](https://github.com/user-attachments/assets/1b6f127b-cd14-424f-b5a4-4d99b0de36a8)


- Another thing is the flop ratio.Flop ratio is defined as the ratio of the number of D flip flops to the total number of cells i.e ,
```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
- So here the number of D flip flops are equal to **1613** and the total number of cells are equal to **14876**.Then the flop ratio becomes :

```math
Flop\ Ratio = \frac{1613}{14876}
```
 = 0.1084 or 10.84% 



