# pes_pd
## DAY 1
### Inception of open-source EDA, OpenLANE and Sky130 PDK
<details>
<summary> How to talk to computers </summary>
  
**Introduction to QFN-48 Package, chip, pads, core, die and IPs**

How computers work
* An Arduino board is a well-known open-source electronics platform that encompasses a microcontroller and a development environment.
* It represents a compact computing chip responsible for executing instructions and managing the operations of your electronic project.
* The functionality of Arduino boards revolves around enabling you to create and upload code that dictates how the microcontroller on the board behaves.

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/74ac0bd8-41ad-425a-9b16-9b66bfe2271e)

The arduino can be designed as board like:

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/2f2197ba-eebc-4025-941d-22e4a893e033)

* When we examine the IC, it resembles an image referred to as a "chip," although it's technically known as a "PACKAGE."
* These packages are assigned names, such as "QFN-48," and there are various package types available with different configurations.
* The specific pin locations for this package are determined by the Arduino board.
* The size of the package is 7mm x 7mm.
* The chip itself, positioned in the center of the package, is the primary processing unit. It is connected to the package using a method called "wire bonding," facilitating the transfer of signals from external sources into the chip.
* Opening the chip reveals multiple components, including "PADs," which are like metal connectors on the chip's bottom.
* These PADs link the chip to a circuit, allowing external signals to enter for processing.
* The open space within the chip is known as the "Core." This Core functions as the chip's brain, responsible for most of the thinking and information processing.
* It houses digital logic elements such as AND gates, OR gates, and MUXs.
  
* The chip itself, known as the "Die," is the heart of a computer chip. It's a small, flat piece of silicon containing the electronic circuits where critical computations and operations occur. It's manufactured on a "Silicon Wafer."
* The typical Core of a CHIP consists of components like SoC (e.g., RISC-V SoC), SRAM, ADCs, DACs, PLL, SPI, and other elements.
* Collectively, SRAM, ADC, DAC, PLL, and others are referred to as "Foundry IP's" (Intellectual Properties).
* "Foundry" is a pivotal term in chip design, as it refers to the place where chips are manufactured. Foundries encompass machines used in chip production.
* The digital blocks situated within the SoC and the SPI interface are commonly termed "Macros."

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/7b63d0f5-53be-404d-8ad6-4b8bb52c661f)

**Introduction to RISC-V**

Definition of RISC-V:
* RISC-V, known as "RISC-V instruction set architecture" or "ISA," is a language of computing that facilitates communication with computers.
* It operates as an open-source instruction set architecture (ISA) founded on well-established principles of reduced instruction set computing (RISC).
Understanding Instruction Set Architecture (ISA):
* ISA encompasses the instructions a computer's processor can execute, essentially defining its capabilities.
Execution Flow for C Programs on Hardware:
* To execute a C program on specific hardware with a particular layout (e.g., qFlow), a specific flow is followed:
  * The C program is initially compiled into its corresponding assembly language program, which utilizes RISC-V assembly language.
  * This assembly language program is further transformed into machine language, represented as binary code (1's and 0's), understood by the hardware.
  * Although represented in hexadecimal in this context, it is eventually converted into binary format.
  * These binary instructions are then executed within the hardware layout to produce the desired output.
  * An intermediary layer between the C program and the layout is the "HDL" (Hardware Description Language).
  
Definition of HDL:
* HDL stands for "Hardware Description Language."
* It is a specialized programming language employed to articulate the structure and behavior of electronic circuits and systems.
* HDLs play a pivotal role in the design, simulation, and synthesis of digital circuits, including those within microprocessors, memory chips, and integrated circuits.
Types of HDLs:
* There are two primary types of HDLs:
  * Verilog:
    * Developed by Phil Moorby and Prabhu Goel in the 1980s.
  * VHDL (VHSIC Hardware Description Language):
    * Developed by the U.S. Department of Defense in the 1980s.
Implementation of RISC-V Specifications:
* To realize RISC-V specifications effectively, the use of RTL (Register-Transfer Level) is essential.
* In the presented context, the RTL used is the picorv32 CPU core, which serves as an implementation of these RISC-V specifications.
RTL-GDS Flow:
* The utilization of RTL facilitates the implementation of RISC-V specifications.
* The transition from RTL to GDS (Graphics Data System) marks the progression in the design flow, ensuring that the chip's physical layout and manufacturing processes are aligned with RISC-V specifications.

**From Software Applications to Hardware**
* Apps: Application software is a type of computer software that is designed to perform specific tasks or functions for end-users.
* System software: System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs.
* Operating System: The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction.
* Compiler: A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.
* Assembler: An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.
* RTL: RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.
* Hardware: Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/43c4f8e8-d9b4-4d65-9285-64f5068b7b7a)

</details>
<details>
<summary> SoC Design and OpenLane </summary>
  
**Introduction to all Components of Open-source Digital ASIC Design**
To implement Digital ASIC design, several essential components are required. These components include RTL IP's (Register Transfer Level Intellectual Properties), EDA Tools (Electronic Design Automation Tools), and PDK data (Process Design Kit data).
What is PDK?
* PDK (Process Design Kit) is a set of files provided by semiconductor manufacturers.
* It helps designers utilize the manufacturer's fabrication process to create integrated circuits (ICs).
* PDK includes comprehensive information, models, and files specific to the manufacturer's process technology.
* Designers rely on PDK to develop and validate their designs for a particular manufacturing process.
What are EDA Tools?
* EDA (Electronic Design Automation) tools are software applications and utilities used in the design and development of electronic systems.
* These systems encompass integrated circuits (ICs), printed circuit boards (PCBs), and other electronic components.
* EDA tools are critical for designing and testing electronic hardware to ensure proper functionality before manufacturing.
* They automate various aspects of the design process, improving efficiency and reducing errors.
Open-source Digital ASIC Design Components
For open-source Digital ASIC Design, three key elements are crucial:
* RTL IP's: These can be sourced from open repositories such as librecores.org, opencores.org, and GitHub, among others.
* EDA Tools: Open-source EDA tools like qflow, openROAD, and openLANE are available for design and validation.
* PDK: Open-source PDKs, like the Foss 130nm production PDK, provide the process-specific data necessary for designing ASICs.
Achieving 100% Open-source Digital ASIC Design
* The combination of RTL IP's, open-source EDA tools, and open-source PDKs enables the realization of 100% open-source Digital ASIC design.
ASIC Design Flow
* The methodology for open-source Digital ASIC Design is implemented through a structured flow.
* This flow involves a software tool known as "RTL to GDS2."
* The primary objective of the ASIC Design Flow is to take the design from RTL (Register Transfer Level) and convert it into the GDS2 format, which is used for the final layout of the ASIC.

**Simplified RTL to GDS2 Flow**
The simplified RTL to GDS2 flow is a sequence of major implementation steps for designing an Application-Specific Integrated Circuit (ASIC). It starts with an RTL (Register Transfer Level) model and ends with a fabricated masked set layout in the GDS2 format.
1) Synthesis:
* The first step involves synthesis, where the RTL design is translated into circuits composed of components from a standard Cell Library (SCL).
* The result is a gate-level netlist described in Hardware Description Language (HDL), functionally equivalent to RTL.
* Cells from the library have regular layouts, with variable cell widths but discrete sizes.
* Different EDA tools use various views of these cells, including electrical models, HDL, SPICE, and layout views.
3) Floor Planning and Power Planning:
* In this step, you perform floor planning and power planning based on whether you are implementing a single component (macro) or the entire chip.
* The goal is to plan the silicon area and create a robust power distribution network to supply power to the circuits.
* In chip floor planning, the chip die is partitioned between different chip components.
* In macro floor planning, you define the macro's dimensions, pin locations, routing tracks, and rows for later placement and routing steps.
* Power planning involves constructing a power network, often using multiple VDD and ground pins connected to components through power rings and metal power straps.
3) Placement:
* Placement is the third step and involves placing the gate-level netlist cells on vertical rows.
* Connected cells must be placed close to each other to reduce interconnect delays and facilitate successful routing.
* Placement occurs in two steps: global placement and detailed placement.
* Global placement aims to find optimal positions for cells, which may not be legal and can result in overlaps or going off rows.
* Detailed placement minimally alters the positions obtained in global placement to make them legal.
4) Clock Tree Synthesis (CTS):
* Clock tree synthesis is the fourth step, focusing on routing the clock signals before routing other signals.
* It involves creating a clock distribution network to deliver the clock to all clock cells (e.g., flip-flops).
* The clock network resembles a tree, with the clock source as the root and clock elements as the leaves.
* CTS aims to minimize clock skew (arrival time differences) and latency, ensuring a synchronized clock across the design.
5) Routing:
* The fifth step is routing, where signals are routed after clock routing.
* Given the placements and a fixed number of metal layers, a valid pattern of horizontal and vertical wires is found to connect cells together.
* Routing tools use metal layers defined by the PDK, which specify thickness, pitch, tracks, and minimum width.
* Routers often use grid routing methods, breaking routing into global and detailed routing stages.
6) Sign-Off:
* The final step is sign-off, which includes various verifications.
* Physical verification checks include:
  * Design Rule Checking (DRC) to ensure the layout adheres to design rules.
  * Layout vs. Schematic (LVS) to verify that the layout matches the gate-level netlist.
  * Timing verification includes Static Timing Analysis (STA) to ensure that all timing constraints are met, and the circuit operates at the designated clock frequency.
This simplified RTL to GDS2 flow is a fundamental process for designing ASICs, ensuring that the design is correctly synthesized, placed, routed, and verified before fabrication.

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/c3ccad88-3f26-4899-966c-da72a11a924d)

**Introduction to OpenLANE and Strive Chipsets**
What is OpenLANE?
OpenLANE is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow and toolchain that aims to automate the process of designing and manufacturing custom silicon chips. It was primarily developed by efabless, an open-source semiconductor company, and it is part of the Google/Skywater 130nm PDK (Process Design Kit) based ASICs.
* OpenLANE started as an open-source flow for a true open-source tape-out experiment.
* It is designed to produce a clean GDS2 with no human intervention, ensuring no LVS violations or DRC violations.
* OpenLANE is tuned for the SkyWater 130nm Open PDK and also supports XFAB180 and GF130G.
* It offers both autonomous and interactive modes of operation.
* OpenLANE can be used for hardening macros and chips.
* It includes Design Space Exploration to find the best flow configuration.
Strive Chipsets
* Strive is a family of SoCs (System-on-Chips) that are part of the open-source movement.
* It encompasses open PDKs, open EDA (Electronic Design Automation) tools, and open RTL (Register Transfer Level) designs.
* The Strive family includes various members designed for different applications and use cases.
* While specific Strive chipset details are not provided here, they are part of the broader open-source hardware ecosystem promoting transparency and accessibility in chip design.
The OpenLANE ASIC design flow comprises several steps, ensuring a comprehensive and automated approach to designing custom silicon chips. Key components and steps in the OpenLANE flow include:
* Design RTL: The flow starts with the RTL design, which serves as the input.
* Synthesis: The RTL design is synthesized using Yosys, translated into a logic circuit, and optimized.
* Design Exploration: Utilities are used to sweep design configurations and select the best strategy.
* Testing Structural Insertion (Optional): DFT tools are used for test structure insertion.
* Physical Implementation: OpenROAD handles placement, clock tree synthesis, routing, and LEC.
* Antenna Diode Insertion: Prevents transistor gate damage during fabrication.
* Sign-Off: Includes static timing analysis, design rule checking, and Layout vs. Schematic.
Throughout the design flow, OpenLANE relies on open-source projects and tools to automate and optimize the ASIC design process, resulting in a clean GDS2 output ready for fabrication.
</details>
<details> 
<summary> Get familiar to open-source EDA tools </summary>
Skywater-130 PDK and OpenLane Project
  
**Skywater-130 PDK**
* The Skywater PDK files used in this project are located under `$PDK_ROOT`.
* They encompass various components:
  *  `Skywater-pdk`: Contains all foundry-provided PDK-related files.
  * `Open_pdks`: Includes scripts bridging the gap between closed-source and open-source PDKs for EDA tool compatibility.
  * `Sky130A`: Houses the open-source compatible PDK files.
**Invoking OpenLane**
* To initiate OpenLane, a key script is `flow.tcl`, which executes the design processes.

**Importing Package**
* Running `package require openlane 0.9` is necessary to import the required software dependencies into the OpenLane tool.

**Designs in OpenLane and Hierarchy in a Design**
* OpenLane comprises various design-related components:
* `Src folder`: Contains Verilog files and SDC (Synopsys Design Constraints) files.
* `Config.tcl files`: These hold design-specific configuration switches utilized by OpenLane.

**Prepare the Design for the Flow**
* Prepare the design for the flow using the command: `prep -design <design_name> -tag <tag>`.
* This stage creates a "runs" directory where all the results will be stored.

**Synthesis**
* Synthesis is a critical step in the ASIC design process.
* It can be initiated using the command: `run_synthesis`.
* One essential early task is to calculate the flop ratio, which is the ratio of the number of D flip-flops to the total number of cells.

</details>

## Day 2
### Good floorplan vs bad floorplan and introduction to library cells
<details>
<summary> Chip Floor planning considerations </summary>
  
**Floor Planning Considerations**
* When designing integrated circuits, floor planning is a critical step that involves defining the layout and placement of various components.
* Here are some key considerations and steps in the floor planning process.

1. Define Width and Height of Core and Die
- The "die" refers to the entire semiconductor chip, including the core, I/O pads, and additional features.
- The "core" is the central area of the chip where most of the active circuitry resides, such as CPU, GPU, memory, and logic components.

2. Utilization Factor
- Utilization factor is a crucial metric in floor planning.
- It measures the ratio of the area occupied by the actual components to the total available area.
- High utilization factors indicate efficient space usage.
![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/68c095d1-c702-48a4-8bc4-cb3aaebcfc95)

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/9f5bc198-739e-411f-beac-14d5478025e7)

3. Location of Pre-Placed Cells
- Pre-placed cells are specific blocks or cells (e.g., memories, clock gating cells) manually placed by the designer before automated placement tools are used.
- These cells have predetermined locations to optimize placement.

4. De-coupling Capacitors
- De-coupling capacitors are essential in large circuits to mitigate voltage drops and noise.
- They store and discharge electrical energy quickly to filter high-frequency noise and transient voltage fluctuations.

5. Power Planning
- Proper power planning lowers noise in digital circuits caused by voltage droop and ground bounce.
- Robust power distribution networks (PDN) with numerous power strap taps are necessary to reduce resistance in the PDN.

6. Pin Placement
- Pin placement optimization minimizes buffering and enhances power consumption and timing.
- HDL netlists are used to determine where specific pins should be placed.
- Common pins are connected efficiently.

Steps to Run Floorplan using OpenLANE
1. Run floor planning in OpenLANE using the command: `run_floorplan`
2. Navigate to the directory: `` ../openlane/designs/picorv32a/runs/11-09_17-53/results/floorplan``
3. Use the command: `` magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def ``

[Insert Screenshots of Running OpenLANE and Floorplan]

Layout
- Include images showcasing the overall layout and zoomed-in views.

[Insert Layout Images Here]

Standard Cells
- Display images of standard cells used in the design.

[Insert Standard Cells Image Here]

</details>
<details> 
<summary> Library Binding and Placement </summary>
  
1. Bind the netlist with physical cells
Library consists of cells, sizes of cells, various flavours and shapes of the cells, Timing, Power and delay information.
Now, we have the floorplan, netlist and representation of components of netlist in library
place all the components such that the timing is not disturbed and distribute them properly.
2. Optimize Placement
Some components may be located very far to their inputs which can disturb signal integrity (as wire length increases, RC value increases). Therefore we use repeaters(may be series of buffers) inorder to avoid signal loss but area loss comes into picture.
Assuming that all the clock signals are working at ideal rate, we do the timing analysis if the current placement works good.
3. Placement
`run_placement`

![image](https://github.com/shreyakotagal/pes_pd/assets/117657204/2e10b688-78f6-4501-91bb-cdbc019ccb7f)

</details>
<details>
<summary> Cell design and characterization flows </summary>

Inputs for cell design flow

Cell design flow refers to the process of creating and optimizing individual digital logic cells that are part of a standard cell library. These libraries contain a set of pre-designed, characterized, and reusable logic gates, flip-flops, and other basic building blocks used in the design of integrated circuits. These libraries include PDK, DRC and LVS rules, SPICE models, libraries, user-defined specifications. User derfined specifications like Pin location, drawn gate lenght are added to the libarary by the library developer.

Circuit Design

Circuit design:Implment function using nmos and pmos and then derive the network graph. Derive the Euler's path and stick diagram from the graph.

Layout design Convert stick diagram according to the DRC rules Extraction of parasitics,extracted spice list

Characterization timing ,noise power.libs functions Read in the models and tech files and generate extracted spice Netlist. Read the subcircuits and attach power sources. Apply stimulus to characterization setup, provide neccesary output capacitance loads and provide neccesary simulation commands.

</details>
<details>
<summary> General Timing Characterization Parameters </summary>

Timing Threshold Definitions
In digital circuit design, timing thresholds are critical parameters used to measure signal characteristics and performance. Here are some key timing threshold definitions:
* **slew_low_rise_thr:** The threshold is set at 20% from the bottom power supply voltage when the signal is rising.
* **slew_high_rise_thr:** The threshold is set at 20% from the top power supply voltage when the signal is rising.
* **slew_low_fall_thr:** The threshold is set at 20% from the bottom power supply voltage when the signal is falling.
* **slew_high_fall_thr:** The threshold is set at 20% from the top power supply voltage when the signal is falling.
* **in_rise_thr:** Represents the 50% point on the rising edge of the input signal.
* **in_fall_thr:** Represents the 50% point on the falling edge of the input signal.
* **out_rise_thr:** Represents the 50% point on the rising edge of the output signal.
* **out_fall_thr:** Represents the 50% point on the falling edge of the output signal.
These parameters play a crucial role in calculating factors such as propagation delay and transition time, which are essential for assessing signal behavior and performance in digital circuits.
* **Propagation Delay:** Propagation delay is calculated as the time difference between the output threshold (out_thr) and the input threshold (in_thr).
  * Propagation delay=time(out_fall_thr)-time(in_rise_thr)
* **Transition Time:** Transition time is calculated as the time difference between the high slew rate threshold (slew_high_rise_thr) and the low slew rate threshold (slew_low_rise_thr). It measures how long it takes for a signal to transition between logic levels during its rise.
  * Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)
These timing thresholds and calculations are fundamental in ensuring that digital circuits meet their specified performance criteria and timing constraints.

</details>

## DAY 3
###  Design library cell using Magic Layout and ngspice characterization

