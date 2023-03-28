# RTL-LOGIC-GATES
Resistor-Transistor Logic based Logic Gates

### Description
The purpose of this project is building logic gates out of readily available components without using any ICs. The Logic Gates are built out of discrete components and mirror the structure and behaviour of classical Resistor Transistor Gates.

### Design constraints
The logic gate circuits must:
1.  Be powered by a 5V supply voltage from a USB port
2.  Interface with a Arduino Uno for input signal at logic gate ports
3.  Occupy a limited PCB footprint 

### Timeline of the Project and Design Stages

1.  Researching the basic operating principles of RTL Logic
2.  Solving by hand a discrete NPN transistor switch problem 

3.  Basic computer aided circuit analysis for RTL Logic Gates
    * Building and analysing the circuit of a NPN transistor **switch** in ORCAD Capture Lite
    * Building and analysing the circuit of a NPN transistor **inverter gate** in ORCAD Capture Lite
    * Building and analysing the circuit of a NPN **NAND gate** in ORCAD Capture Lite
    * Building and analysing the circuit of a **1:2 DMUX** in Vivado
    
4.  Basic prototyping of the different circuits on stripboard
    * Assembling switch (succesful)
    * Assembling test configuration for NAND gate (succesful)
    * Assembling reduced footprint configuration for NAND gate (succesful)
    * Assembling complete configuration of NAND gate with input and output 3mm LED indicators (failure due to imperfect contacts)
    * Rehash of reduced footprint configuration of NAND and Inverter gate (succesful)
    * Rehash of complete NAND gate configuration on a perf board (succesful)
    * Final perf board prototype of 1:2 DMUX 


### RTL Basics
[schematic of RTL gates side by side with symbol of gate and truth table][done in powerpoint]
[how RTL switches work][done in latex, schematic done in powerpoint]

### Final Circuits in PSpice
[circuit in PSpice vs circuit on perf board with overlay on both of them with voltages]

### Showcase of circuits 
[simple inverter education circuit with current shunts and values]
[NAND gate and 1:2 DMUX working as intended with truth table overlay]
