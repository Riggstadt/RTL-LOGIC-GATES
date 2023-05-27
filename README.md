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


[Cum scot valorile rezistentelor]
$$V_{CC} = R_{B}\cdot I_{B}+V_{BE(sat)}\Longrightarrow R_{B}=\frac{5-0.65}{0.001}=4.35K\Omega$$
$$V_{CC} = R_{C}\cdot I_{C}+V_{CE(sat)}\Longrightarrow \frac{5-0.2}{0.01}=480\Omega$$
Note that $V_{CE(sat)}$ is the worst case value, we can have even lower saturation voltages whilst under 10mA collector current.

![TESTCASE_INV_page-0001](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/03417f3d-e9bc-4cb9-a8d5-545ea77a8cde)
![TESTCASE_INV_page-0001](https://github.com/Riggstadt/RTL-LOGIC-GATES/assets/127757267/0badeb5a-ee04-46f4-9467-623e68e4ad8c)






#### Practical circuit and measurements
The first iterations of the inverter circuits I built were more ad-hoc and clunky. The simplest way of checking the proper functioning of the circuit is connecting a LED in series with a current limiting resistor at the output of the gate. I targeted various nominal parameters for the leds I used. It turned out the LEDs, although all of the same colour, had significantly different forward voltages (10mA @ 1.81V or 20mA @ 2.01V). The availability of the parts also dictated the construction of the gates. Having used a significant number of my low value resistor in the prototype stage of this project and of other projects I was left with mainly 270ohm / 470ohm resistors.
After taking a quick glance at the simulations in falstad and LTspice and confirming the appropriate values I soldered the pieces on the strip-board.
The inverters work well enough that they can be integrated into multigate circuits, such as an SR latch.

| High at input  | . | Low at input | . |
| ------------- |---| ------------- |---|
| $V_{CE}\\;[V]$ |0.0389|$V_{CE}[V]$|3.714|
| $V_{BE}\\;[V]$ |0.823|$V_{BE}[V]$|0.045|
| $I_{C}\\;[A]$ |4.82|$I_{C}[A]$|1.36|
| $V_{out}\\;[V]$ |0.043|$V_{out}[V]$|3.7|
| $I_{D}\\;[A]$ |0|$I_{D}[A]$|1.655|
| $I_{B}\\;[A]$ |4.26|$I_{B}[A]$|0|

### The OR Gate
[Versiunea mea (cu poveste)  vs versiunea mainstream]
https://www.youtube.com/watch?v=i5K1sYbVUmo&ab_channel=electronzapdotcom
I was trying to build a XOR gate but couldn't find many proper schematics and explanations. I chose to use the circuit presented in this hackaday post: https://cdn.hackaday.io/images/original/532881532876841662.gif. No matter how hard I tried I couldn't convince the circuit to obbey the truth table of the xor functin, but discovered that with a few tweaks here and there you could make an OR gate. The gates I built worked well enough and were integrated in bigger multigate cirucit without significant losses or errors.
[imagine cu schema si cand functioneaza care cum].
The main problem with my implementation, barring the obvious absence of a ground without connecting the state LED, is that the transistors don't really work as they're supposed to. $V_{E}$ will be slightly bigger than $V_{C}$ and the current will flow from the emitter to the collector. V_{E} < V_{B} and V_{C} < V_{B} so the transistor should be considered saturated. There shouldn't be any problems with this approach as all the possible voltages and currents are far too low to inflict any damage upon the transistors. One unexpected advantage of this "reverse" configuration is that $V_{CE(sat)}$ will be significantly smaller than its classical counterpart, from 0.2/0.3V to a 1/2mV or less
https://electronics.stackexchange.com/questions/29756/bjt-in-reverse-active-mode-of-operation
### The NAND Gate
[adaug momentan doar imagini stil galerie cu disclaimer de completare]

### SR Latch 
[adaug momentan doar imagini stil galerie cu disclaimer de completare]

###Pe viitor (Poarta XOR)
http://sullystationtechnologies.com/npnxorgate.html
https://electronics-fun.com/logic-gates/#XOR_gate
https://math.stackexchange.com/questions/1523748/simplifying-boolean-algebra-expression-that-contains-xor
