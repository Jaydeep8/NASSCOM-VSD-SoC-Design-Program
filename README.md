# NASSCOM-VSD-SoC-Design-Program
# Contents 
1) [Day1: Inception of open-source EDA, OpenLANE and Sky130 PDK](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/tree/main?tab=readme-ov-file#day1---inception-of-open-source-eda-openlane-and-sky130-pdk)
2) [Day2: Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/tree/main?tab=readme-ov-file#day2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
3) [Day3: Design library cell using Magic Layout and ngspice characterization](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/tree/main?tab=readme-ov-file#day3---design-library-cell-using-magic-layout-and-ngspice-characterization)
4) [Day4: Pre-layout timing analysis and importance of good clock tree](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/tree/main?tab=readme-ov-file#day4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
5) [Day5: Final steps for RTL2GDS using tritonRoute and openSTA](https://github.com/Jaydeep8/NASSCOM-VSD-SoC-Design-Program/tree/main?tab=readme-ov-file#day5---final-steps-for-rtl2gds-using-tritonroute-and-opensta)


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


## Day2 - *Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells*
Chip FloorPlanning Considerations
![image](https://github.com/user-attachments/assets/3292fd6c-0838-40b3-8864-3cdef867e621)
Utilization Factor and Aspect Ratio
In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.

- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.

- Die is an area that encircles the core area and used for placing I/O related components.

The height and width of core area will be decided by the netlist of the design. It will be based on the no.of components required in order to execute the logic and the height and width of the die area will be dependent on the core area height and width.

![image](https://github.com/user-attachments/assets/0a1dd892-3d34-4040-9873-54322c6fd552)         
*Utilization Factor :*  Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area".For a good FloorPlan, The Utilization Factor should never be '1' because when the Utilization factor becomes '1' , there will be no place for adding additional logic if needed and it will be considered as a bad FloorPlan.

`Utilization Factor = (Area occupied by netlist / Total core area)`

*Aspect Ratio :*  Aspect Ratio is defined as "The ratio of Height of the core to the width of the core". If the Aspect ratio is '1' , then the core is said to be in a square shape and other than '1' the core will be a rectangle.

`Aspect Ratio = (Height of the core / Width of the core)`

![image](https://github.com/user-attachments/assets/42cf43d1-a8c2-443c-b228-c592fed3309f)

In this case, when calculated

- Utilization factor = (4 squnits)/(4 squnits) = 1

- Aspect Ratio = (2 units)/(2 units) = 1 //The core is in a square shape.


![image](https://github.com/user-attachments/assets/d002ec6c-0f26-4f74-9287-dac78967d5ff)

In this case, when calculated

 Utilization factor = (4 squnits)/(8 squnits) = 0.5

  Aspect Ratio = (2 units)/(4 units) = 0.5 //The core is in a rectangular shape.

- Define location of pre-placed cells                                                               
  Some of the IPs are placed by the user before automated placement and routing and placement. Hence they are called pre-placed cells.

 - Surround pre-placed cell with decoupling capacitor.                                                                             
 state change from a logic '0' to logic '1' requires charge from a voltage source. But, due to the connecting wires from the voltage source to the filpflops, 
 there might be voltage drop because of resistance of the wires. If the voltage drop is less than the noise margin, there will no state change. To mitigate this 
 issuse , we make use of decoupling capacitors. These decoupling capacitors are placed near all the sub-blocks.

- Power planning                                                                                    
  Power planning is a critical aspect of integrated circuit (IC) and system-on-chip (SoC) design that involves creating an efficient power distribution network 
  (PDN) to ensure reliable power delivery to all components of the chip.

 - Pin placement                                              
  The I/O pins are placed between the boundaries of die and core. The pins are placed in such a way that they are close to the blocks that they feed as input to. 
  The clocks pins are bigger than the normal pins as to provide least resistance path since clocks provide continuous signals throughout the chip function.

 - Logical cells placement blockage                          
  we make sure to block the pin placement region as to avoid the automated place and route from accessing this region. This is called Logical cells placement 
  blockage.

## day2 lab 

```bash
 run_floorplan
```

![run_floorplan](https://github.com/user-attachments/assets/b3f26a7a-524f-4ef8-a90a-c12f5441f4f2)

**`poicorv32a.floorplan.def file`**

![image](https://github.com/user-attachments/assets/e123d7ba-df3b-4554-86b2-4b05d96b0c55)
According to floorplan def

```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Area\ of\ die\ in\ microns = \frac{660.685 * 671.405}{1000 * 1000} = 443587.21\ Microns^2
```

Once the floorplan is complete, you can review the generated report to assess aspects such as die area. However, to visualize the design in a graphical user interface (GUI), you should use the MAGIC tool.

```bash
# in a seperate terminal enter the directory with def file 
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![image](https://github.com/user-attachments/assets/b521317e-3168-4ea5-849f-b6f785775069)

The magic tool
![image](https://github.com/user-attachments/assets/c2705fb1-834d-4b75-80e1-68866a0752fd)

![image](https://github.com/user-attachments/assets/7def29e5-f291-4b2e-90ae-d6dc193ad1c8)

![image](https://github.com/user-attachments/assets/cb09c9eb-0fa3-466a-b833-782b6978e7d6)
to get the cell details place cursuor on the cell and type **`s`** and enter **`what`** command in the tkon window

 Do "s" to select the element under the cursor
**Placement**

It involves determining the physical locations of standard cells or logic elements within a chip or block.
In order to start the placement we need to use the command 
```bash
 run_placement
```
![image](https://github.com/user-attachments/assets/fbd916a9-d36c-48ee-a58a-3f2e4ead3604)
```bash
#command to load picorv32a.placement.def file in magic
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/user-attachments/assets/8be1a905-9a70-4e49-8816-e316b8fac28d)
![image](https://github.com/user-attachments/assets/731b7c58-2a1b-43ba-a98a-1d8134cf06f2)
![image](https://github.com/user-attachments/assets/8f8d96cf-e0c2-4aee-b24b-c43354c73673)







## Day3 - *Design library cell using Magic Layout and ngspice characterization*

## lab 3

- Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow.](https://github.com/nickson-jose/vsdstdcelldesign).

```bash
# Enter the Openlane work dir
/Desktop/work/tools/openlane_working_dir/openlane

# Clone the repo with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign.git

# Enter repo directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

```
![image](https://github.com/user-attachments/assets/9d72c070-b6b9-4f1c-8e2b-a4291af73921)

```bash
# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
![image](https://github.com/user-attachments/assets/465b87dd-4619-436a-a9a8-a80857f0c662)


## Day4 - *Pre-layout timing analysis and importance of good clock tree*









## Day5 - *Final steps for RTL2GDS using tritonRoute and openSTA*


