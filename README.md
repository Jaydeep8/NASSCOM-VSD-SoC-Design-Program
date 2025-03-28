# NASSCOM-VSD-SoC-Design-Program
# Contents 
1. [Day1](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/edit/main/README.md#day1---inception-of-open-source-eda-openlane-and-sky130-pdk)

## Day1 - *Inception of open-source EDA, OpenLANE and Sky130 PDK*

### How to talk to computers
**Introduction to QFN-48 Package, chip, pads, core, die and IPs**
![image](https://github.com/user-attachments/assets/f2bb4515-daa0-4369-8b27-5243e1834e3c)
-Core : 
It is the area where our entire logic will be implemented.

-Die :
It is the size of the chip.

-Pads :
Through these pads signals can travel into the chip from external sources and viceversa.

![image](https://github.com/user-attachments/assets/bc3a2ec5-64b6-410a-9698-68b23343f071)
Foundry IPs : These are the pre designed Intellectual Properties provided by the foundry like SRAM, ADC etc.

**Introduction to RISC-V**
![image](https://github.com/user-attachments/assets/b20d2666-a748-4358-863a-e51d4a78fe05)
**ISA** : Instruction set Architecture helps computer chip to understand the task and guide the layout fow.


**From Software Applications to Hardware**
![image](https://github.com/user-attachments/assets/336fde2a-2cab-4a21-b809-bce40c62934e)
The software application to hardware flow is shown in the image
where 

**Application software** gives the task command to the OS

**OS** will trasnlate the software command in the programming language like C and C++, It also handles the memory allocation and the IO operations.

**Compiler** will take the output of the OS and convert it into the assembly language (.exe) file based on the Hardware type

**Assembler** will take the .exe file and will generate the mchine code (consisting of 1s and 0s)

### SoC design and OpenLANE

**Introduction to all components of open-source digital asic design**

![image](https://github.com/user-attachments/assets/1ddb63c0-5e32-4898-9ea2-96902fbddfcd)

**RTL Designs**, **EDA Tools** and **PDK Data** are the three main components of open souce digital ASIC design.


**Simplified RTL2GDS flow**
![image](https://github.com/user-attachments/assets/7caeae3b-5fc1-46c0-888d-15b21c4d7bd2)

The simplified RTL2GDS2 flow is shown in the image
- Synthesis : It converts the rtl level design to the circuit level design using standrd cell library.
  
- Floor Planning & Power Planning : in Floor Planning the area of chip is partioned and defined , In Power Planning the the vdd & vds network of the chip is defined 

- Placement : the designed components are placed on the defined areas according to the floorplan. it has two stages
  1) Global Placement
  2) Detailed Placement
 
- Clock Tree Synthesis : the clock routing network is designed to provide clock signal to the various blocks, H-tree X-tree and I-tree are the symmetric tree structures used to reduce the clock skew

- Routing : The signal routing is done with metal layers. It has two stages 
 1) Global Routing
 2) Detailed Routing
    
- Sign-Off : this is the final step to generaye the GDS2 file, During the sign-off various kinds of verifications are perfomed like
  1) DRC : Design Rule Check
  2) LVS : Layout versus Schematic
  3) STA : Static Timing Analysis

**Introduction to OpenLANE Detailed ASIC Design Flow**
![image](https://github.com/user-attachments/assets/2fcf7a5e-26a1-487e-979c-c54aa96ac70d)

The Openlane flow is the complete Open source process to perform RTL2 GDS2 process , The openlane supports various tools that support in the flow like **Yosys,open STA, fault, openlane road, magic**.

### Get familiar to open-source EDA tools
The **picorv32a** is the design that we are giong to work on![empty folder](https://github.com/user-attachments/assets/39644788-7813-497e-9763-3204db5f1405)

The first step is to go to the openlane directory **`~/Desktop/work/tools/openlane_working_dir/openlane`**
and then **`docker`** command is used to enter the bash.
**`./flows.tcl -interactive`** is used to run the interactive (step by step mode)
**`package require openlane 0.9`** it will import the 0.9 openlane package.
**`prep -design picorv32a`** it will prepare the implementation of picorv32a design
**`run_synthesis`** it will run the yosys and abc synthesis
![run synthesis](https://github.com/user-attachments/assets/e8d8a541-cafc-4e6b-ae59-bc4b495a5d88)
![synthesis complete](https://github.com/user-attachments/assets/80b5f7c8-61ec-48f9-b082-88326cdbc81c)

Finding the flipflop ratio
![calculation](https://github.com/user-attachments/assets/37399314-e3dd-4863-b872-2231ae907ca2)
The total no.of cells used in the design are 14876 and The count of D-flipflops in the design are 1613.
to find the flip flop ratio (1613/14876)*100= **10.84%**

after running synthesis the new files are created in the **picorv32a** folder

the mergerd file
![new files with merged file](https://github.com/user-attachments/assets/e47daf49-db2a-42da-b045-61c1fa2970cc)
the synthesis file
![synthesis file](https://github.com/user-attachments/assets/a9728ad6-c5c8-4950-a8c8-485150f2309a)


