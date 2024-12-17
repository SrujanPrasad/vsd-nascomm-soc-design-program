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

![25](https://github.com/user-attachments/assets/af304681-c15b-4efe-abd6-23bc4e3a7092)


- So here the number of D flip flops are equal to **1613** and the total number of cells are equal to **14876**.Then the flop ratio becomes:

```math
Flop\ Ratio = \frac{1613}{14876}
```
 = 0.1084 or 10.84% 

## DAY-2 - Good floorplan VS Bad Floorplan and introduction to library cells

- This module involves understanding what is meant by utilization factor,aspect ratio and its significance in the physical design.
- A section of the silicon wafer is called as silicon die.

**Utilization factor** is defined as the ratio of the Area occupied by the netlist to the total area of the core.i.e,
```math
\text{Utilization Factor} = \frac{\text{Area Occupied by the Netlist}}{\text{Total Area Occupied by the Core}}
```
- Suppose the dimensions of a netlist are 2unit x 2unit and the dimensions of the core are 2unit x 2unit then the utilization factor is given by : 
  ```math
    \text{Utilization Factor}= \frac{2x2}{2x2}
  ```
  then the utilization factor = 1.This signifies that there is **100% utilization**.

  ![20](https://github.com/user-attachments/assets/f9fceb02-6f72-402d-93bf-0b2e088eed43)

  - Another important thing is the **aspect ratio**.Aspect ratio is defined as the ratio of the height to the width of the core.i.e,
```math
    \text{Aspect Ratio} = \frac{\text{Height}}{\text{Width}}
```
- Typically this aspect ratio is set to **1**.
- Few more points to consider are :
   - If the utilization factor is exactly equal to 1 then it is said to be 100% utilization and the core is of **square shape**.
   - If the utilization factor is equal to 0.5 then the core is of **rectangular shape**.
 
- Preplaced cells are the cells which are placed only once before the placement and routing as shown below :

![21](https://github.com/user-attachments/assets/bab9bf73-bdd5-4b35-a62d-c18caf6d692a)

![22](https://github.com/user-attachments/assets/19043fb1-355f-4931-884a-0f89694bfdde)

- **Noise margin** is defined as the maximum amplitude that can be superimposed on all the nodes of a long chain of inverter such that it doesnot cause any change in the logic level of the output.

  ![23](https://github.com/user-attachments/assets/af684a39-8a51-4ff1-99df-c702a2834e28)

- As the signal propagates there are more chances of the signal to get degraded.So for this reason decoupling capacitors are used to get the exact output.

  ![24](https://github.com/user-attachments/assets/eb66a917-66a4-4879-8827-da3e4eea7e3b)
  
  - Whenever there is a switching happening the decoupling capacitor looses its charge to the main circuit.
  - When there is no switching happening the decoupling capacitor replenishes its own charge.

- Consider the signal 0001101000111001.Upon application of this input to the inverter the output becomes : 1110010111000110.i.e all the capacitors at logic 1 will discharge to the same ground point as they are tapped to the same ground.This causes a problem called as the **ground bounce**.
- Similarly,all the capacitors at logic 0 will charge towards the Vdd (supply) and a problem called **voltage drooping** arises,as shown below :

   Ground bounce:
   ![26](https://github.com/user-attachments/assets/536bc75c-cea5-46a9-bf05-e3d6bd0d1c28)

  Voltage drooping:
  ![27](https://github.com/user-attachments/assets/be68146a-2034-475a-9719-f6776f5ea9ee)

- For this reason the recent chips have more than one supply points.

  ![29](https://github.com/user-attachments/assets/23605a3d-8604-465e-9dbe-1f073f66673b)

- The view of the power planning is shown below :

  ![30](https://github.com/user-attachments/assets/95c12812-b9b4-4af1-8d62-451ddfd050bb)

- Netlist is represents the connectivity.

  ![31](https://github.com/user-attachments/assets/2694dfaa-f54d-4792-b8f7-69e6ee7b809c)

- Final floorplan that is ready for the placement and routing step is shown below :

  ![32](https://github.com/user-attachments/assets/c05e7c34-4449-436d-826c-3b35444bb23a)

- ## Running Floorplan in OpenLane :

```
run_floorplan
```
```
cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/15-12_09-29
ls -ltr
cd results/floorplan
```

![33](https://github.com/user-attachments/assets/2c511161-32c7-4b67-95b4-060be5c84058)

![34](https://github.com/user-attachments/assets/d44fd32b-1dbc-45a3-9e3f-22feb4ec211a)

![35](https://github.com/user-attachments/assets/ac567438-375d-4b41-9af3-fcdce5da7e21)


  - To view the results :

    ```
     magic - T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read .. /../tmp/merged. lef def read picorv32a. floorplan. def &
    ```
![36](https://github.com/user-attachments/assets/34aea91b-0859-4575-a9c3-874b1eecf684)

Created layout : 
![37](https://github.com/user-attachments/assets/508a257f-55b6-4e4a-bf59-af0b34ab218f)

![38](https://github.com/user-attachments/assets/f996920d-575c-403a-8193-f3755879150c)

**NOTE :** 
``` math
1 micron = 1000 database units
```
According to our specifications it is 660685 and 671405
So according to our constraints the dimensions are : 
``` math
  \text{Dimensions }= \frac{660685}{1000} = 660.6 microns
```
``` math
   \text{Dimensions }= \frac{671405}{1000} = 671.405 microns
```

- Also we need to place the blocks as close as possible to the input and output ports in order to reduce the delays.
- Optimize placement is the stage where we estimate the wire lengths,capacitors and so on.
- We use a repeater block to reproduce the original signal so that signal integrity will be maintained.These are nothing but the **buffers**.

![39](https://github.com/user-attachments/assets/779d874f-3372-4710-b41e-5106f291e5b2)

- ## Running Placement in OpenLane :

 ```
cd results/floorplan
ls -ltr
cd ../placement/
ls
magic - T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged. lef def read picorv32a.placement. def &
```

![40](https://github.com/user-attachments/assets/9282f945-9ca8-429e-bd91-734bd51de5a4)

Below are the results : 

![41](https://github.com/user-attachments/assets/ca2626c6-e5d5-4283-a37b-eefa2cb6e28a)

![42](https://github.com/user-attachments/assets/d0751216-c59b-4d82-8ebd-532ac971aa93)

![43](https://github.com/user-attachments/assets/5dc05027-ed03-432d-ba04-362b56be46da)

- Cell design flow involves the following steps :

  ![44](https://github.com/user-attachments/assets/72762670-ccfd-4187-9161-5d8eb3419ff6)

```mermaid
flowchart TD
    Inputs --> DesignStep
    DesignStep --> Outputs
```

- The most important thing is the timing constraints.We need to understand some timing variables,the terms such as rise time,fall time and the propagation delay.
   - **Rise time** is defined as the time taken to transition from 10% to 90 % of the final value whereas **fall time** is defined the time taken to transition from 90% to 10% of the final value.
   - Below are some of the variables involved :

      ![45](https://github.com/user-attachments/assets/b71be7e7-4a7f-4d9d-9472-2f28f5207637)

   - **Propagation delay** is defined as the difference between the high level (fall or rise) and the low level (fall or rise).

      ![46](https://github.com/user-attachments/assets/ebacd555-d4d2-4cc9-ad5b-9cb079c7f93c)


## DAY-3 - Design Library using Magic Layout and NGSpice Characterization 

- So looking at the IO-Placer.We can change the environment variable by setting it to 2.

```
set ::env(FP_IO_MODE) 2
run_floorplan
```

We might see the below changes : 

![47](https://github.com/user-attachments/assets/cb7af822-4e60-4e4d-9fae-1c56f8d81531)

![48](https://github.com/user-attachments/assets/c6eedf79-6a71-4b6f-bddf-8a2dc43e6f15)

![49](https://github.com/user-attachments/assets/278c82d6-cd87-4e38-a9ca-e6f13056886c)


- CMOS Inverter is a CMOS circuit which performs the basic logic inversion of the input signal.It is a robust (strong) circuit.
- Analysing a CMOS Inverter by plotting its VTC (Voltage Transfer Characteristics) using the Spicedeck which involves the following processes :
  
 ```mermaid
flowchart TD
    Component_Connectivity --> Component_Values
    Component_Values --> Identify_Nodes
    Identify_Nodes --> Name_the_Nodes
```

  ![50](https://github.com/user-attachments/assets/069359da-f06a-4d05-b205-72496cd44bb9)

![51](https://github.com/user-attachments/assets/13508c7e-9684-42d7-a1cc-4e32b7955793)

  ![52](https://github.com/user-attachments/assets/b7d6924c-5fde-43a4-8b51-0f85d4b537ab)

- ### Cloning the github

  ![53](https://github.com/user-attachments/assets/4932a2bf-1425-47a2-9a7a-8660df0e4ea9)

  Copying the sk130A.tech file to the github repository that we have just cloned :

  ![54](https://github.com/user-attachments/assets/be8bd66a-16c6-4b48-b3e4-de3fc9c11c6a)

- Layout of a CMOS Inverter is shown below :

  ![55](https://github.com/user-attachments/assets/8be8444a-4211-4a82-8fe3-69668696e2ec)

- **CMOS Fabrication** process involves the following steps :
  - Select the substrate.
  - Create active regions for the transistor.
  - N-Well and P-well formation.
  - Formation of gate.
  - Lightly doped drain formation.
  - Source and drain formation.
  - Form interconnects and the contacts.
  - Higher level formation.

  The final fabricated CMOS is as shown below :

  ![56](https://github.com/user-attachments/assets/4d534266-ea39-40af-b530-1818138654cf)

 - We can get to know about the particular section in a layout by placing our cursor on it and hitting S on our keyboard to select it.
 - We can then go to the tkcon window and type **''what''** to know about it.

    ![image](https://github.com/user-attachments/assets/070ed493-94f9-48b8-a2c2-2edc38c33734)

    ![image](https://github.com/user-attachments/assets/fc3258c9-a247-45aa-91df-b0baca810202)

- Below are the steps that need to be followed in order to create the spice file :
   - In the tkcon window type the following commands :
     ```
     extract all
     ext2spice cthreshold 0 rthreshold 0
     ext2spice
     ```

    ![59](https://github.com/user-attachments/assets/834cc4e9-ffcb-4716-85a0-2eadda933fc7)

    In the terminal window : 
     
  ```
  cd ~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
  ls -ltr
  vim sky130_inv.spice
  ```
  ![60](https://github.com/user-attachments/assets/0d7b8b95-fa4c-4129-a9a7-6966fa3b4961)


  This opens the following :

  ![61](https://github.com/user-attachments/assets/d497f76b-c558-42ac-af62-b345534fae8d)

  So the parameters are edited in the .spice file that is we first include the necessary libraries such as pshort.lib and nshort.lib and run the ngspice as shown in the below image :

  ![63](https://github.com/user-attachments/assets/4a6c4d7f-95b0-4d12-bd7a-3c01177c6746)

  We then run the following command :

  ```
  ngspice sky130_inv.spice
  ngspice->plot y vs time a
  ```

  ![64](https://github.com/user-attachments/assets/c052a0ec-c216-49c3-bdc4-a871e0677690)

  This opens the transient response as shown below :

  ![65](https://github.com/user-attachments/assets/558c0720-c036-4d63-91bd-a6d2cbcae4a1)

  



  
  

