# Rupesh-VSD-PD-Workshop
This is the repo containing all the documentations for VSD PD workshop. it uses OpenLane and Skywater 130nm


# Contents

- [Day 1 - Introduction to open-source EDA, OpenLANE and SKY130 PDK](#day-1---introduction-to-open-source-eda-openlane-and-sky130-pdk)
    1. [Basic IC Design Terminologies](#basic-ic-design-terminologies)
    2. [Introduction To RISC-V](#introduction-to-risc-v)
    3. [Introduction To RTL to GDSII Flow](#introduction-to-rtl-to-gdsii-flow)
    4. [List of Open Source Tools Used](#list-of-open-source-tools-used)
    5. [Google SkyWater130 PDK](#google-skywater130-pdk)
    6. [What is OpenLANE](#what-is-openlane)
    7. [Getting Started with OpenLANE](#getting-started-with-openlane)
        - [PDK Directory Structure](#pdk-directory-structure)
        - [OpenLANE Initialization](#openlane-initialization)
        - [Design Preparation](#design-preparation)
        - [Design Synthesis and Results](#design-synthesis-and-results)
 - [Day 2 - Good floorplan vs bad floorplan and introduction to library cells](#day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
    - [Chip Floorplanning](#chip-floorplanning)
      - [Utilization Factor and Aspect Ratio](#utilization-factor-and-aspect-ratio)
      - [Power Planning](#power-planning)
      - [Pin Placement](#pin-placement)
      - [Floorplan using OpenLANE](#floorplan-using-openlane)
      - [Review Floorplan Layout in Magic](#review-floorplan-layout-in-magic)
    - [Placement](#placement)
      - [Placement and Optimization](#placement-and-optimization)
      - [Placement using OpenLANE](#placement-using-openlane)
    - [Cell Design and Characterization Flows](#cell-design-and-characterization-flows)
      - [Cell Design Flow](#cell-design-flow)
      - [Characterization Flow](#characterization-flow)
  - [Day 3 - Design library cell using Magic Layout and ngspice characterization](#day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
    - [Importing Custom Inverter Design ](#importing-custom-inverter-design)
    - [CMOS Inverter Design using Magic](#cmos-inverter-design-using-magic)
    - [Extract SPICE Netlist from Standard Cell Layout](#extract-spice-netlist-from-standard-cell-layout)
    - [Transient Analysis using NGSPICE](#transient-analysis-using-ngspice)
  - [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
    - [Magic Layout to Standard Cell LEF](#magic-layout-to-standard-cell-lef)
      - [Importing custom LEF into synthesis flow](#importing-custom-lef-into-synthesis-flow)
    - [Timing Analysis using OpenSTA](#timing-analysis-using-opensta)
    - [Clock Tree Synthesis using TritonCTS](#clock-tree-synthesis-using-tritoncts)
  - [Day 5 - Final steps for RTL2GDS](#day-5---final-steps-for-rtl2gds)
    - [Generation of Power Distribution Network](#generation-of-power-distribution-network)
    - [Routing using TritonRoute](#routing-using-tritonroute)
    - [SPEF File Generation](#spef-file-generation)
  - [References](#references)
  - [Acknowledgement](#acknowledgement)

## Introduction To RTL to GDSII Flow
  RTL to GDSII Flow refers to the all the steps involved in converting a logical Register Transfer Level(RTL) Design to a fabrication ready GDSII format. GDSII is a database file format which is an industry standard for data exchange of IC layout artwork.
  The RTL to GSDII flow consists of following steps:
  - RTL Synthesis
  - Static Timing Analysis(STA)
  - Design for Testability(DFT)
  - Floorplanning / Powerplanning
  - Placement
  - Clock Tree Synthesis(CTS)
  - Routing
  - GDSII Streaming

#Day1 task:

## OpenLANE Initialization:

A custom shell script or commands can be generated to make the task simpler.

-To invoke OpenLANE run the ./flow.tcl script.
-OpenLANE supports two modes of operation: interactive and autonomous.
-To use interactive mode use -interactive flag with ./flow.tcl


flop ratio = (# D Flip-Flop) / (# cell)

           = 1613 / 14876
           
           = 0.1084
           
           = 10.84%

![image](https://user-images.githubusercontent.com/94752269/215266396-82641036-1ddd-456b-b492-0943c7df0797.png)

![image](https://user-images.githubusercontent.com/94752269/215266491-a19084c7-5f40-4a04-800c-9a4a272a9405.png)

#Day 2

Configuration precedance

openlane/designs/picorv32a/runs/29-01_08-22
![image](https://user-images.githubusercontent.com/94752269/215329406-83f0e76d-071e-4015-8e48-62c31f78c4ab.png)

openlane/configuration/floorplan.tcl

![image](https://user-images.githubusercontent.com/94752269/215328808-01451fb8-b6c2-4d36-bec4-40d2a3407b24.png)

openlane/designs/picorv32a/config.tcl

![image](https://user-images.githubusercontent.com/94752269/215329088-f114e240-d18c-467b-bff3-58d3a5a2b3e2.png)

openlane/designs/picorv32a/sky130A_sky130_fd_sc_hd_config.tcl

![image](https://user-images.githubusercontent.com/94752269/215329228-2d619ede-2fcb-4491-96a0-785f8a1380ec.png)

Floorplan def(design exchange file) file output:
![image](https://user-images.githubusercontent.com/94752269/215336194-a663e23d-e596-42d2-bd4d-f74a90dee468.png)

#Review floorplan layout in Magic

![image](https://user-images.githubusercontent.com/94752269/215336711-7f7465c3-dc98-4f44-b582-2e82408bcf27.png)

horizontal pin in metal layer 3
![horizonatal pin](https://user-images.githubusercontent.com/94752269/215338207-f2d8ab3e-8183-4d92-ac6d-3ca3d5f5db2e.png)

vertical pin in metal layer 2
![vertical pin](https://user-images.githubusercontent.com/94752269/215338087-0d1ae2e2-b429-476e-ba5f-7269926aad5a.png)

standard cell
![standard cell](https://user-images.githubusercontent.com/94752269/215338548-c47a02a2-0d48-4679-a4d8-43ae193a9626.png)

#cell placement in magic

![placement in magic](https://user-images.githubusercontent.com/94752269/215349113-f8450733-8d29-45cd-b18a-eddc6e6ce238.png)

#cmos inverter in magic
![inv_magic](https://user-images.githubusercontent.com/94752269/215521049-8a69b215-29e8-4733-ab0f-b6827b1c039d.png)

![nmos](https://user-images.githubusercontent.com/94752269/215521069-7443c2f2-14b1-43d8-b5a3-e49e68866426.png)
![pmos](https://user-images.githubusercontent.com/94752269/215521080-2fe3a9fe-24c2-4c46-ad80-43596f763984.png)

![inv_spice](https://user-images.githubusercontent.com/94752269/215521054-79871ddc-18ca-4f6f-9be0-b57f19fc4c18.png)

![inv_char_graph](https://user-images.githubusercontent.com/94752269/215557351-ddbb8b8c-0e91-4215-a287-d4c7d9cd0b60.png)


Using this transient response, we will now characterize the cell's slew rate and propagation delay:

Rise Time [output transition time from 20%(0.66V) to 80%(2.64V)]:
Rise Time = 2.24417 - 2.1828 = 0.0618 ns

Fall Time [ouput transition time from 80%(2.64V) to 20%(0.66V)]:
Fall Time = 8.09512 - 8.0679 = 0.02722 ns

Rise Delay [delay between 50%(1.65V) of input to 50%(1.65V) of output]:
Rise Delay = 6.15069 6.15 = 0.00069 ns

Fall Delay [delay between 50%(1.65V) of input to 50%(1.65V) of output]:
Fall Delay = 8.07770- 8.05075 = 0.02695 ns

The characterization done above was done at 27 C.


