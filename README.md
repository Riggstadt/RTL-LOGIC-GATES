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
[schema cu circuitul si valorile simulate pentru diversi parametri]
[emulare irl cu 4.35 = 2k + 2k + 330 si 480 = 470]




#### Practical circuit and measurements
The first iterations of the inverter circuits I built were more ad-hoc and clunky. The simplest way of checking the proper functioning of the circuit is connecting a LED in series with a current limiting resistor at the output of the gate. I targeted various nominal parameters for the leds I used. It turned out the LEDs, although all of the same colour, had significantly different forward voltages (10mA @ 1.81V or 20mA @ 2.01V). The availability of the parts also dictated the construction of the gates. Having used a significant number of my low value resistor in the prototype stage of this project and of other projects I was left with mainly 270ohm / 470ohm resistors.
After taking a quick glance at the simulations in falstad and LTspice and confirming the appropriate values I soldered the pieces on the strip-board.
The inverters work well enough that they can be integrated into multigate circuits, such as an SR latch.

[Schema cu valori a inversorului si simulare]
[masuratori pe circuit]

### The OR Gate
[Versiunea mea (cu poveste)  vs versiunea mainstream]
https://www.youtube.com/watch?v=i5K1sYbVUmo&ab_channel=electronzapdotcom
Note: la versiunea mea tranzistorii sunt in regim inverse activ si curentul curge de la emitor la colector not best desig
### The NAND Gate
[adaug momentan doar imagini stil galerie cu disclaimer de completare]

### SR Latch 
[adaug momentan doar imagini stil galerie cu disclaimer de completare]

###Pe viitor (Poarta XOR)
http://sullystationtechnologies.com/npnxorgate.html
https://electronics-fun.com/logic-gates/#XOR_gate
https://math.stackexchange.com/questions/1523748/simplifying-boolean-algebra-expression-that-contains-xor
