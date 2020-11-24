# VSD-Beginner-Physical-Design-workshop
An informative workshop on Beginner Physical Design using Open-source EDA tools organized by VSD(VLSI system Design) Corp. It provides an hands-on experience to understand ASIC implementation steps from RTL to GDSII using open source EDA tools and tsmc 180nm process design kit. The workshop is organized in a very lucrative fashion to give a complete understanding of  SoC design flow from device physics point of view to real time implementation. The course structure is designed with day by day content in a progressive way of understanding and learning .
## Contents :
- Introduction to RISC-V architecture design specification

- Day 1: SoC Design and familiarity to open source eda tools

- Day 2: Chip floorplan and Introduction to Library Cells

- Day 3: Design and Characterization of cells using Magic Layout tool and ngspice

- Day 4: Timing Analysis using OpenSTA, Clock Tree Synthesis and Signal Integrity

- Day 5: Routing and SPEF Extraction

## Day 1:
Day 1 workshop is organized to give introduction about the design on web based linux virtual machine and introduction of EDA tools used at various stages of design flow.  
The learning platform is divided in two sections - 1. Learners corners, which gives labs instances to perform various tasks related to design flow 
                                                   2. Assessments - which gives access to multiple question based on learning .
### Topics covered in day 1:
- Introduction to RISC V SOC architecture - packeage, chip/ die specifications like pads, core(picorv32)
- Introduction to The Raven Chip - Raven soc, I/O's, Macros,IP's.
- preparation for qflow and synthesis 
  RISC-V ISA Introduction :
  Very well presentation of the conversion of the high level language code to machine code using complier and assembler with the help of pictorial depiction.
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

### work done on 1 :
git clone https://github.com/kunalg123/vsdflow.git  this is done to clone the vsdflow repo from github, vsdflow contains all the required dirctories required for the design flow
- commands used to use this vsdflow repo are as:
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

