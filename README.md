# VSD-Beginner-Physical-Design-workshop
An Informative workshop on Beginner Physical Design using Open-source EDA tools organized by VSD(VLSI system Design) Corp. It provides an hands-on experience to understand ASIC implementation steps from RTL to GDSII using open source EDA tools and tsmc 180nm process design kit. The workshop was organized in a very lucrative fashion to give a complete understanding of  SoC design flow from device physics point of view to real time implementation. The course structure is designed with day by day content in a progressive way of understanding and learning .
## Contents :
- Introduction to RISC-V architecture design specification

- Day 1: SoC Design and familiarity to open source EDA tools

- Day 2: Chip floorplan and Introduction to Library Cells

- Day 3: Design and Characterization of cells using Magic Layout tool and ngspice

- Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis and Signal Integrity

- Day 5: Routing and SPEF Extraction

## Day 1:
Day 1 workshop was organized to give introduction about the design on web based linux virtual machine and introduction of EDA tools used at various stages of design flow.  
The learning platform is divided in two sections - 1. Learners corners, which gives labs instances to perform various tasks related to design flow 
                                                   2. Assessments - which gives access to multiple question based on learning .
                                                   
- Introduction to RISC V SOC architecture - packeage, chip/ die specifications like pads, core(picorv32)
- Introduction to The Raven Chip - Raven SoC, I/O's, Macros,IP's.
- Preparation for qflow and synthesis 
  RISC-V ISA Introduction :
  Very well Presentation of the conversion of the high level language code to machine code using complier and assembler with the help of pictorial depiction.
  RIS-V based SoC is introduced -Raven and picoSoC
  Implementation of the RISC-V can be done by RTL coding using HDL's( Verilog,VHDL) and then its physical implentation can be done using backend of ASIC flow( RTL to GDSII).
## EDA tools used in the deisgn flow:
- Yosys     - for synthesis
- Graywolf  - for placement
- Qrouter   - for routing
- Opentimer - for static timing analysis
- Magic     - for layout editor, extraction and DRC
- ngspice   - for circuit simulation (pre and post layout)
- qflow     - for RTL to GDSII Intergration
- virtualbox - to get linux environment on windows

### 
git clone https://github.com/kunalg123/vsdflow.git  this was done to clone the vsdflow repo from github, vsdflow contains all the required dirctories for the design flow
### Commands used to implement this vsdflow repo are as:
- cd vsdflow
- ./vsdflow spi_slave_design_details.csv
- ls -ltr outdir_spi_slave/
- after these steps lots of files are cretaed, to see the number of files, following command is used,
- ls -ltr outdir_spi_slave | wc

### Commands used to open qflow in gui are as :
- cd outdir_spi_slave
- qflow display spi_slave
- after these two steps two windows gets open - one for "layout1" and one for "tkcon" 
- to find the area of the layout, type "box" in the tkcon window.
![img1](https://user-images.githubusercontent.com/73484928/100149831-cba52e80-2ec4-11eb-8cf6-5977f0b7a4c1.png)
#### As we can see in the image area is 1542024 micron.
#### After this task, next lab task is to get introduced with 'picorv32' module in qlow .
### Commands used:
- cd vsdflow 
- mkdir my_picorv32 
- cd my_picorv32 mkdir source synthesis layout 
- cp ~/vsdflow/verilog/picorv32.v source/. 
- qflow gui &
#### after this gui window gets open, where we need to do some settings in qflow manager to run the synthesis and other flow properly. 
### Steps are as:
- Technology = osu018
- Verilog source file : picorv32.v
- Verilog module : picorv32
- Click set stop button on the setting window in qlow manager
- Click on the run button adjacent to preparation and synthesis 
#### After successful run of the synthesis, we could see the log file by clicking on the okay button at synthesis stage.
![img2](https://user-images.githubusercontent.com/73484928/100149833-cba52e80-2ec4-11eb-9f69-c4def72394ee.png)
#### During step task was to calculate the % ratio of DFF/logic cells
#### And the answer was : in between 12-13.99% as per the option given in the MCQ during assessment 

## Day 2:
- Chip floor planning 
- Library binding and placement
- Cell design characterization flows
- General timing characterization parameters 
### Chip Floorplaning :

 Topics covered in this part of day 2 of workshop were :
- Definition of width and height of core and die .
- Utilization factor and aspect ratio.
- Concepts of pre placed cells 
- Concept of decoupling capacitor and its usage in providing required voltage to cells for their proper functioning and to keep chip functionality proper.
- Power planning of the chip 
- Pin placement and logical cell placement blockage 

### Placement :
During this stage following were done as :
- Netlist binding with the initial place design using cell library that contains different flavours of a cell 
- Optimization of placement using estimated wire length and capacitance since routing has not done yet 
- After this step timing analysis is done with ideal clock since CTS has not done till this stage 

### Cell Design :
  It consists of three parts 
- Inputs - PDKs (Process design kits), DRC & LVS rules, SPICE models, library & user-defined specs.
- Design Steps Design steps - Circuit Design, Layout Design, Characterization. 
- Outputs -CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir), timing, noise, power.libs, function.

### Timing definition 
- Defintion of Threshold voltage of a cell and its propagation delay is covered and some tasks related to rise time, fall time, Threshold voltage calculation were also done .
- Important parameters of timing characterization were as :
- Rise Delay: Time taken for waveform to rise from 20% to 80% of VDD.
- Fall Delay: Time taken for waveform to fall from 80% to 20% of VDD.
- Propagation Delay: Measured between 50% of Input transition to 50% of Output transition.

### Commands used:
- cd vsdflow
- mkdir my_picorv32                    # to  create directory of  my_picorv32 module
- cd my_picorv32
- mkdir source synthesis layout   # to  create subdirectory source synthesis layout within my_picorv32 
- cp ~/vsdflow/verilog/picorv32.v source/. # to copy picorv32.v file into source directory
- qflow gui & 
#### after running  above commands, gui window of qflow gets open where we need to change some settings before running placement  like :
- Select technode osu018
- Select verilog module picorv32
- Set stop
- Prep: run
- Synthesis: run
- Placement settings: init. Density 0.7
- Arrange Pins: Auto Group and apply
- Arrange Pins: New Group and create my_pin_grouping for resetn and clk pins. Check only left box.

### Placement Settings in Qmanager 
![placementsetting](https://user-images.githubusercontent.com/73484928/100171459-cc51bb00-2eec-11eb-930e-3c16bc2ad44d.png)

#### After performing these settings, click on run to start placement which is shown as 
![img3](https://user-images.githubusercontent.com/73484928/100149835-cc3dc500-2ec4-11eb-8021-2bd47df6d7c4.png)
![img4](https://user-images.githubusercontent.com/73484928/100149838-ccd65b80-2ec4-11eb-9639-489e08cebd3f.png)
![img5](https://user-images.githubusercontent.com/73484928/100149841-ccd65b80-2ec4-11eb-8feb-3c5fe1acb518.png)
![img6](https://user-images.githubusercontent.com/73484928/100149844-cd6ef200-2ec4-11eb-8623-5c8bcf17734e.png)
#### Now to check the layout area of the above design following commands are used :
- cd
- cd vsdflow/my_picorv32
- qflow display picorv32 &
- This will open layout and tkcon window In the layout window, select whole chip using below steps
- Take cursor to bottom left
- Left mouse click
- Take cursor to top right
- Right mouse click
- Press Shift+i
#### This will select the whole layout Now in tkcon window, type below command
- Box

![img7](https://user-images.githubusercontent.com/73484928/100149847-ce078880-2ec4-11eb-9bbb-0fe9984f8709.png)
#### As we could see on image above, the area of the layout was '812062.19 microns.'


## Day 3:
- Spice deck Creation for CMOS Inverter and  Simulation using ngspice and magic tool
- Euler’s Path and stick diagram for layout 
- 16 mask process for CMOS Fabrication

### simulation using ngspice 
   - Spice netlist modeling for CMOS Inverter
   - Static behaviour of CMOS and its robustness
   - Dynamic behaviour and timing definition 
     1.Switching threshold voltage of inverter
     2.Propagation delay( defintion of rise time and fall time )
    
### Euler's Path and Stick diagram for Layout 
   - Importance of Euler's path in making layout with respect to routing resources
   - Relation between circuit design and its layout using stick diagram
   
### 16 Mask Process for CMOS Fabrication
  - Selecting a substrate.
  - Creating active region for transistors
  - N-Well and P-Well formation
  - Formation of ‘gate'
  - Lightly doped drain(LDD) formation
  - Source and Drain formation
  - Steps to form contacts and Interconnects(local)
  - Higher level metal formation
  ### 16 mask CMOS Fabrication
  
  ![fab](https://user-images.githubusercontent.com/73484928/100171431-ca87f780-2eec-11eb-8ae9-1f2c6ae78c2b.png)

  ### commands used:
  - git clone https://github.com/kunalg123/ngspice_labs.git  # to clone ngspice_labs 
  - cd ngspice_labs
  - cat inv.spice
  
  ![img8](https://user-images.githubusercontent.com/73484928/100149850-cea01f00-2ec4-11eb-83f9-88f1f0c7aac7.png)

  ### commands used for simulation of above spice netlist
  - cd ngspice_labs
  - ngspice inv.spice
  - ngspice 1 ->
  - run
  - setplot dc1
  - plot out in
  
  ![img9](https://user-images.githubusercontent.com/73484928/100149852-cea01f00-2ec4-11eb-9c06-83efcc3dcce5.png)
  
####  To make some modification in the spice netlist to observe changes in Vm of CMOS
  - leafpad inv.spice   # this will open up editor window 
  
  ![img11](https://user-images.githubusercontent.com/73484928/100149858-cf38b580-2ec4-11eb-84a0-ef33cb51a06b.png)
 
 ### Pre layout transient analysis
    1. spice netlist
    2. commands used to run transien analysis
    3. outwaveform
    4. timing defintion 
    
 ![timing def2](https://user-images.githubusercontent.com/73484928/100173554-c6f66f80-2ef0-11eb-9d9d-e322d471d35b.PNG)
 
 ![img13_a](https://user-images.githubusercontent.com/73484928/100149863-d069e280-2ec4-11eb-887a-2e1d600d7c03.png)
 
 ![img13](https://user-images.githubusercontent.com/73484928/100149861-d069e280-2ec4-11eb-9490-2908ea389cc6.PNG)

###  Post Layout Analysis
   - cd ngspice_labs
   - magic -T min2.tech  # to open magic layout window and tkcon window
   - source draw_fn.tcl  #  layout using tcl script
 
 ![img14](https://user-images.githubusercontent.com/73484928/100149865-d1027900-2ec4-11eb-9c91-d039e5d8f048.png)
 
 ![img15](https://user-images.githubusercontent.com/73484928/100149866-d19b0f80-2ec4-11eb-8e71-839470898097.png)
 
 ![img16](https://user-images.githubusercontent.com/73484928/100149869-d19b0f80-2ec4-11eb-92f5-ee10a3617946.PNG)
   
   
## Day 4:   
 - Timing modelling using delay table for a cell ( function of input slew and ouput capacitive load)
 - Clock tree synthesis
 - Concept of setup and hold time with real clock
 
### Delay Table of a cell with Different Drive strength 
![delay table](https://user-images.githubusercontent.com/73484928/100149824-c9db6b00-2ec4-11eb-8de1-c949595ecb97.png)

### CTS 
![cts1](https://user-images.githubusercontent.com/73484928/100149900-d65fc380-2ec4-11eb-8a2c-42874ec83131.png)

## H tree CTS
![cts2](https://user-images.githubusercontent.com/73484928/100149902-d65fc380-2ec4-11eb-997b-0923c1945324.png)

## CTS with Buffer
![cts3](https://user-images.githubusercontent.com/73484928/100149904-d6f85a00-2ec4-11eb-801b-cfc6d39ca37a.png)

## CTS with Crosstalk
![crosstalk](https://user-images.githubusercontent.com/73484928/100149897-d5c72d00-2ec4-11eb-9093-3a716e54b893.png)


## Shielding to prevent Crosstalk
![cts4](https://user-images.githubusercontent.com/73484928/100149909-d790f080-2ec4-11eb-9318-a27d7ca8c13b.png)


## Setup analysis with real clock
![setup](https://user-images.githubusercontent.com/73484928/100171467-ccea5180-2eec-11eb-8af0-c83c9caaf544.PNG)

## Hold analysis with real clock
![hold](https://user-images.githubusercontent.com/73484928/100171452-cc51bb00-2eec-11eb-988a-a7c7f02c16d4.PNG)
![placementsetting](https://user-images.githubusercontent.com/73484928/100171459-cc51bb00-2eec-11eb-930e-3c16bc2ad44d.png)

### Commands used for Prelayout Sta analysis with real clock :
  - /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib  # .lib path 
  - cd vsdflow/my_picorv32
  - leafpad picorv32.sdc      # to open .sdc file in editor for clock definition
  - create_clock -name clk -period 2.5 -waveform {0 1.25} [get_ports clk]
  - leafpad prelayout_sta.conf
  - read_liberty /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
  - read_verilog synthesis/picorv32.rtlnopwr.v
  - link_design picorv32
  - read_sdc picorv32.sdc
  - report_checks
  - sta prelayout_sta.conf

![img17](https://user-images.githubusercontent.com/73484928/100149871-d233a600-2ec4-11eb-9aba-56ac03aed93b.png)
  
  ## Slack at Prelayout stage is -0.5516
  
  
 ## Day 5:
  - Routing - Concept of Routing using Maze Algorthim
  - DRC     - Rules related to metal width, metal spacing, pitch, via sizing, via spacing 
  - Parasitic Extraction - Representation of R and C parasitics in form of SPEF file.
  - Pre and Post routing STA analysis
  
 ### MAZE Routing  
 ![maze](https://user-images.githubusercontent.com/73484928/100149873-d233a600-2ec4-11eb-944b-4cf3b72f19c6.png)
  
 ### Routing in Progress 
 ![rout1](https://user-images.githubusercontent.com/73484928/100149881-d364d300-2ec4-11eb-8040-9a0515a25f72.png)
  

 ### Routing Completion Report
 ![routing result](https://user-images.githubusercontent.com/73484928/100149890-d4960000-2ec4-11eb-84f0-0ce3bf711486.png)
 
 ###  Sucessful Routing 
 ![rout2](https://user-images.githubusercontent.com/73484928/100149885-d3fd6980-2ec4-11eb-838a-9248c12e6572.png)
   
   
 ### Pre Route Sta log
 ![pic32](https://user-images.githubusercontent.com/73484928/100149876-d2cc3c80-2ec4-11eb-8032-675b7cff90e5.PNG)
   
 ### Post Route Sta log
 ![pic33](https://user-images.githubusercontent.com/73484928/100149878-d364d300-2ec4-11eb-8236-be58437b3e67.PNG)
  
 ####  we could see the reduction in maximum clock frequency of 20Mhz after post Routing( because of the RC parasitics) .
  
 ## SPEF Representation :
   
 ![timing def](https://user-images.githubusercontent.com/73484928/100149895-d5c72d00-2ec4-11eb-85e4-28e3dc801762.PNG)
 
 ## Acknowledgements:
 - Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)
 - Nickson P Jose, Teaching Assistant (VSD Corp. Pvt. Ltd)
 
   
   
   
   
   
  
  

   







