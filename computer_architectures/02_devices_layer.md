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
<!-- to do - insulators, conductors and semiconductors -->
<!-- to do - circuit, nodes, branches and meshes -->
<!-- to do - ideal and real voltage source component -->
<!-- to do - ideal and real current source component -->
<!-- to do - Kirchhoff’s laws: KCL and KVL -->
<!-- to do - components in series and in parallel -->
<!-- to do - measure the current with an ammeter and the sunt resistance -->
<!-- to do - measure the voltage with a voltmeter -->
<!-- to do - Thevenin transformation -->
<!-- to do - Norton transformation -->

### 02.03. Resistance and Resistors
<!-- to do - ideal resistor -->
<!-- to do - real resistor -->
<!-- to do - types of resistor -->
<!-- to do - resistors in series -->
<!-- to do - resistors in parallel -->
<!-- to do - equivalent resistance in a circuit -->
<!-- to do - Ohm's law -->
<!-- to do - R circuits -->

### 02.03. Capacitor and Capacitance
<!-- to do - ideal capacitor -->
<!-- to do - real capacitor -->
<!-- to do - types of capacitor -->
<!-- to do - capacitors in series -->
<!-- to do - capacitors in parallel -->
<!-- to do - equivalent capacitance in a circuit -->
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