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
**Application** software gives the task command to the OS

**OS** will trasnlate the software command in the programming language like C and C++, It also handles the memory allocation and the IO operations.

**Compiler** will take the output of the OS and convert it into the assembly language (.exe) file based on the Hardware type

**Assembler** will take the .exe file and will generate the mchine code (consisting of 1s and 0s)

## SoC design and OpenLANE


