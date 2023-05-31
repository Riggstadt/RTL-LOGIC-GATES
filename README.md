# RTL-LOGIC-GATES
Resistor-Transistor Logic based Logic Gates

### Description
This repo covers some of the logic gates I designed and built out of discrete bipolar transistor

### Design constraints
The logic gate circuits must:
1.  Be powered by a 5V (±0.1V) supply voltage from a regular USB port
2.  Occupy a limited PCB footprint
3.  Insure a big enough current to drive at least one LED as a state indicator (H/L)

### Parts used overall
I've decided to use the 2N3904 transistor as its gain of roughly 150 at collector currents between 5 to 10 mA is very appropriate. The resistors used are all power rated for a maximum dissipation of 250mW, which is unlikely to be reached in these circuits. The circuits were assembled and build on strip-board (veroboard).

### The Inverter
#### Theoretical Aspects
The inverter is a simple circuit, only one transistor being needed for its construction.
How it works:
* If we provide a High signal at the base, the transistor will enter its saturation region and drop a small amount of voltage between collector and ground, thus ensuring that the output is a logical Low.
* If we instead provide a Low signal at the base, the transistor will enter its cutoff region and will no longer conduct electricity, thus ensuring the output voltage will be about 5V.
There are a few characteristics that are of great interest to us, such as VCE(sat) and current gain at saturation.

We will design a proof of concept circuit using the test values provided by the datasheet: VCE(sat,max) = 0.2V, Ib = 1mA, Ic = 10mA.


$$V_{CC} = R_{B}\cdot I_{B}+V_{BE(sat)}\Longrightarrow R_{B}=\frac{5-0.65}{0.001}=4.35K\Omega$$
$$V_{CC} = R_{C}\cdot I_{C}+V_{CE(sat)}\Longrightarrow \frac{5-0.2}{0.01}=480\Omega$$
Note that $V_{CE(sat)}$ is the worst case value, we can have even lower saturation voltages whilst under 10mA collector current.

![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/cc738bed-8c1f-4d4b-b39c-a31204025a64)







#### Practical circuit and measurements
The first iterations of the inverter circuits were more ad-hoc and clunky. The simplest way of checking the proper functioning of the circuit is connecting a LED in series with a current limiting resistor at the output of the gate. I targeted various nominal parameters for the leds I used. It turned out the LEDs, although all of the same colour, had significantly different forward voltages (10mA @ 1.81V or 20mA @ 2.01V). The availability of the parts also dictated the construction of the gates. Having used a significant number of my low value resistor in the prototype stage of this project and of other projects I was left with mainly 270ohm / 470ohm resistors.
After taking a quick glance at the simulations in falstad and LTspice and confirming the appropriate values I soldered the pieces on the strip-board.
The inverters work well enough that they can be integrated into multigate circuits, such as an SR latch.

| High at input  | . | Low at input | . |
| ------------- |---| ------------- |---|
| $V_{CE}\\;[V]$ |0.0389|$V_{CE}[V]$|3.714|
| $V_{BE}\\;[V]$ |0.823|$V_{BE}[V]$|0.045|
| $I_{C}\\;[A]$ |17.85e-3|$I_{C}[A]$|5e-3|
| $V_{out}\\;[V]$ |0.043|$V_{out}[V]$|3.7|
| $I_{D}\\;[A]$ |0|$I_{D}[A]$|5.015e-3|
| $I_{B}\\;[A]$ |15.78|$I_{B}[A]$|0|

### The OR Gate
I was trying to build an XOR gate but had a hard time finding appropriate schematics. I decided to experiment with this circuit from a hackaday post:
![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/c6c808a1-2631-44ab-bb30-d51598bb54e6)


No matter how hard I tried I couldn't convince the circuit to obey the truth table of the xor function, but discovered that with a few tweaks you could make an OR gate. The gates I built worked well enough and were integrated in bigger multigate circuits without significant losses or errors.

The main problem with my implementation, barring the obvious absence of a ground without connecting the state LED, is that the transistors don't really work as they're supposed to. $V_{E}$ will be slightly bigger than $V_{C}$ and the current will flow from the emitter to the collector. $V_{E} < V_{B}$ and $V_{C} < V_{B}$ so the transistor should be considered saturated. There shouldn't be any problems with this approach as all the possible voltages and currents are far too low to inflict any damage upon the transistors. One unexpected advantage of this "reverse" configuration is that $V_{CE(sat)}$ will be significantly smaller than its classical counterpart, from 0.2/0.3V to a 1/2mV or less
A falstad simulation of my OR gate implementation.
Do note that in the above presented simulation only one of the inputs is High, and as such only one transistor is in saturation. If both of the inputs are High, the circuit will act like a very low gain current amplifier, as the transistors would be in the Reverse Active Region.

![REVORGATE_page-0001](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/eb60184f-803d-45f3-958c-b32c2baaeb7e)


|A_ON,B_ON|T1|T2|A_ON,B_OFF|T1|T2|
|---|---|---|---|---|---|
| $V_{CE}\\;[V]$ |-0.869|-0.867|$V_{CE}\\;[V]$|-1.93|<0.001|
| $V_{BE}\\;[V]$ |-0.182|-0.182|$V_{BE}\\;[V]$|-1.93|0.748|
| $I_{B}\\;[A]$ |0.5e-3|0.5e-3|$I_{B}\\;[A]$|0|3.57e-3|
| $V_{out}\\;[V]$ |4.24|4.24|$V_{out}\\;[V]$|3.18|3.18|
| $I_{D}\\;[A]$ |6.4e-3|6.4e-3|$I_{D}\\;[A]$|3.57e-3|3.57e-3|

The alternative is to build a more classical OR logic gate. The gate is built out of two transistors connected in parallel with common collector and emitter currents. When one transistor is in cutoff, the other will conduct, insuring a voltage drop of about $V_{CC}-V_{BE}$ at the output of the gate.

![normalorgate_page-0001](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/95c2579a-0de8-415b-a0d2-004d624c2215)

The classical approach has several key advantages:
* The current doesn't change drastically when connecting both inputs to High 
* The gate has a ground connection without needing a state indicator's grounding
* The circuit works within the confines of the active operating region.

OR gate(L) and Inverter(R, base and collector resistors present on the other side of the perfoboard)

![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/5b58683a-2d8f-4dd5-b754-9d018e800d46)

### SR Latch 
Will add more details to this section, at the moment only a showcase of the circuit:
![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/eb3a23c2-464d-482d-90d0-805675fc6c4a)
![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/954cb97f-6d02-4f8f-a51e-282af0e29af5)
![image](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/ac137065-f500-44ae-ab52-38e582a4bfb5)




### Selected Sources/ Resources
* https://www.youtube.com/watch?v=i5K1sYbVUmo&ab_channel=electronzapdotcom
* https://hackaday.io/project/8449-hackaday-ttlers/log/150147-bipolar-xor-gate-with-only-2-transistors
* https://electronics.stackexchange.com/questions/29756/bjt-in-reverse-active-mode-of-operation
* https://www.falstad.com/circuit/
* https://learn.sparkfun.com/tutorials/transistors/operation-modes
