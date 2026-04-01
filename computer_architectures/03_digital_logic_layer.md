# 03. Digital Logic Layer

### 03.01. Boolean Algebra

**Boolean Algebra**: boolean algebra is a branch of mathematics used to represent and manipulate logical variables and logical operations, where variables can take only two values. These values are called boolean literal and it can be assigned to the boolean variables.

**Boolean Variable**: a variable that can take only two possible values: 0, or 1. Boolean variables are the fundamental elements of the boolean algebra and the digital logic circuits. Normally, a boolean variable is indicated by an uppercase letter, like `A`, or `B`.

**Boolean Literal**: a fixed logical value that can be `0`, or `1` only. In boolean algebra only two values are usable: `0` (also called `false`, or `low`) and `1` (also called `true`, or `high`). Note that there are only two valid boolean literals in the boolean algebra: `0` and `1`.

**Voltage and Boolean Algebra Relationship**: positive logic means and high value of tension (normally Vcc, or Vdd) is considered the `1` logical value, meanwhile a low value of tension (normally GND) is considered the `0` logical value. Digital circuits have the own specifications about the voltage levels: for example, an integrated circuit could consider as `1` logical value a voltage between 2.5 V and 5 V and as `0` logical value a voltage between 0 V and 1.5 V. It depends on the construction techniques.

**Positive and Negative Logic**: a positive logic associates the `1` logical value to an high voltage and the `0` logical value to a low voltage. Differently, the negative logic associates the `1` logical value to a low voltage and the `0` logical value to an high voltage.

**Functionally Complete Set**: as any other branch of the mathemtatics, in boolean algebra is considered a functionally complete set a set of boolean operators that can be used to express any boolean expression. A set of logic operations is functionally complete if every Boolean expression can be built using only those operations. Often, in boolean algebra the most common functionally complete set is: `AND`, `OR`, `NOT`. Another functionally complete set is the `NAND` gate alone and another also is the `NOR` alone: both the two previous sets are commonly used for the VLSI (Very Large Scale Integration) digital circuits implementation.

<!-- to do - truth tables -->
<!-- to do - main logical operations: NOT, AND, OR -->
<!-- to do - derived logical operations: NAND, NOR, XOR, XNOR -->
<!-- to do - one-variable principles -->
<!-- to do - two-variables principles -->
<!-- to do - de morgan laws -->
<!-- to do - minterms and maxterms -->
<!-- to do - fist canonic form and SOP (Sum Of Products) -->
<!-- to do - second canonic form and POS (Product Of Sums) -->
<!-- to do - two-variable k-maps -->
<!-- to do - three-variable k-maps -->
<!-- to do - four-variable k-maps -->
<!-- to do - the X value -->
<!-- to do - the Z value -->

### 03.02. Logic Gates and Truth Tables

**NOT gate**: the NOT gate is a basic logic gate that produces the inverse (complement) of its input. It accepts an input and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = !A`. The NOT logical gate has the following turth table:

| A | Y |
|---|---|
| 0 | 1 |
| 1 | 0 |

The NOT gate is represented in the following figure:

<!-- to do -->
*In Figure - The NOT logical gate with A input and Y output*


**BUF gate**: the BUF gate, contraction of BUFfer, is a basic logic gate that produces the same logical value of its input. It accepts an input and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = A`. This gate serves no logically useful function from a logical point of view. The BUF logical gate has the following turth table:

| A | Y |
|---|---|
| 0 | 0 |
| 1 | 1 |

The BUF gate is represented in the following figure:

<!-- to do -->
*In Figure - The BUF logical gate with A input and Y output*

But for which reason a BUF logical gate should be used? Normally, in the digital logical circuits, the length of a cable and the noise affects the digital signal and slowly degenreate it. The BUF logical gate is very useful to regenerate the signal (in terms of voltage and current). This is a common application when a digital signal must be delivered to one, or more devices, or circuits.

**AND gate**: the AND gate is a basic logic gate that produces the AND logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = A x B`, often abbreviated in `Y = AB`, like in the classic algebra. The AND logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

The AND gate is represented in the following figure:

<!-- to do -->
*In Figure - The AND logical gate with A and B inputs and Y output*

An AND gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, an AND3 gate (AND gate with 3 inputs) has a lower delay than an AND8 (AND gate with 8 inputs). Here's an example of an AND4 gate:

<!-- to do -->
*In Figure - The AND4 logical gate with four inputs and Y output*

**OR gate**: the OR gate is a basic logic gate that produces the OR logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = A + B`, where the OR function is representend by the sum operator (`+`), like in the classic algebra. The OR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

The OR gate is represented in the following figure:

<!-- to do -->
*In Figure - The OR logical gate with A and B inputs and Y output*

An OR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, an OR3 gate (OR gate with 3 inputs) has a lower delay than an OR8 (OR gate with 8 inputs). Here's an example of an OR4 gate:

<!-- to do -->
*In Figure - The OR4 logical gate with four inputs and Y output*

**NAND gate**: the NAND gate is a basic logic gate that produces the complement of the AND logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = !(A x B)`, often abbreviated in `Y = !(AB)`, like in the classic algebra. The NAND logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

The NAND gate is represented in the following figure:

<!-- to do -->
*In Figure - The NAND logical gate with A and B inputs and Y output*

An NAND gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a NAND3 gate (NAND gate with 3 inputs) has a lower delay than a NAND8 (NAND gate with 8 inputs). Here's an example of a NAND4 gate:

<!-- to do -->
*In Figure - The NAND4 logical gate with four inputs and Y output*

**NOR gate**: the NOR gate is a basic logic gate that produces the complement of the OR logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = !(A + B)`, where the sum operator (`+`) represents the OR function in the boolean algebra, like in the classic algebra. The NOR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

The NOR gate is represented in the following figure:

<!-- to do -->
*In Figure - The NOR logical gate with A and B inputs and Y output*

An NOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a NOR3 gate (NOR gate with 3 inputs) has a lower delay than a NOR8 (NOR gate with 8 inputs). Here's an example of a NOR4 gate:

<!-- to do -->
*In Figure - The NOR4 logical gate with four inputs and Y output*

**XOR gate**: the XOR gate (eXclusive OR) is a basic logic gate that produces the `1` logical output only if the number of inputs set to `1` is odd. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = A ⊕ B`, where the circled sum operator (`⊕`) represents the XOR function in the boolean algebra. The XOR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

The XOR gate is represented in the following figure:

<!-- to do -->
*In Figure - The XOR logical gate with A and B inputs and Y output*

An XOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a XOR3 gate (XOR gate with 3 inputs) has a lower delay than a XOR8 (XOR gate with 8 inputs). Here's an example of a XOR4 gate:

<!-- to do -->
*In Figure - The XOR4 logical gate with four inputs and Y output*

The XOR gate is also called "diversity gate", cause a XOR with two inputs returns an output euqal to the `1` logical value only if the two inputs are different (`A = 0` and `B = 1`, or viceversa).

**XNOR gate**: the XNOR gate (eXclusive NOT OR) is a basic logic gate that produces the `1` logical output only if the number of inputs set to `1` is even. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = !(A ⊕ B)`, where the circled sum operator (`⊕`) represents the XOR function in the boolean algebra. The XNOR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

The XNOR gate is represented in the following figure:

<!-- to do -->
*In Figure - The XNOR logical gate with A and B inputs and Y output*

An XNOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a XNOR3 gate (XNOR gate with 3 inputs) has a lower delay than a XNOR8 (XNOR gate with 8 inputs). Here's an example of a XNOR4 gate:

<!-- to do -->
*In Figure - The XNOR4 logical gate with four inputs and Y output*

The XNOR gate is also called "equality gate", cause a XNOR with two inputs returns an output euqal to the `1` logical value only if the two inputs are equal (`A = 0` and `B = 0`, or `A = 1` and `B = 1`).

**TRI gate**: the TRI gate (TRIstate) is a specific gate that has one input called `A`, one control signal called enables, `E`, and one output called `Y`. The `E` signal can be active high, or active low: in both the cases the `A` signal passes throughout the TRI gate and the `Y` output is the same as `A`. If the `E` is not enabled (inactive high, or inactive low), the output `Y` assumes a value called `Z`: in the digital circuits, in particular in the logical circuits, the `Z` value indicates an high impedance, a synonym to indicate a floating state of the `Y` output. In the next paragraph we'll se the meaning of the `Z` value, even if from a logical point of view it is not useful for the boolean variables; it is only a useful value from a circuit point of view. The TRI gate has the following turth table:

| E | A | Y |
|---|---|---|
| 0 | 0 | Z |
| 0 | 1 | Z |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

The following figure represents two types of the TRI gate (active high and active low):

<!-- to do -->
*In Figure - On the left: a TRI logical gate with E active high. On the right: a TRI logical gate with !E active low*

Like the BUF gate, TRI is used to regenerate a digital signal, or to provide a clean digital signal to one, or more digital circuits. But TRI is also used to enable, or disable a specific circuit (like a portion of the central memory, or a I/O lines) in the modern system architectures.

### 03.03. Combinational Circuits
<!-- to do - definition of combinational circuits -->
<!-- to do - first canonic form with NOT, AND and OR -->
<!-- to do - second canonic form with NOT, AND and OR -->
<!-- to do - multilevel logic circuits -->
<!-- to do - NAND-only implementation -->
<!-- to do - NOR-only implementation -->
<!-- to do - don't care conditions -->
<!-- to do - implicants, prime implicants and essential prima implicants -->
<!-- to do - delays: raise time, fall time, propagation delay, contamination delay, path delay, critical path delay -->

### 03.04. Combinational Blocks
<!-- to do - half adder -->
<!-- to do - full adder -->
<!-- to do - multiplexer -->
<!-- to do - demultiplexer -->
<!-- to do - encoder -->
<!-- to do - priority encoder -->
<!-- to do - decoder -->
<!-- to do - comparator -->
<!-- to do - magnitude comparator -->
<!-- to do - PLA (Programmable Logic Array) -->
<!-- to do - PAL (Programmable Array Logic) -->

### 03.05. Sequential Circuits
<!-- to do - definition of sequential circuits -->
<!-- to do - difference between combinational and sequential circuits -->
<!-- to do - memory elements -->
<!-- to do - feedback concept -->
<!-- to do - clock signal -->
<!-- to do - synchronous sequential circuits -->
<!-- to do - asynchronous sequential circuits -->
<!-- to do - latches vs flip-flops -->
<!-- to do - SR latch -->
<!-- to do - D latch -->
<!-- to do - SR flip-flop -->
<!-- to do - D flip-flop -->
<!-- to do - JK flip-flop -->
<!-- to do - T flip-flop -->
<!-- to do - setup time -->
<!-- to do - hold time -->
<!-- to do - clock-to-Q delay -->
<!-- to do - metastability -->
<!-- to do - FSMs (Finite State Machines) -->
<!-- to do - Mealy machines -->
<!-- to do - Moore machines -->
<!-- to do - state diagram -->
<!-- to do - state table -->
<!-- to do - state minimization -->
<!-- to do - state encoding -->

### 03.06. Sequential Blocks
<!-- to do - register -->
<!-- to do - parallel register -->
<!-- to do - shift register -->
<!-- to do - serial-in serial-out (SISO) register -->
<!-- to do - serial-in parallel-out (SIPO) register -->
<!-- to do - parallel-in serial-out (PISO) register -->
<!-- to do - parallel-in parallel-out (PIPO) register -->
<!-- to do - universal shift register -->
<!-- to do - register with load control -->
<!-- to do - register with clear/reset -->
<!-- to do - synchronous counters -->
<!-- to do - asynchronous (ripple) counters -->
<!-- to do - up counter -->
<!-- to do - down counter -->
<!-- to do - up/down counter -->
<!-- to do - modulo-n counter -->
<!-- to do - ring counter -->
<!-- to do - Johnson counter -->
<!-- to do - sequence detector -->

### 03.07. HDLs (Hardware Description Languages)
<!-- to do - definition of hardware description languages (HDLs) -->
<!-- to do - role of HDLs in digital system design -->
<!-- to do - abstraction levels in HDL design: - behavioral level - register-transfer level (RTL) - structural level -->
<!-- to do - introduction to SystemVerilog -->
<!-- to do - module definition in SystemVerilog -->
<!-- to do - ports: input, output, inout -->
<!-- to do - data types: - logic - wire - reg - bit -->
<!-- to do - vectors and arrays --> 
<!-- to do - parameters and localparams -->
<!-- to do - operators in SystemVerilog: - arithmetic operators - logical operators - bitwise operators - relational operators - reduction operators -->
<!-- to do - continuous assignments (assign) -->
<!-- to do - procedural blocks: - always_comb - always_ff - always_latch -->
<!-- to do - blocking vs non-blocking assignments -->
<!-- to do - combinational circuit modeling in SystemVerilog -->
<!-- to do - sequential circuit modeling in SystemVerilog -->
<!-- to do - clocked logic description -->
<!-- to do - reset handling: - synchronous reset - asynchronous reset -->
<!-- to do - finite state machine (FSM) modeling in SystemVerilog -->
<!-- to do - enumerated types (enum) -->
<!-- to do - case statements -->
<!-- to do - if statements -->
<!-- to do - generate blocks -->
<!-- to do - hierarchy and modular design -->
<!-- to do - parameterized modules -->
<!-- to do - interfaces (basic concept) -->
<!-- to do - testbench structure -->
<!-- to do - simulation vs synthesis -->
<!-- to do - synthesis constraints (basic idea) -->
<!-- to do - FPGA implementation workflow (overview) -->