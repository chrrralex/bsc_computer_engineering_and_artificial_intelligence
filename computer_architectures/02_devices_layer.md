# 02.01. Devices Layer

### 02.01. Electrical Quantities

**Atom Model**: the atom is the basic particle of a chemical element and it's the fundamental building block of matter. An atom consists of a nucleus (where there is the 99.94% of the atom mass) of the two subparticles protons and neutrons, surrounded by an electromagnetically bound swarm of electrons (another type of subparticles). The electrons of an atom are attracted to the protons in an atomic nucleus by the electromagnetic force, meanwhile the protons and neutrons in the nucleus are attracted to each other by the nuclear force: both are very important for the atom stability (and, at the global level, for the matter stabiliy). An atom is composed by three main elements (in reality there are more elements and the atom's structure is very complex, but we will simplify everything):

- Protons: indicated with `p+` (or simply `p`), which have a negative charge.
- Neutrons: indicated with `n` (or simply `n`), which have a neutral charge.
- Electrons: indicated with `e-` (or simply `e`), which have a negative charge.

Different numbers of `p+` in the nucleus defines different chemical elements. Atoms with the same number of `p+`, but a different number of `n` are called isotopes of the same element. Atoms are extremely small, typically around 100 pm (picometers) across (1 pm = 10^(-12) m). Aroms are so small that accurately predicting their behavior using classical physics is not possible due to quantum effects.

The following figure shows the current models accepted for the atom:

<!-- to add -->
*In Figure: the accepted model of the atom*

The following is the Bhor's model (also known as Rutherford–Bohr model), not accepted in quantum physics, but considered generally a valid model when it comes to electric current and electricity:

<!-- to add -->
*In Figure: Rutherford–Bohr model, a simplified model*

Electrons are the main protagonists of the electric current: it's in fact defined as a flow of negative electric charges that flow from one area to another within a given material. In an atom, `p+` have a positive charge of `+1.602 * 10^(-19)`, meanwhile `e-` have a symmettric negative charge of `-1.602 * 10^(-19)`.

**Voltage**: is the difference in electric potential between two points in an electrical circuit that causes electric charge to flow. It represents the energy per unit charge available to move electrons through a conductor. The voltage `V` is the ratio between the work (or energy) `W` and the electric charge `Q`, also kown as electric quantity:

```
V = W / Q
1 V = 1 J / 1 C
```

where:

- `V` is expressed in Volt (`V`),
- `W` is expressed in Joule (`J`),
- `Q` is expressed in Coulombs (`C`).

**Current Quantity and Intensity**: intensity of the electric current is the rate at which electric charge flows through a conductor. Quantity of the electri current is the product between the intensity of the electric current and the time difference (normally one second, or 1 s). It measures how much charge passes through a point in a circuit per unit time. Electric quantity is described by the following formula:

```
Q = I x Δt
1 C = 1 A x 1 s
```

where:

- `Q` is expressed in Coulomb (`C`),
- `I` is expressed in Ampere (`A`),
- `t` is expressed in seconds (`s`).

You can calculate the electrical current intensity `I` in the following way:

```
I = Q / Δt
1 A = 1 C / 1 s
```

where all quantities are the same of the previous formula.

Electric current represents the movement of charge carriers, typically electrons (in conductors). Using the water analogy, the voltage `V` is the pressure and the intensity of the electrical current `I` is the flow rate of water.

**Energy**: is the capacity to perform work, or produce change in a physical system. In electrical systems, energy represents the ability to move electric charges through a circuit. Energy is measured in Joule (`J`) and is the product between the work (measured in Netwon, `N`) and distance (measured in meters, `m`):

```
E = L x d
1 J = 1 N x 1 m
```

Electrical energy can be calculated as:

```
E = V x I x Δt
1 J = 1 V x 1 A x 1 s
```

**Power**: is the rate at which energy is transferred or converted per unit time. It measures how fast work is done or how quickly energy is used. The power is the result of the following formula:

```
P = E / Δt
1 W = 1 J / 1 s 
```

where:

- `P` is expressed in Watts (`W`),
- `t` is expressed in seconds (`s`).

**Resistance**: is the property of a material or component that opposes the flow of electric current in a circuit. It determines how much a conductor resists the movement of electric charges. From the physical point of view, the resistance `R` of a material depends on the material type, it's spatial extensions (length for conductors), cross-sectional area and temperature. The resistance `R` of a material is given by:

```
R = ρ * (L / A)
```

where:

- `ρ` is called resistivity and it's material-specific (for example, silver generally has a very very low resistivity, while glass has a very high resistivity);
- `L` is the length of the material, or conductor;
- `A` is the area of the material, or conductor.

The following figure shows the listed parameters:

<!-- to add -->
*In Figure: the various parameters used to calculate the resistivity of a material*

**Conductance**: is the measure of how easily electric current flows through a material, or component. It is the reciprocal (inverse) of electrical resistance. Given a resistance `R` of a specific material, you can calculate the conductance in this way:

```
G = 1 / R
1 S = 1 / 1 Ω
```

or, equivalently:

```
G = R^(-1)
1 S = 1 Ω^(-1)
```

In practice, conductance is the inverse of resistance: while the latter measures how much a material tends to oppose the flow of electric charges, the former measures how much the material itself favors it. Conductance is measured in Siemens (`S`) and it's indicated with the letter `G`.

### 02.02. Circuit Basics

**Insulators, Conductors and Semiconductors**: to implement different types of conductors, there are different types of materials:

- Conductors: material that have a high conductance. Conductors are materials with very low resistivity and they favor the flow of electric curent.
- Insulators: material that have a high resistance. Insulators are materials that prevent the flow of electric current, characterized by high resistivity and a large band gap.
- Semiconductors: material that have a medium conductance (or medium resistivity). Semiconductors are materials with electrical conductivity between conductors and insulators, commonly used in electronic components like diodes and transistors. Semiconductors are the base of the digital circuits.

**Circuit, Node, Branch and Mash**: an electrical circuit is a set of components of various nature (electrical, mechanical, electromechanical) appropriately placed in order to react adequately to the flow of electric current.

A node is a point in an electrical circuit where two or more circuit elements are connected together; all points belonging to the same node share the same electrical potential (voltage). There are three types of nodes: a simple node is an interconnection of two elements, an essential node is an interconnection of three (or more) elements and a reference node (also called ground, or GND) is a node with a voltage equal to `0 V`.

A branch is a portion of an electrical circuit that contains a single circuit element (such as a resistor, capacitor, source, or inductor) connected between two nodes. For example, a resistor called `R1` connected to another resistor called `R2` defines a branch between two components. A branch connects only and only two nodes.

A mesh is a closed loop in an electrical circuit that doesn't contain any other loops inside it. It is the smallest possible closed path in a planar circuit. Meshes are used to analyze the circuit, or to isolate a specific closed path of the circuit (a subcircuit).

The following figure shows an example of circuit. In the figure arw shows nodes, branches and mashes.

<!-- to add -->
*In Figure: example of circuit where branches, nodes and mashes are shown*

**Ideal and Real Voltage Source**: the "pressure" of the flow of the electric current is given by the voltage source. An ideal voltage source is a source that provides a constant voltage independent of the current drawn from it and it has the following characteristics:

- The voltage is always constant under any load.
- Internal resistance of the source is `0 Ω`.
- Can supply any amount of current.
- Does not exist in practice: the ideal voltage source is a theoretical model only.

A real voltage source provides a voltage that changes slightly with load current due to its internal resistance. A real voltage source has the following characteristics:

- Voltage decreases when load current increases.
- Internal resistance isn't `0 Ω`.
- Limited current capability.
- Exists in practical systems (batteries and power supplies).

The following figure shows the relationships between the voltage provided by an ideal and a real voltage source and the time:

<!-- to add -->
*In Figure: relationship between voltage and time of an ideal and real voltage source*

**Ideal and Real Current Source**: the "intensity" of the flow of the electric current is given by the current source. An ideal current source is a source that provides a constant intensity of electrical current independent of the current drawn from it and it has the following characteristics:

- The current is always constant under any load.
- Internal resistance of the source is infinite.
- Can maintain constant current regardless of terminal voltage.
- Does not exist in practice: the ideal current source is a theoretical model only.

A real current source provides an approximately constant current but is affected by its internal resistance. A real current source has the following characteristics:

- Output current varies slightly with load voltage.
- Internal resistance is large but finite.
- Limited voltage compliance range.
- Exists in practical electronic circuits.

The following figure shows the relationships between the intensity of the electrical current provided by an ideal and a real current source and the time:

<!-- to add -->
*In Figure: relationship between current and time of an ideal and real current source*

**Kirchhoff’s laws: KCL and KVL**: the Kirchoff's laws are very useful to analyze what happen in a specific region, or node of a circuit. Kirchhoff's laws are based on the conservation principles. There are two Kirchhoff’s laws: KCL and KVL. Here's a simple explanation of each:

KCL (Kirchhoff’s Current Law) states that the algebric sum of currents at a node is zero. If we indicate the currents with `Ii`, where `i` is an index varting from `1` to `n` (`n` are the number of the currents), we can express the KCL law in this way:

```
∑ Ii = 0, i = 1, 2, ..., n
```

All currents entering the node are positive and all currents leaving the node are negative.

The following figure shows the application of the KCL principle:

<!-- to add -->
*In Figure: the application of the KCL principle in an example of a circuit*

KVL (Kirchoff's Voltage Laws) states that the algebric sum of voltages around any closed loop is zero. If we indicate the voltages with `Vi`, where `i` is an index varting from `1` to `n` (`n` are the number of the voltages), we can express the KVL law in this way:

```
∑ Vi = 0, i = 1, 2, ..., n
```

The sign of each voltage depends on the chosen loop direction and polarity convention. The voltage source is tipically positive and each other components of the circuit that consumes a parte of the voltage has a negative voltage.

The following figure shows the application of the KVL principle:

<!-- to add -->
*In Figure: the application of the KVL principle in an example of a cuircit*

**In series and in parallel components**: components are in series when they are connected end-to-end along a single path (or branch), so the same current flows through all of them. An `n` components in series have the following characteristics:

- They've the same current: `I1 = I2 = I3 = ... = In`; therefore all components receive the same current intensity `I`.
- Total voltage equals the sum of voltage drops (each component represent a voltage drop): `Vtot = V1 + V2 + V3 + ... Vn`; 
each component consumes a certain amount of voltage, directly proportional to its characteristics (such as internal resistance). For the component `i`, the voltage is given by the following formula: `Vi = Ri * I`.

The following figure shows an example of components in series (resistors):

<!-- to add -->
*In Figure: an example of a circut to calculate resistors in series*

Components are in parallel when they are connected across the same two nodes, so the same voltage appears across each component. An `n` components in parallels have the following characteristics:

- They've the same voltage: `V1 = V2 = V3 = ... = Vn`; therefore all components receive the same voltage `V`.
each component consumes a certain amount of voltage, directly proportional to its characteristics (such as internal resistance).
- Total current equals the sum of each branch current: `Itot = I1 + I2 + I3 + ... In`; each component consumes a certain amount of current, directly proportional to its characteristics (such as internal resistance). For the component `i`, the voltage is given by the following formula: `Ii = V / Ri`.

The following figure shows an example of components in parallels (resistors):

<!-- to add -->
*In Figure: an example of a circut to calculate resistors in parallels*

**Thevenin Transformation**: the Thevenin transformation replaces any linear two-terminal circuit with an equivalent circuit consisting of a single voltage source `Vth` in series with a single resistance `Rth`. This equivalent circuit produces the same terminal behavior (same voltage and current) as the original circuit when connected to any load. The Thevenin voltage is the open-circuit voltage at the terminals, and the Thevenin resistance is the equivalent resistance seen from the terminals with independent sources turned off. This is a very useful application in the circuit analysis to simplify it. Here's an example of the Thevenin transofrmation:

<!-- to add -->
*In Figure: an example of the Thevenin transformation*

**Norton Transformation**: the Norton transformation replaces any linear two-terminal circuit with an equivalent circuit consisting of a single current source `In` in parallel with a single resistance `Rn`. The Norton current is the short-circuit current between the terminals, and the Norton resistance equals the equivalent resistance seen from the terminals with independent sources turned off. The Norton equivalent circuit behaves identically to the original circuit at its terminals for any connected load. Here's an example of the Norton transofrmation:

<!-- to add -->
*In Figure: an example of the Norton transformation*

### 02.03. Resistance and Resistors

**Ideal Resistor**: an ideal resistor is the ideal working model of the resistor component. A resistor is an electronic component with tha main pruprose of opposing the flow of charges. In practice, the resistor is the real component of the resistance in a circuit model. An ideal resistance is a theoretical component that opposes the flow of electric current with a constant resistance value independent of temperature, voltage, frequency, or physical conditions. It doesn't store energy and has no parasitic effects such as inductance, or capacitance.

**Real Resistor**: a real resistance is a physical component whose resistance value can change with temperature, frequency, and operating conditions. It also includes small parasitic inductance and capacitance and dissipates energy as heat, so its behavior slightly deviates from the ideal model in practical circuits. There are different types of resistors:

- Carbon composition resistors: are made from a mixture of carbon powder and insulating material molded into a cylindrical shape. They are inexpensive and can withstand high energy pulses, but they have lower accuracy and higher noise compared to modern resistors.
- Carbon film resistors: are made by depositing a thin layer of carbon on a ceramic rod and cutting a spiral groove to adjust resistance. They provide better stability and accuracy than carbon composition resistors and are widely used in general electronic circuits.
- Metal film resistors: they use a thin metal layer deposited on a ceramic base, offering high precision, low noise, and good temperature stability. They are commonly used in precision electronic applications.
- Wire-wound resistors: are made by winding a metal wire around a ceramic core and are capable of handling high power and high current. They are typically used in power supplies, industrial equipment, and high-current applications.
- Variable resistors: they allow adjustment of resistance manually using a rotating or sliding control. They are commonly used for volume control, tuning circuits, and calibration in electronic devices.
- Thick and thin film resistors: are made by printing a resistive paste onto a substrate, while thin film resistors are produced by depositing a very thin resistive layer onto a surface. Thin film resistors provide higher precision, while thick film resistors are cheaper and widely used in surface-mount electronics.

The following figure shows the different types of resistors:

<!-- to add -->
*In Figure: different types of resistors*

**Resistors in series**: a group of resistors in series form a single resistor whose resistance value is the sum of all resistors in series. For example, we consider the following circuit with `R1`, `R2` and `R3` resistors in series:

<!-- to add -->
*In Figure: a circuit with three resistors in series*

The three resistors shown in figure can be replaced by a single resistor, for example called `Rtot`, with the following value:

```
Rtot = R1 + R2 + R3
```

The new circuit is:

<!-- to add -->
*In Figure: the same previous circuit with the equivalent resistance*

`Rtot` is also called equivalent resistance.

**Resistors in parallel**: a group of resistors in parallel form a single resistor whose resistance value is the inverse of the sum of all inverse resistance of each resistors in parallel. For example, we consider the following circuit with `R1`, `R2` and `R3` resistors in parallel:

<!-- to add -->
*In Figure: a circuit with three resistors in parallel*

The three resistors shown in figure can be replaced by a single resistor, for example called `Rtot`, with the following value:

```
Rtot = 1 / (R1^(-1) + R2^(-1) + R3^(-1))
```

Alternatively, you can use the following formula:

```
1 / Rtot = R1^(-1) + R2^(-1) + R3^(-1)
```

If you have only two resistances in parallel, you can use the following formula:

```
Rtot = (R1 * R2) / (R1 + R2)
```

The new circuit is:

<!-- to add -->
*In Figure: the same previous circuit with the equivalent resistance*

`Rtot` is also called equivalent resistance.

**Equivalent Resistance**: the equivalent resistance of a circuit is a single resistance obtained by calculating the total resistance of a circuit. A circuit can have both resistances in series and resistances in parallel. The following circuit has both resistances in series and resistances in parallel:

<!-- to add -->
*In Figure: a circuit with two resistors in parallel and three resistors in series*

First, we can calculate the equivalent resistance of the resistors `R2` and `R3`, that are in parallel, by obtaining the `Rp` resistor. Next, we can see `R1`, `Rp` and `R4` like three resistances in series, so we can calculate the `Rtot`, or `Req`.

So, we can operate in two steps:

```
Step 1: calculate the Rp equivalent resistance
Rp = (R2 * R3) / (R2 + R3)

Step 2: calculate the Rtot equivalent resistance
Rtot = R1 + Rp + R4
```

**Ohm's Law**: the Ohm's law is one of the most important law in electronic circuits. It describes the relationships between the voltage `V`, the resistance `R` and intensity of the current `I` in an electric circuit. The original form of the Ohm's law states that the intensity of the electric current `I` flowing through a conductor is directly proportional to the voltage `V` across it and inversely proportional to its resistance `R`, provided temperature and physical conditions remain constant.

```
V = R x I
```

From the previous formula, we can discover `R` if `V` and `I` are known:

```
I = V / R
```

or, if you know both `V` and `I`:

```
R = V / I
```

### 02.03. Capacitor and Capacitance

**Ideal Capacitor**: an ideal capacitor is the ideal working model of the capacitor component. A capacitor is an electronic component with tha main pruprose of collecting charges. In practice, the capacitor is the real component of the capacitance in a circuit model. An ideal capacitor is a theoretical component that stores electrical energy only in the form of an electric field between its plates and has a constant capacitance value independent of frequency, temperature, or voltage. It has no energy loss, no internal resistance, and no parasitic inductance, so it behaves perfectly according to capacitor equations.

**Real Capacitor**: a real capacitor is a practical component whose behavior deviates from the ideal model because it includes internal resistance, leakage current, and small parasitic inductance. Its capacitance may vary with temperature, frequency, and voltage, and some stored energy is lost as heat during operation. There are different types of capacitor:

- Ceramic capacitors: are made using ceramic material as the dielectric between two conductive plates. They are small, inexpensive, and widely used in high-frequency applications such as filtering, bypassing, and decoupling in electronic circuits.
- Electrolytic capacitors: use an electrolyte as one of the conductive plates and provide very high capacitance values in a compact size. They are polarized components commonly used in power supplies for filtering and energy storage.
Tantalum capacitors: are a type of electrolytic capacitor that uses tantalum metal as the electrode, offering high capacitance stability and reliability in a small size. They are commonly used in portable electronic devices and precision circuits.
- Film capacitors: use thin plastic films such as polyester or polypropylene as the dielectric material. They provide good stability, low losses, and are widely used in timing circuits, signal processing, and audio applications.
- Mica capacitors: are made using mica as the dielectric material and provide very high accuracy and stability with low losses. They are typically used in high-frequency and radio-frequency circuits.
- Variable capacitors: allow adjustment of capacitance by changing the distance or overlap between plates. They are commonly used in tuning circuits such as radio receivers and oscillators.

The following figure shows the different types of capacitors:

<!-- to add -->
*In Figure: different types of capacitors*

**Capacitors in series**: a group of capacitors in series form a single capacitor whose resistance value is the reverse of the sum of all the reverse of the capacitance of each capacitor in series. For example, we consider the following circuit with `C1`, `C2` and `C3` capacitors in series:

<!-- to add -->
*In Figure: a circuit with three capacitors in series*

The three capacitors shown in figure can be replaced by a single capacitor, for example called `Ctot`, with the following value:

```
Ctot = 1 / (C1^(-1) + C2^(-1) + C3^(-1))
```

Alternatively, you can use the following formula:

```
1 / Ctot = C1^(-1) + C2^(-1) + C3^(-1)
```

If you have two capacitors in series only, you can use the following formula:

```
Ctot = (C1 * C2) / (C1 + C2)
```

The new circuit is:

<!-- to add -->
*In Figure: the same previous circuit with the equivalent capacitance*

`Ctot` is also called equivalent capacitance.

**Capacitors in parallel**: a group of capacitors in parallel form a single capacitor whose capacitance value is the sum of the capacitance of each capacitors in parallel. For example, we consider the following circuit with `C1`, `C2` and `C3` capacitors in parallel:

<!-- to add -->
*In Figure: a circuit with three capacitors in parallel*

The three capacitors shown in figure can be replaced by a single capacitor, for example called `Ctot`, with the following value:

```
Ctot = C1 + C2 + C3
```

The new circuit is:

<!-- to add -->
*In Figure: the same previous circuit with the equivalent capacitance*

`Ctot` is also called equivalent capacitance.

**Equivalent Capacitance**: the equivalent capacitance of a circuit is a single capacitor obtained by calculating the total capacitance of a circuit. A circuit can have both capacitors in series and capacitors in parallel. The following circuit has both capacitors in series and capacitors in parallel:

<!-- to add -->
*In Figure: a circuit with two capacitors in parallel and three capacitors in series*

First, we can calculate the equivalent capacitance of the capacitors `C2` and `C3`, that are in parallel, by obtaining the `Cp` capacitor. Next, we can see `C1`, `Cp` and `C4` like three capacitors in series, so we can calculate the `Ctot`, or `Ceq`.

So, we can operate in two steps:

```
Step 1: calculate the Cp equivalent capacitance
Cp = (C2 * C3) / (C2 + C3)

Step 2: calculate the Ctot equivalent capacitance
Ctot = C1 + Cp + C4
```

<!-- to do - RC circuits -->

### 02.04. Inductor and Inductance
<!-- to do - ideal inductor -->
<!-- to do - real inductor -->
<!-- to do - types of inductor -->
<!-- to do - inductors in series -->
<!-- to do - inductors in parallel -->
<!-- to do - equivalent inductance in a circuit -->
<!-- to do - RLC circuits -->

### 02.05. Semiconductors Basics
<!-- to do - crystalline structure of silicon -->
<!-- to do - energetic bands: valenca band and conduction band -->
<!-- to do - intrinsic semiconductors -->
<!-- to do - charge carriers: p-type and n-type dopants -->
<!-- to do - electrons and holes -->
<!-- to do - drift and diffusion current -->

### 02.06. Diode
<!-- to do - PN junction -->
<!-- to do - depletion region -->
<!-- to do - barrier potential -->
<!-- to do - forward and reverse polarization -->
<!-- to do - reverse-bias polarization -->
<!-- to do - diode I-V characteristic -->
<!-- to do - diode as a switch -->
<!-- to do - basic diode logic -->

### 02.07. BJT (Bipolar Junction Transistor)
<!-- to do - BJT introduction: advantages and problems -->
<!-- to do - structure: NPM and PNP -->
<!-- to do - operating regions: cutoff, active, saturation -->
<!-- to do - BJT as a switch -->
<!-- to do - basic BJT logic -->

### 02.08. MOS (Metal-Oxide Semiconductor)
<!-- to do - MOS and MOSFET introduction: advantages and problems -->
<!-- to do - MOS capacitor -->
<!-- to do - MOSFET structure: NMOS and PMOS -->
<!-- to do - operating regions: cutoff, triode, saturation -->
<!-- to do - threshold voltage -->
<!-- to do - MOSFET I-V characteristic -->
<!-- to do - body effect -->
<!-- to do - MOS as a switch -->
<!-- to do - basic MOS logic: NMOS inverter, PMOS inverter, ratioed logic -->

### 02.09. CMOS (Complementary Metal-Oxide Semiconductor)
<!-- to do - CMOS introduction: advantages and problems -->
<!-- to do - CPUN (Complementary pull-Up Network) -->
<!-- to do - CPDN (Complementary pull-Down Network) -->
<!-- to do - structure -->
<!-- to do - CMOS as a switch -->
<!-- to do - basic CMOS logic: realization of NOT, NAND, NOR, AND, OR, XOR and XNOR gates with CMOS -->
<!-- to do - VTC (Voltage Transfer Characteristic) -->
<!-- to do - noise margins: NMH and NML -->
<!-- to do - fan-in and fan-out -->
<!-- to do - propagation delay: raise time and fall time -->
<!-- to do - static and dynamic power dissipation -->
<!-- to do - short-circuit power -->
<!-- to do - switching activity -->
<!-- to do - power-velocity tradeoff -->

### 02.10. ICs (Integrated Circuits) Basics
<!-- to do - definition of integrated circuits (ICs) -->
<!-- to do - advantages of integrated circuits vs discrete components -->
<!-- to do - levels of integration: - SSI (Small-Scale Integration), MSI (Medium-Scale Integration), LSI (Large-Scale Integration), VLSI (Very Large-Scale Integration) and ULSI (Ultra-Large-Scale Integration) -->
<!-- to do - digital vs analog integrated circuits -->
<!-- to do - mixed-signal integrated circuits --> 
<!-- to do - semiconductor technologies overview: BJT technology, MOS technology and CMOS technology -->
<!-- to do - basic IC structure: substrate, diffusion regions, polysilicon, metal interconnect layers -->
<!-- to do - logic families overview: TTL, NMOS logic, PMOS logic, CMOS logic -->
<!-- to do - CMOS as dominant digital IC technology -->
<!-- to do - IC packaging concepts: DIP, QFP, BGA -->
<!-- to do - pin configuration and pinout diagrams -->
<!-- to do - power supply pins: VDD, VSS, GND -->
<!-- to do - propagation delay in ICs -->
<!-- to do - power dissipation in ICs: static power, dynamic power -->
<!-- to do - fan-in and fan-out concepts -->
<!-- to do - noise margins in digital ICs -->
<!-- to do - scaling trends in integrated circuits (Moore’s Law overview) -->
<!-- to do - reliability considerations in ICs: heat dissipation, signal integrity and process variations -->