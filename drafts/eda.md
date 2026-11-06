# EDA

EDA is located in the Bottom layer of IoT 3-layer hierarchy: Perceive/Sensor layer. In this course, we learned how to build a real PCB to implement the previous courses: MCU, ARM Arch. and Sensor Principle…

Basically, what i learned in this course can be generalized to a process: 

Create Component Library → Design the schematic and ERC → Export Netlist and BOM → Design the PCB and DRC → Export manufacturing files and order → Assembly & Solder the PCB

We did that with LC-EDA platform.

### Create the Component Library

The EDA platform has built-in standard component library, but sometimes the components needed do not exist, so we need to create our own component library and customized component. 

To create the component in our own library, we need to design the Schematic Symbol and PCB Footprint according to the Datasheet of needed component. And then map them as a new component. 

We took the experiment that create the component library and created the component of CC2530F256 according to the TI datasheet. The package is QFN-40.

### Design the Schematic and ERC

Then, we need to design the schematic. Schematic is a logical chart showing the connective relation b/t the components. 

The experiment we took is the designation of STM32F103 minimum system board. We placed the MCU, power module, crystal module and interface module on the schematic. Then adjust the net label and no-connect label to implement the logical connection of the components.

After that, we took the ERC(electrical rule check) to detect the electrical errors.

Then, we exported the netlist file for designation of PCB and BOM for purchase of materials.

### PCB Layout

Then create the PCB based on the Netlist file, place the components modularly and route them. 

We export the netlist file of the former STM32 minimum system board schematic. And then create the PCB based on that. 1st, we adjusted the mechanical layer: the outline and the 4-layer board: signal, PWR, GND, signal. 2nd, we place the components functionally. 3rd, we route according to the air wires. 1. signal & power trace width 2. 45-degree angles. 4th, apply the GND copper pour. 5th. DRC check: detect the design errors.

### Export the manufacturing file and order

This is the last step of designation: export the Gerber file and order the PCB from manufacturer. We ordered the PCB from JLCPCB. 

### Solder

As we received the PCB, we sent the BOM to our professor and she prepared the materials we needed. Then, we tried to solder the components onto the PCB. We adopted 2 diff. soldering techniques: THT (Through-Hole) and SMT (Surface Mount). And as we finished the soldering of components, the PCB is done.