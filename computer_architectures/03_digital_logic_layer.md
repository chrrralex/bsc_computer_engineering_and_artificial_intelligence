# 03. Digital Logic Layer

### 03.01. Boolean Algebra

**Boolean Algebra**: boolean algebra is a branch of mathematics used to represent and manipulate logical variables and logical operations, where variables can take only two values. These values are called boolean literal and it can be assigned to the boolean variables.

**Boolean Variable**: a variable that can take only two possible values: 0, or 1. Boolean variables are the fundamental elements of the boolean algebra and the digital logic circuits. Normally, a boolean variable is indicated by an uppercase letter, like `A`, or `B`.

**Boolean Literal**: a fixed logical value that can be `0`, or `1` only. In boolean algebra only two values are usable: `0` (also called `false`, or `low`) and `1` (also called `true`, or `high`). Note that there are only two valid boolean literals in the boolean algebra: `0` and `1`.

**Voltage and Boolean Algebra Relationship**: positive logic means and high value of tension (normally Vcc, or Vdd) is considered the `1` logical value, meanwhile a low value of tension (normally GND) is considered the `0` logical value. Digital circuits have the own specifications about the voltage levels: for example, an integrated circuit could consider as `1` logical value a voltage between 2.5 V and 5 V and as `0` logical value a voltage between 0 V and 1.5 V. It depends on the construction techniques.

**Positive and Negative Logic**: a positive logic associates the `1` logical value to an high voltage and the `0` logical value to a low voltage. Differently, the negative logic associates the `1` logical value to a low voltage and the `0` logical value to an high voltage.

**Functionally Complete Set**: as any other branch of the mathemtatics, in boolean algebra is considered a functionally complete set a set of boolean operators that can be used to express any boolean expression. A set of logic operations is functionally complete if every Boolean expression can be built using only those operations. Often, in boolean algebra the most common functionally complete set is: `AND`, `OR`, `NOT`. Another functionally complete set is the `NAND` gate alone and another also is the `NOR` alone: both the two previous sets are commonly used for the VLSI (Very Large Scale Integration) digital circuits implementation.

**Boolean Expression**: is a mathematical expression used in the boolean algebra that combines boolean literals (`0` or `1`) using logic operations like `AND`, `OR`, and `NOT` to produce a result that is also a boolean value between `0` and `1`. For example, the following is a boolean expression:

```
Y = AB + C(!D) + !(E + !(A))
```

Where: `A`, `B`, `C`, `D` and `E` are all boolean variables. `!` is the `NOT` (or inverter) operator; `+` is the `OR` (or logical disjunction) operator; `x` (often not indicated) is the `AND` (or logical conjunction) operator. These three boolean operators are basically the main boolean operators. The previous expression is also called boolean function of five boolean variables and is also indicated in this way:

```
Y = f(A, B, C, D, E) = AB + C(!D) + !(E + !(A))
```

We'll see in details how the basic boolean algebra operators works.

**Turth Table**: a turth table is the main way to describe the relationship between a set of boolean variables and a boolean expression. Given a boolean expression, its turth table is composed by an header and a body. The header defines at least N + 1 columns, where N is the number of the boolean variables present in the boolean expression and the remaining column is the result of that boolean expression. For example, consider the following expression:

```
Y = !(AB) + AB(!C) + A
```

In this example three boolean variables appear: `A`, `B` and `C`. So the tirth table has `3 + 1` columns. The body of the turth table has 2^N rows: in this case, cause we have three boolean variables, the turth table has 2^3 = 8 rows. For each row appear a specific combination of the `A`, `B` and `C` boolean variables. Normally, the combinations follow the binary count and in the our example we start from `000` and we and to `111`. The following is the turth table of the previous boolean expression, without values for the `Y` column:

| A | B | C | Y |
|---|---|---|---|
| 0 | 0 | 0 |   |
| 0 | 0 | 1 |   |
| 0 | 1 | 0 |   |
| 0 | 1 | 1 |   |
| 1 | 0 | 0 |   |
| 1 | 0 | 1 |   |
| 1 | 1 | 0 |   |
| 1 | 1 | 1 |   |

Note that, in decimal, each combination varying from `0` to `2^N - 1`, in our case from `0` (`000`) to `7` (`111`). When you creating a turth table for a complex boolean expression, it's useful to add some columns to track the values of the subexpressions, like `!(AB)`, or `AB(!C)`, or `A`. For example, we can add four other columns in the previous turth table, each with intermediate values:

| A | B | C | !C | AB | !(AB) | AB(!C) | Y |
|---|---|---|----|----|-------|--------|---|
| 0 | 0 | 0 | 1  | 0  |   1   |   0    |   |
| 0 | 0 | 1 | 0  | 0  |   1   |   0    |   |
| 0 | 1 | 0 | 1  | 0  |   1   |   0    |   |
| 0 | 1 | 1 | 0  | 0  |   1   |   0    |   |
| 1 | 0 | 0 | 1  | 0  |   1   |   0    |   |
| 1 | 0 | 1 | 0  | 0  |   1   |   0    |   |
| 1 | 1 | 0 | 1  | 1  |   0   |   1    |   |
| 1 | 1 | 1 | 0  | 1  |   0   |   0    |   |

Finally, we can easily calculate the values for the `Y` column (the result of the boolean expression):

| A | B | C | !C | AB | !(AB) | AB(!C) | Y |
|---|---|---|----|----|-------|--------|---|
| 0 | 0 | 0 | 1  | 0  |   1   |   0    | 1 |
| 0 | 0 | 1 | 0  | 0  |   1   |   0    | 1 |
| 0 | 1 | 0 | 1  | 0  |   1   |   0    | 1 |
| 0 | 1 | 1 | 0  | 0  |   1   |   0    | 1 |
| 1 | 0 | 0 | 1  | 0  |   1   |   0    | 1 |
| 1 | 0 | 1 | 0  | 0  |   1   |   0    | 1 |
| 1 | 1 | 0 | 1  | 1  |   0   |   1    | 1 |
| 1 | 1 | 1 | 0  | 1  |   0   |   0    | 0 |

As we'll see in the next paragraphs, this expression is a NAND of the following three boolean variables: `A`, `B` and `C`. 

**NOT operator**: the inverter operator is a one-operand boolean operator that performs a complement of the input and it's indicated with `!`. The turth table of the `NOT` operator is:

| A | !A |
|---|---|
| 0 | 1 |
| 1 | 0 |

**AND operator**: the logical conjunction operator is a two-operands boolean operator that returns `1` only if both inputs are `1` and it's indicated with `x` (often implicit, like in the classic algebra). The `AND` boolean operator follows the same rules of the product operator used in the classic algebra: any value multiplied by `0` returns `0` as a result. The turth table of the `AND` operator is:

| A | B | AB |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**OR operator**: the logical disjunction operator is a two-operands boolean operator that returns `1` if at least one input, or both inputs are `1` and it's indicated with `+`. The `OR` boolean operator follows the same rule of the sum operator (`+`) of the classic algebra, but there is an exception: `1 + 1` is `1`, not `10`. Remember that the plus symbol, in boolean algebra, is used to indicate the `OR` logical operator. The turth table of the `OR` operator is:

| A | B | A + B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

**NAND operator**: the `NAND` operator is a derived logical operator with two-operands that returns `0` only if both the inputs are `0` and it's indicated with the expression `!(AB)`. The turth table of the `NAND` operator is the same of the `AND`, excepts the result column, that is the complement:

| A | B | !(AB) |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**NOR operator**: the `NOR` operator is a derived logical operator with two-operands that returns `1` only if both the inputs are `0` and it's indicated with the expression `!(A + B)`. The turth table of the `NOR` operator is the same of the `OR`, excepts the result column, that is the complement:

| A | B | !(A + B) |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

**XOR operator**: the `XOR` operator is a derived logical operator with two-operands that returns `1` only if the inputs are different: one is `0` and the remaning is `1`. It's indicated with the circled-sum operator: `⊕`. The turth table of the `XOR` operator is the same of the `OR`, excepts the last row of the result column, that is `0`:

| A | B | A ⊕ B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**XNOR operator**: the `XNOR` operator is a derived logical operator with two-operands that returns `1` only if the inputs are equal: one both are `0`, or both are `1`. It's indicated with the circled-sum operator and this expression: `!(A ⊕ B)`. The turth table of the `XNOR` operator is the complement of the `XOR`:

| A | B | A ⊕ B |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

<!-- to do - one-variable principles -->
<!-- to do - two-variables principles -->
<!-- to do - de morgan laws -->
<!-- to do - minterms and maxterms -->
<!-- to do - implicating and implicated -->
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

<!-- to add -->
*In Figure - The NOT logical gate with A input and Y output*


**BUF gate**: the BUF gate, contraction of BUFfer, is a basic logic gate that produces the same logical value of its input. It accepts an input and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = A`. This gate serves no logically useful function from a logical point of view. The BUF logical gate has the following turth table:

| A | Y |
|---|---|
| 0 | 0 |
| 1 | 1 |

The BUF gate is represented in the following figure:

<!-- to add -->
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

<!-- to add -->
*In Figure - The AND logical gate with A and B inputs and Y output*

An AND gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, an AND3 gate (AND gate with 3 inputs) has a lower delay than an AND8 (AND gate with 8 inputs). Here's an example of an AND4 gate:

<!-- to add -->
*In Figure - The AND4 logical gate with four inputs and Y output*

**OR gate**: the OR gate is a basic logic gate that produces the OR logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the input `A` and the output `Y` is `Y = A + B`, where the OR function is representend by the sum operator (`+`), like in the classic algebra. The OR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

The OR gate is represented in the following figure:

<!-- to add -->
*In Figure - The OR logical gate with A and B inputs and Y output*

An OR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, an OR3 gate (OR gate with 3 inputs) has a lower delay than an OR8 (OR gate with 8 inputs). Here's an example of an OR4 gate:

<!-- to add -->
*In Figure - The OR4 logical gate with four inputs and Y output*

**NAND gate**: the NAND gate is a basic logic gate that produces the complement of the AND logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = !(A x B)`, often abbreviated in `Y = !(AB)`, like in the classic algebra. The NAND logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

The NAND gate is represented in the following figure:

<!-- to add -->
*In Figure - The NAND logical gate with A and B inputs and Y output*

An NAND gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a NAND3 gate (NAND gate with 3 inputs) has a lower delay than a NAND8 (NAND gate with 8 inputs). Here's an example of a NAND4 gate:

<!-- to add -->
*In Figure - The NAND4 logical gate with four inputs and Y output*

**NOR gate**: the NOR gate is a basic logic gate that produces the complement of the OR logical function of its input. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = !(A + B)`, where the sum operator (`+`) represents the OR function in the boolean algebra, like in the classic algebra. The NOR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

The NOR gate is represented in the following figure:

<!-- to add -->
*In Figure - The NOR logical gate with A and B inputs and Y output*

An NOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a NOR3 gate (NOR gate with 3 inputs) has a lower delay than a NOR8 (NOR gate with 8 inputs). Here's an example of a NOR4 gate:

<!-- to add -->
*In Figure - The NOR4 logical gate with four inputs and Y output*

**XOR gate**: the XOR gate (eXclusive OR) is a basic logic gate that produces the `1` logical output only if the number of inputs set to `1` is odd. The basic gate accepts two inputs and it produces an output. The boolean relationship between the `A` and `B` inputs and the output `Y` is `Y = A ⊕ B`, where the circled sum operator (`⊕`) represents the XOR function in the boolean algebra. The XOR logical gate has the following turth table:

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

The XOR gate is represented in the following figure:

<!-- to add -->
*In Figure - The XOR logical gate with A and B inputs and Y output*

An XOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a XOR3 gate (XOR gate with 3 inputs) has a lower delay than a XOR8 (XOR gate with 8 inputs). Here's an example of a XOR4 gate:

<!-- to add -->
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

<!-- to add -->
*In Figure - The XNOR logical gate with A and B inputs and Y output*

An XNOR gate can have more than two inputs, but the gate delay introduced by its circuitry depends in a linear way by the number of the inputs accepted. For example, a XNOR3 gate (XNOR gate with 3 inputs) has a lower delay than a XNOR8 (XNOR gate with 8 inputs). Here's an example of a XNOR4 gate:

<!-- to add -->
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

<!-- to add -->
*In Figure - On the left: a TRI logical gate with E active high. On the right: a TRI logical gate with !E active low*

Like the BUF gate, TRI is used to regenerate a digital signal, or to provide a clean digital signal to one, or more digital circuits. But TRI is also used to enable, or disable a specific circuit (like a portion of the central memory, or a I/O lines) in the modern system architectures.

### 03.03. Combinational Circuits

**Minterms and Maxterms**: a minterm is a product (AND combination) of all variables in a boolean function, each appearing exactly once in either complemented or uncomplemented form, that evaluates to `1` for exactly one input combination. A maxterm is a sum (OR combination) of all variables in a boolean function, each appearing exactly once in either complemented or uncomplemented form, that evaluates to `0` for exactly one input combination.

**Implicant and Prime Implicant**: an implicant is a product term of a Boolean function that implies the function value 1 for all input combinations covered by that term. A prime implicant is an implicant that cannot be combined with another implicant to eliminate a variable and still remain an implicant of the function.

**Implicate and Prime Implicate**: an implicate is a sum term (OR combination of literals) that is true whenever the Boolean function is true, meaning the function logically implies that term. A prime implicate is an implicate that cannot be simplified further by removing literals without changing the function.

**Combinational Circuit**: a circuit called combinational is a digital circuit (or digital network) where the outputs depend only and only from the current inputs. A combinational circuit can have zero, one, or more inputs and can have zero, one, or more outputs. The logical gates analyzed in the previous paragraph are all examples of the simplest combinational circuits. The following figure shows an example of combinational circuit:

<!-- to add -->
*In Figure: an example of a combinational circuit*

The following rules defines how a combinational circuit can be implemented:

- Each element of a combinational network is combinational.
- Each node of a combinational network is an input of the network, or it's linked to a single output of a network.
- A combinational network doesn't contain any cyclic link.

The following figure shows some examples of a non-combinational networks: the (a) network isn't combinational cause there is a cyclic link; the (b) network isn't combinational cause the outputs of two different elements is linked to the same input of a combinational element; the (c) network isn't combinational, but it's a particular sequential network (we'll analyze the sequential networks in the next paragraph).

**First Canonic Form**: the boolean algebra allows the designer to completely describe a combinational network. The FCF (First Canonic Form), also called SOP (Sum of Products), consists of an OR of products, where each product is an AND. Given a combinational circuit, like the circuit shown in the following figure:

<!-- to add -->
*In Figure: an example of combinational circuit that can be described with the SOP form*

we can create the turth table by following the same rules analyzed at the start of the present chapter. The following turth table is the relationship between the inputs `A`, `B` and `C` and the output `Y`:

| A | B | C | Y | Minterms |
| - | - | - | - | -------- |
| 0 | 0 | 0 | 0 | m0 |
| 0 | 0 | 1 | 1 | m1 |
| 0 | 1 | 0 | 0 | m2 |
| 0 | 1 | 1 | 0 | m3 |
| 1 | 0 | 0 | 0 | m4 |
| 1 | 0 | 1 | 0 | m5 |
| 1 | 1 | 0 | 1 | m6 |
| 1 | 1 | 1 | 1 | m7 |

The first step to create a SOP form of the combinational circuit is to consider the rows of the turth table where `Y = 1`. The rows `1`, `6` and `7` are the rows where `Y = 1`. This means that we consider the following minterms: `m0`, `m6` and `m7`. We can write the `Y` output is `1` where at least one of the previous specified minterms is `1`:

```
Y = f(A, B, C) = m0 + m6 + m7
```

Or, equivalently:

```
Y = f(A, B, C) = ∑(m0, m6, m7)
```

Or, in another way:

```
Y = f(A, B, C) = ∑(0, 6, 7)
```

Where:

- The `m0` minterm is the product `!(A)!(B)!(C)`.
- The `m6` minterm is the product `AB!(C)`.
- The `m7` minterm is the product `ABC`.

The previous boolean formula is equivalent to the following:

```
Y = !(A)!(B)!(C) + AB!(C) + ABC
```

The following figure shows the two-level combinational circuit described by the previous formula:

<!-- to add -->
*In Figure: two-level combinational circuit described by the formula `Y = !(A)!(B)!(C) + AB!(C) + ABC`*

Note that to write the SOP form you can take each boolean variable in straight form if it's `1`, in negated form if it's `0`. The SOP form is an example of two-levels logic: the first level is a set of AND gates, the second level is a "big" OR with all minterms accepted as inputs.

**Second Canonic Form**: the boolean algebra allows the designer to completely describe a combinational network. The SCF (Second Canonic Form), also called POS (Product of Sums), consists of an AND of sums, where each sum is an OR. Given a combinational circuit, like the circuit shown in the following figure:

<!-- to add -->
*In Figure: an example of combinational circuit that can be described with the POS form*

we can create the turth table by following the same rules analyzed at the start of the present chapter. The following turth table is the relationship between the inputs `A`, `B` and `C` and the output `Y`:

| A | B | C | Y | Maxterms |
| - | - | - | - | -------- |
| 0 | 0 | 0 | 0 | M0 |
| 0 | 0 | 1 | 1 | M1 |
| 0 | 1 | 0 | 0 | M2 |
| 0 | 1 | 1 | 0 | M3 |
| 1 | 0 | 0 | 0 | M4 |
| 1 | 0 | 1 | 0 | M5 |
| 1 | 1 | 0 | 1 | M6 |
| 1 | 1 | 1 | 1 | M7 |

The first step to create a POS form of the combinational circuit is to consider the rows of the turth table where `Y = 0`. The rows `0`, `2`, `3`, `4` and `5` are the rows where `Y = 0`. This means that we consider the following minterms: `M0`, `M2`, `M3`, `M4` and `M5`. We can write the `Y` output is `1` where all the previous specified maxterms is `0`:

```
Y = f(A, B, C) = M0 * M2 * M3 * M4 * M5
```

Or, equivalently:

```
Y = f(A, B, C) = Π(M0, M2, M3, M4, M5)
```

Or, in another way:

```
Y = f(A, B, C) = Π(0, 2, 3, 4, 5)
```

Where:

- The `M0` minterm is the product `A + B + C`.
- The `M2` minterm is the product `A + !(B) + C`.
- The `M3` minterm is the product `A + !(B) + !(C)`.
- The `M4` minterm is the product `!(A) + B + C`.
- The `M5` minterm is the product `!(A) + B + !(C)`.

The previous boolean formula is equivalent to the following:

```
Y = (A + B + C)(A + !(B) + C)(A + !(B) + !(C))(!(A) + B + C)(!(A) + B + !(C))
```

The following figure shows the two-level combinational circuit described by the previous formula:

<!-- to add -->
*In Figure: two-level combinational circuit described by the formula `Y = (A + B + C)(A + !(B) + C)(A + !(B) + !(C))(!(A) + B + C)(!(A) + B + !(C))`*

Note that to write the POS form you can take each boolean variable in straight form if it's `0`, in negated form if it's `1` (basically the opposite of the SOP form). Also the POS form is an example of two-levels logic: the first level is a set of OR gates, the second level is a "big" AND with all maxterms accepted as inputs.

**NAND-only and NOR-only Implementations**: most common IC (Integrated Circuits) and most common commercial chips uses a NAND-only implementation, or a NOR-only implementation.

NAND-only implementation uses the NAND logical gate only to implement any other logical gate. The following figure shows how each logical gate can be implemented by using NAND basic gate:

<!-- to add -->
*In Figure: NAND gate used to implement NOT, AND and OR logical gates*

NOR-only implementation uses the NOR logical gate only to implement any other logical gate. The following figure shows how each logical gate can be implemented by using NOR basic gate:

<!-- to add -->
*In Figure: NOR gate used to implement NOT, AND and OR logical gates*

Both NAND-only and NOR-only implementations are used in the modern VLSI (Very Large Scale Integration) IC. NAND and NOR gates need a less number of transistors (nMOS, pMOS, or CMOS): this is the main reason that the modern CPUs, caches and other chips are based on NAND-only, or NOR-only logical gates.

**Multilevel Logic Circuits**: a multilevel logic circuit is a combinational circuit where at least one (or more) input pass through more than two logical gates to reach the output. The following figure shows an example of a multilevel logic circuit:

<!-- to add -->
*In Figure: an example of a multilevel logic circuit*

**Don't Care Conditions**: are input combinations for which the output of a boolean function is not specified or not relevant to the operation of the circuit. In a turth table, they're are usually represented by `X`, meaning the output can be either 0 or 1, whichever simplifies circuit. Normally, don't care conditions occur when some input combinations never appear in practice, or a certain combinations are unused, or some outputs are irrelevant for specific states. The following figure shows how a combinational circuit can be optimized and implemented with don't care conditions:

<!-- to add -->
*In Figure: how a combinational circuit can be represented*

Now, in the combinational circuit and sequential circuit we can use three symbols:

- `0` is tipically a low voltage (in the positive logic).
- `1` is tipically an high voltage (in the positive logic).
- `X` is "anything", it's a don't care condition for a particular boolean variable.

**High Impedance State**: indicated with `Z`, it represents a high-impedance state (also called tristate) in digital circuits, meaning the output is electrically disconnected from the circuit. The following figure shows a tristate, a logical gate with two inputs and one output:

<!-- to add -->
*In Figure: the tristate gate, with A as data input, E as control input and Y as data output*

When `E = 1`, the tristate is transparent and each value of `A` is propagated (with a small delay) and rigenerated in the `Y` output. When `E = 0`, the tristate is opaque and `Y = Z`. This means the `Y` output is in an high impedance state. Note that a Z output is not a logic value, but a circuit condition indicating the output is electrically inactive and does not influence the signal line. A `Z` output (high-impedance state) means the output pin of a digital circuit is electrically disconnected from the signal line, behaving like an open switch.

**Delay**: there are different types of delays in a combinational circuit.

Rise time is the time required for a signal to transition from a low logic level to a high logic level, typically measured between 10% and 90% of the final voltage value. It characterizes how quickly a digital signal switches from `0` to `1` and it's an important parameter of the basic logical gates.

Fall time is the time required for a signal to transition from a high logic level to a low logic level, typically measured between 90% and 10% of the initial voltage value. It describes how quickly a signal switches from `1` to `0` and it's an important parameter of the basic logical gates.

Propagation delay is the time between a change at the input of a logic gate or circuit and the corresponding change at its output. It represents the response time of the circuit and is usually measured between 50% voltage transition points. It is indicated with `tpd` (time propagation delay).

Contamination delay is the minimum time after an input change at which the output may begin to change. It represents the earliest possible effect of an input transition on the output. It is indicated with `tcd` (time contamination delay).

**Critical Path Delays**: the propagation delay of the entire logical circuit is the maximum path delay among all possible input-to-output paths in a combinational circuit. It determines the minimum clock period and therefore the maximum operating speed of the circuit. The propagation delay of a multilevel logic circuit is the sum of the propagation delays of the gates along the longest input-to-output path, called the critical path. For example, consider the following logic circuit:

<!-- to add -->
*In Figure: an example of a combinational circuit with a critical path, used to calculate the propagation delay of the circuit `tpd`*

In the critical path we've three logical gates: a NOT, an AND and an OR. The propagation delay `tpd` of the circuit is the sum of the propagation delay of each logical gate:

- `tpdNOT` for the NOT gate.
- `tpdAND` for the AND gate.
- `tpdOR` for the OR gate.

So, the total propagation delay, indicated with `tpd`, is:

```
tpd = tpdNOT + tpdAND + tpdOR
```

The contamination delay of the entire logical circuit is the minimum path delay between the inputs change and the output change. The contamination delay of a multilevel logic circuit is the sum of the contamination delays of the gates along the smallest input-to-output path, called the shortest path. For example, consider the following logic circuit:

<!-- to add -->
*In Figure: an example of a combinational circuit with a shortest path, used to calculate the contamination delay of the circuit `tcd`*

In the shortest path we've two logical gates: a NOT and a NAND. The contamination delay `tcd` of the circuit is the sum of the contamination delay of each logical gate:

- `tcdNOT` for the NOT gate.
- `tcdMAND` for the NAND gate.

So, the total contamination delay, indicated with `tcd`, is:

```
tcd = tcdNOT + tcdNAND
```

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