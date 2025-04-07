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


After extracting the SPICE file, we need to update it according to the design.

![image](https://github.com/user-attachments/assets/c5832f19-5c39-4ac1-85c1-b92479db6a3c)


```bash
#To run the SPICE file using ngspice tool
ngspice sky130_inv.spice

# To load the plot
plot y vs time a
```
![image](https://github.com/user-attachments/assets/c25c59d6-b431-45be-be0e-fd88d4109cca)

![6 all delay calculation](https://github.com/user-attachments/assets/5024f8d4-524d-4500-88b7-8475bb4d1d44)
```math
Rise\  time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%
```
```math
20\%\ of\ output = 0.66\ V
```
```math
80\%\ of\ output = 2.64\ V
```


```math
Rise\  time = 2.205 - 2.164 = 0.041\ ns 
```




```math
Fall\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```
```math
Fall\ time = 8.068 - 8.040 = 0.028\ ns
```



```math
Propagation\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```



```math
Propagation\ Delay = 2.185 - 2.15 = 0.035\ ns 
```



```math
Cell\ Fall\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%
```


```math
50\%\ of\ 3.3\ V = 1.65\ V
```



```math
Cell\ Fall\ Delay = 4.05467 - 4.04998 = 0.00469\ ns 
```


```bash
#Download the drc_test folder in home directory
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

#To extract the labs from the zip file
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -lrt

# Command to view .magicrc file
gvim .magicrc

#To open magic tool
magic -d XR



```
![image](https://github.com/user-attachments/assets/227beae4-08e7-422b-bcd5-18bee720f89f)
![image](https://github.com/user-attachments/assets/1b933219-ba32-437e-9e14-cd4c770f7d46)

```bash
#The metal 3-filled area will be associated with the VIA2 mask.
cif see VIA2
```
![image](https://github.com/user-attachments/assets/5a9018b1-5bd9-4ccf-a3ec-0e92284d5b63)

- open the ploy.mag file. use the below command in tkcon window
```bash
load poly.mag
```
![image](https://github.com/user-attachments/assets/a40d958c-6c9d-49d3-ac4b-d29fdb77f714)

![image](https://github.com/user-attachments/assets/58e93d4d-43e8-429b-9e8f-5d2459733c8e)


- Insert new commands in sky130A.tech file to update drc

![image](https://github.com/user-attachments/assets/5a3ef36a-c7a3-42d8-b64c-6ee22008e8a8)

![image](https://github.com/user-attachments/assets/efc428c4-d556-4478-bb97-4dc03952fc50)


```bash
 # Loading updated tech file
   tech load sky130A.tech

 # Must re-run drc check to see updated drc errors
  drc check

 # Selecting region displaying the new errors and getting the error messages 
  drc why
```
![image](https://github.com/user-attachments/assets/def5b7de-6fb7-46bb-be9e-e6af03113d11)


![image](https://github.com/user-attachments/assets/4a678cf6-043a-426d-8301-0550bc982556)

![image](https://github.com/user-attachments/assets/af9a8f32-d71b-4f50-b032-7812ef026fd9)




- Incorrectly implemented nwell.4


![image](https://github.com/user-attachments/assets/043000ad-4f67-4486-b673-47bc1dbead18)


- New commands inserted in sky130A.tech file to update drc
![image](https://github.com/user-attachments/assets/68e3d1c3-6d35-4254-bca9-aa8f9bf214a0)




![image](https://github.com/user-attachments/assets/8aaa07e6-d435-4966-89ee-cbccd3dd663f)






## Day4 - *Pre-layout timing analysis and importance of good clock tree*


Screenshot of tracks.info of sky130_fd_sc_hd

![image](https://github.com/user-attachments/assets/1ceb887e-7388-44e2-a89c-30fe77dc2285)


Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

```
![image](https://github.com/user-attachments/assets/b0b9ae0f-da4c-4ad6-9165-4419e0995230)

Commands for tkcon window to set grid as tracks of locali layer
```bash

# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um


```



![image](https://github.com/user-attachments/assets/687be951-a2bc-4551-8003-f01b2828f0ef)

```bash
#to write lef file
lef write
```
- Now we can open the LEF file and go through it.

![image](https://github.com/user-attachments/assets/b0dcafb6-9b25-4205-8404-a726037b2efe)

- Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
![image](https://github.com/user-attachments/assets/7899addb-3357-4685-86fb-98d102b20951)

- Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
```bash
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]


````
![image](https://github.com/user-attachments/assets/4367005d-093d-411c-ae06-23b19246a19f)

- Run openlane flow synthesis with newly inserted custom inverter cell.
```bash
# Open the openlane terminal
cd Desktop/work/tools/openlane_working_dir/openlane

docker

./flow.tcl -interactive

# Inside openlane terminal

# below cmd to be used to overwrite previous run data 
prep -design picorv32a -tag 28-03_10-01 -overwrite 

# Cmds to include the new cell led in merged.lef in /tm[ folder
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

run_synthesis

```
![image](https://github.com/user-attachments/assets/255f474f-62b7-4dec-b2b3-b6c29cfbf1e5)

```bash
# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled , if enabled =1
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING, if enabled =1
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)


```
![image](https://github.com/user-attachments/assets/738a2d7e-a1a6-41a7-9dfd-7973b9ba7230)

```bash
run_synthesis
```
![image](https://github.com/user-attachments/assets/a47e832a-c0e0-4ecd-9760-1199fa870842)

Comparing to previously noted run values area has increased and worst negative slack has become 0

- Now run Floor plan

```bash
#insted of run_floorplan

init_floorplan
place_io
tap_decap_or



```
![image](https://github.com/user-attachments/assets/2e86f718-381c-4118-86b9-18e094c3bb5d)


```bash
run_placement
```

- Open the layout using MAGIC tool to see is our inverter is inserted into the picorv32 design

```bash
# enter the dir of design
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/28-03_10-01/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/user-attachments/assets/ab3b9fd4-51c1-4fa1-8ac1-6e034adf170d)


![image](https://github.com/user-attachments/assets/b1823817-a7f3-48e7-94b3-0a7b372a8679)

![image](https://github.com/user-attachments/assets/fec37c62-75a1-4324-aac6-665b6fdf3293)
```bash
#command to view internal connectivity layers 
expand
```
![image](https://github.com/user-attachments/assets/1919ea44-c6cb-41bc-a96b-4f3881171712)

- Newly created pre_sta.conf for STA analysis in openlane directory

![image](https://github.com/user-attachments/assets/5358bbe1-1eb5-487a-b001-067051f1c8c9)

- Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the file openlane/scripts/base.sdc

  ![image](https://github.com/user-attachments/assets/a1f98a8f-ba6e-4dbc-9421-984186142fe3)

Commands to run STA in another terminal
```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
![image](https://github.com/user-attachments/assets/bb16e4c1-9f58-48b0-a28e-aa9b75d3c7a4)

![image](https://github.com/user-attachments/assets/5d7fbe63-7a6e-4280-a3cf-6e46af775792)

![image](https://github.com/user-attachments/assets/3240dc11-585b-4147-be53-874ae0b2ccf1)

![image](https://github.com/user-attachments/assets/adc95805-37aa-4e04-88a6-312bc67fb409)

![image](https://github.com/user-attachments/assets/d63da4fe-6bc9-4e38-9251-db7ddbc98dbc)

- Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

```bash
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 28-03_10-01 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis



```
![image](https://github.com/user-attachments/assets/03ab9c99-756b-4786-b9e1-533d6a6c1f4d)


- Again run STA

```bash
sta pre_sta.conf

#Reports all the connections to a net
report_net -connections _00293_

#To replacing cell
replace_cell _33213_ sky130_fd_sc_hd__mux2_2

#To generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```
![image](https://github.com/user-attachments/assets/2bdb733d-2b2e-492c-8d49-7b065faef43b)

![image](https://github.com/user-attachments/assets/3143a6e1-16be-41c4-a510-b5741affbf42)

**`slack has reduced to -4.5889 from -4.62`**

![image](https://github.com/user-attachments/assets/4d15501e-6381-476b-9ecc-7cb339a63a63)
![image](https://github.com/user-attachments/assets/23c1d078-c581-4fc2-9445-6e27f4ae0e64)

**`slack has reduced to -4.0255 from -4.5889`**

- to check the timimg through a cell we changed

```bash
report_checks -from _35312_ -to _35239_ -through _22284_
#Generating custom timing report


```
![image](https://github.com/user-attachments/assets/2a10f8e2-a3c2-4560-a212-892ccdd9b7a7)


- Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/28-03_10-01/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

```
- Commands to write verilog

```bash

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/28-03_10-01/results/synthesis/picorv32a.synthesis.v

```

![write verilog](https://github.com/user-attachments/assets/8d507920-6f08-43bf-b085-7bf6a238b052)

![picorv32a synthesis](https://github.com/user-attachments/assets/dc6723f7-fedf-4354-8b9e-7d6003805071)

- Run following commands in the opelane flow

```bash

# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 28-03_10-01 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

#Command to set new max fanout
set ::env(SYNTH_MAX_FANOUT) 4


# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts

```

![21 running synthesis](https://github.com/user-attachments/assets/6d8e989c-fc91-46e6-9ea4-eb6391611b4f)

![23 run cts](https://github.com/user-attachments/assets/4d20b2bb-f193-4ba7-b82b-aab5a366957e)

![23 ct 1](https://github.com/user-attachments/assets/cc40a720-a582-40a3-8c28-1767c62616f6)

![23 cts 2](https://github.com/user-attachments/assets/b11bece0-e0f4-458e-acff-048ef7dbabfe)




**`Hold slack`**
![image](https://github.com/user-attachments/assets/b813f918-fe2e-47ef-82cc-b710c98155dd)

**`Setup slack`**
![image](https://github.com/user-attachments/assets/c8a2b3ba-62aa-467d-825f-c336e17ee1fe)


```bash

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Setting def as placement def otherwise, we get clock not found error
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/28-03_10-01//results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/28-03_10-01//tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/28-03_10-01//results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/28-03_10-01//results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit


# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)


```

![25 openroad commands](https://github.com/user-attachments/assets/4f126c48-778c-42b0-8e25-6be8e39684b8)


![25 openroad](https://github.com/user-attachments/assets/d7f00cfe-43b2-409a-b79c-4b2b038256cc)



**`Hold Slack`**
![image](https://github.com/user-attachments/assets/6ea1c350-5610-48ef-b58d-dc228018c7ca)

**`Setup Slack`**
![image](https://github.com/user-attachments/assets/27fb123a-0945-4965-9a1f-533dac2836fc)




## Day5 - *Final steps for RTL2GDS using tritonRoute and openSTA*


