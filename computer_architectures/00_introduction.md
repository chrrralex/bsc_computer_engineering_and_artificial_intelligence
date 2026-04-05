# 00. Introduction

### 00.01. Manage complexity

**Abstraction**: is the process throughout a real system is converted in a model. Abstraction consists in two steps:

1. Consider the essential and useful details only.
2. Delete the useless details.

An abstraction allows an architect to see a model at different point of views. For example, an electronics engineer might see a computer as a set of circuits, while a microprocessor designer might see it as a set of combinatorial and sequential logic blocks.

**Three-Y Model**: the three-Y (from the three principles herarchY, modularitY and regularitY) is a model very useful to study, deisgn and understand a modern digital system. The three principles are:

- Hierarchy: each complex system, like a modern digital system, can be seen as a tree of components. The root component is the conceptual view of the considered system and it has the generic details only. The root component is composed by one, two, or more other components: you can inspect these components, that revelas other details about the system. Hierarchy is the design principle of organizing a complex system into multiple levels of abstraction, where each level is built from simpler components of lower levels. The following figure shows how you can think to the hierarchy principle:

<!-- to add -->
*In Figure: hierarchy design principle*

- Modularity: is the design principle of dividing a system into independent functional blocks called modules, each performing a specific task. Each independent entity is also called component, or subsystem. For example, the CPU of a computer has the main purpose to execute programs; the main memory of a computer has the main purpose to store programs; the system bus of a computer has the main purpose to allow the communication between each subsystems (CPU, RAM, I/O devices, HD, SSD, GPU, TPU and so on). Each component of the system must be completely defined in terms of inputs, outputs and control signals. Moreover, a component must be as generic as possible. 

<!-- to add -->
*In Figure: modularity design principle*

- Regularity: is the design principle of using repeated structures and uniform patterns throughout a system. In general: if a problem has been already resolved by another component, the simplest and most efficient solution is often to reuse that component. For the same problem, or task, the system must use the same component, or module. In this way, the layout of the system becomes predictable.

<!-- to add -->
*In Figure: regularity design principle*

**Discipline**: is a set of rules and conventions that define how signals behave and interact in a system, ensuring predictable and correct operation of interconnected components. In the context of digital circuits, discipline usually refers to the rule that signals are interpreted only as discrete logic levels (typically 0 and 1) rather than continuous analog values. Each components must include the complete specifications of its behavior.

### 00.02. Digital Abstraction

**Bit**: a bit is the simplest digital unit that a digital system can process during an execution. A bit (contraction of the two terms "binary" and "digit") is a bistable value which can vary from `0` to `1`: `0` is also called `low`, or `0 V`, or `-5 V`; `1` is also called `high`, or `5 V`, or `+5 V`. A bit is normally represented by a specific level of the voltage. If you have a string of `N` bit, you can represent `2^N` different combinations: from `0` to `2^N - 1` (the string of all bits set to `0` is part of the possible and allowed combinations).

**Information Quantity**: a discrete variable is a variable that can assume one of a finite statuses. A discrete variable with `N` statuses can be represented by `log2(N)` (to be prceise from `ceil(log2(N))`). For example, a semaphore can be in three statuses: yellow, green and red. Two bits are sufficient to represent its status: `00` for the yellow, `01` for the green and `10` for the red (`11` isn't used, or isn't a valid status, or maybe it can be used to indicate an error).

**Information Hierarchy**: in the following chapters we'll analyze in detail how the hierarchical memory is organized and why is organized in this way. Fundamentally, a modern memory organizes bits in the following way:

- Bit: it can be `0`, or `1`.
- Nibble: it's composed by four bits, from `0000` to `1111` (`2^4 = 16`) combinations. It's half of a Byte.
- Byte: it's composed by eight bits, from `00000000` to `11111111` (`2^8 = 256`) combinations.
- Word: modern memory system is organized in more lines; each lines has the same size, often a multiple of a Byte. Modern digital system has a main memory with a line of `32`, or `64` Bytes (`256`, or `512` bits).
- Half-Word: it's half of a word. For example, if a memory is organized in word of `32` Bytes, an half-word is composed by `16` Bytes (or `128` bits).

**msb, lsb, MSB and LSB**: a string of bit is composed by a specific number of binary digits, in which each digit can be `0`, or `1`. The position of each digit progressively increase from right to left, it starts from `0` and finishes to `N - 1`, where `N` is the length of the binary string. We defined:

- lsb (least significant bit): the first bit of the string, that is the bit located to the far right of the string.
- msb (most significant bit): the last bit of the string, that is the bit locate to the far left of the string.
- LSB (Least Significant Byte): the group of eight bits located to the for right of the string (the first eight bits).
- MSB (Most Significant Byte): the group of eight bits located to the for left of the string (the last eight bits).

Let's take an example. In the following binary string:

```
10010011 10100000 11110000
```

- lsb is `0`,
- msb is `1`,
- LSB is `11110000`,
- MSB is `10010011`.

**Positional Numeric Systems**: a positional numeric system is a numeric system in which each digit of the number has a specific weight based on its position into the number-self. There are four important positional numeric systems used in computer science:

- Binary System: composed by only two digits, `1` and `0`.
- Octal System; composed by eight digits, from `0` to `7`.
- Decimal System: the most common used by the human, composed by ten digits, from `0` to `9`.
- Hexadecimal System: composed by sixteen digits, from `0` to `9` and from `A` (or `a`) to `F` (or `f`). The digits from `A` to `F` represents the numbers from `10` to `15` in the decimal system.

To understand positional numeric system, we consider the following decimal number:

```
1236
```

It's composed by four digits, from left to right: `1`, `2`, `3` and `6`. The base of a positional numeric system is the number of digits that it can use: in our case, the base is `10`. The position starts from `0` (the first digit on the right side) and it's incremented one by one as you move from right to left. In our example, the positions are:

```
6 at positon 0
3 at position 1
2 at position 2
1 at position 3
```

In general, a number composed by `N` digits has the positions from `0` to `N - 1`. How can you calculate the weight associated to each digit of a number? Easy, you can use this rule:

```
D * B^P
```

Where:

- `D` is the digit (in decimal system, a number between `0` and `9`);
- `B` is the base (for decimal system is `10`);
- `P` is the position of the `D` digit (for a number with `N` digits, it can be from `0` to `N - 1`).

So, the weight of each decimal digit in our example is:

```
6 * 10^0 = 6 x 1 = 6
3 * 10^1 = 3 x 10 = 30
2 * 10^2 = 2 x 100 = 200
1 * 10^3 = 1 x 1000 = 1000
```

If you sum all weights, you'll obtain the original number:

```
6 + 30 + 200 + 1000 = 1236
```

That's it! For the binary system, the game is the same. If we have the following binary number:

```
1010
```

The `B` base is `2`, and the positions of each digit (`1`, or `0`) is:

```
0 at position 0
1 at position 1
0 at position 2
1 at position 3
```

We can calculate the weight of each position with the same rule (`D * B^P`):

```
0 * 2^0 = 0 * 0 = 0
1 * 2^1 = 1 * 2 = 2
0 * 2^2 = 0 * 4 = 0
1 * 2^3 = 1 * 8 = 8
```

And we can verify if all weights are correct by executing the sum of each weight:

```
0 + 2 + 0 + 8 = 10
```

`10` (in decimal) is equivalent to `1010` in binary.

**Binary to Decimal Conversion**: this operation convert a number expressed in the binary positional numeric system to a number expressed in decimal positional numeric system.

```
Binary: 1010
Decimal: ?

Bin-to-Dec Conversion:
1010 = (1 * 2^3) + (0 * 2^2) + (1 * 2^1) + (0 * 2^0) = 8 + 0 + 2 + 0 = 10

Binary: 1010
Decimal: 10
```

**Decimal to Binary Conversion**: this operation convert a number expressed in the decimal positional numeric system to a number expressed in binary positional numeric system.

```
Decimal: 10
Binary: ?

Dec-to-Bin Conversion:
10 / 2 = 5, remainder is 0 <- this is the lsb (least significant bit)
5 / 2 = 2, remainder is 1
2 / 2 = 1, remainder is 0
1 / 2 = 0, remainder is 1 <- this is the msb (most significant bit)

Decimal: 10
Binary: 1010
```

**Binary to Octal Conversion**: this operation convert a number expressed in the binary positional numeric system to a number expressed in octal positional numeric system.

```
Binary: 1000 (with groups: 001 000)
Octal: ?

Bin-to-Oct Conversion:
000 is 0 in the octal numeric positional system
001 is 1 in the octal numeric positional system

Binary: 001000
Octal: 10
```

This conversion is possible cause there is a direct correspondence between each three binary digits and each one octal digit. The corrispondences are:

| Binary Digits | Octal Digit |
| ------------- | ----------- |
| 000 | 0 |
| 001 | 1 |
| 010 | 2 |
| 011 | 3 |
| 100 | 4 |
| 101 | 5 |
| 110 | 6 |
| 111 | 7 |

**Octal to Binary Conversion**: this operation convert a number expressed in the octal positional numeric system to a number expressed in binary positional numeric system.

```
Octal: 174
Binary: ?

Oct-to-Bin Conversion:
4 is 100 in binary
7 is 111 in binary
1 is 001 (or 1) in binary

Octal: 174
Binary: 001111100, or 1111100
```

This conversion is possible cause there is a direct correspondence between each three binary digits and each one octal digit. The corrispondences are:

| Binary Digits | Octal Digit |
| ------------- | ----------- |
| 000 | 0 |
| 001 | 1 |
| 010 | 2 |
| 011 | 3 |
| 100 | 4 |
| 101 | 5 |
| 110 | 6 |
| 111 | 7 |

**Binary to Hexadecimal Conversion**: this operation convert a number expressed in the binary positional numeric system to a number expressed in hexadecimal positional numeric system.

```
Binary: 1111 1010 0000 0010
Hexadecimal: ?

Bin-to-Hex Conversion:
0010 in binary is 2 in hexadecimal
0000 in binary is 0 in hexadecimal
1010 in binary is 10 in decimal, that is A in hexadecimal
1111 in binary is 15 in decimal, that is F in hexadecimal

Binary: 1111 1010 0000 0010
Hexadecimal: FA02
```

This conversion is possible cause there is a direct correspondence between each four binary digits and each one hexadecimal digit. The corrispondences are:

| Binary Digits | Hexadecimal Digit | Decimal Digits |
| ------------- | ----------------- | -------------- |
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |
| 1010 | A (or a) | 10 |
| 1011 | B (or b) | 11 |
| 1100 | C (or c) | 12 |
| 1101 | D (or d) | 13 |
| 1110 | E (or e) | 14 |
| 1111 | F (or f) | 15 |

**Hexadecimal to Binary Conversion**: this operation convert a number expressed in the hexadecimal positional numeric system to a number expressed in binary positional numeric system.

```
Hexadecimal: FFC8
Binary: ?

Hex-to-Bin Conversion:
8 in hexadecimal is 8 in decimal, that is is 1000 in binary
C in hexadecimal is 12 in decimal, that is is 1100 in binary
F in hexadecimal is 15 in decimal, that is is 1111 in binary
F in hexadecimal is 15 in decimal, that is is 1111 in binary

Hexadecimal: FFC8
Binary: 1111 1111 1100 1000
```

This conversion is possible cause there is a direct correspondence between each four binary digits and each one hexadecimal digit. The corrispondences are:

| Binary Digits | Hexadecimal Digit | Decimal Digits |
| ------------- | ----------------- | -------------- |
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |
| 1010 | A (or a) | 10 |
| 1011 | B (or b) | 11 |
| 1100 | C (or c) | 12 |
| 1101 | D (or d) | 13 |
| 1110 | E (or e) | 14 |
| 1111 | F (or f) | 15 |

**Binary Sum**: the sum between two binary numbers is the most common operation executed by a digital system, or a CPU. The sum of two binary numbers follows the same rules of the sum between two decimal numbers. Here's an example:

```
A: 1101
B: 0101

A   1 1 0 1 +
B   0 1 0 1 =
--------------

Step 1:
1 + 1 = 0 with carry

        1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
           0

Step 2:
1 + 0 + 0 = 1 without carry

        1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
        1 0

Step 3:
1 + 1 = 0 with carry

    1   1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
      0 1 0

Step 4:
1 + 1 + 0 = 0 with carry

    1   1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
  1 0  0 1 0

Results: 10010
```

**Binary 1-Complement**: 1-complement is a binary operation in which each binary digit takes on the inverse of its value. If a digit is `1`, it's converted to `0`; viceversa, if a digit is `0`, it's converted to `1`. Here's an example:

```
Binary:             10 10 00 11
1-complement:       01 01 11 00
```

The 1-complement operation is very useful to represent negative number in the module-and-sign number representation in a memory of a digital system. We'll analyze the various coding techniques of numbers in the next paragraph. 

**Binary 2-Complement**: 2-complement is a binary operation in which each binary digit takes on the inverse of its value and, after all digits are changed, 1 is added to the result. 2-complement consists in two steps:

1. Calculate the 1-complement of the number.
2. Add 1 to the 1-complement of the number. This is the 2-complement. 

Here's an example:

```
Binary:             10 10 00 11

Step 1:
1-complement:       01 01 11 00

Step 2:
Add 1:              01 01 11 00 +
                    00 00 00 01 =
                    -------------
                    01 01 11 01
```

The 2-complement operation is very useful to represent negative number in the 2-complement number representation in a memory of a digital system. We'll analyze the various coding techniques of numbers in the next paragraph. 

**Binary Product**: the product between two binary numbers is one of the most common operation executed by a digital system, or a CPU. The product of two binary numbers follows the same rules of the product between two decimal numbers. Here's an example:

```
A: 1101
B: 0101

A   1 1 0 1 +
B   0 1 0 1 =
--------------

Step 1:
Multiply 1 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1

Step 2:
Multiply 0 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0  

Step 3:
Multiply 1 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1

Step 4:
Multiply 1 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1
  0 0 0 0

Step 5:
Sum of all partial results

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1
  0 0 0 0
-----------------
  1 0 0 0 0 0 1

Results: 1000001
```

### 00.04. Data Representation

**Coding of natural numbers (unsigned integers)**: binary encoding is normally used to represent natural numbers, or positive integers (including zero) within a computer's memory. All bits are reserved to represent the magnitude of the number. With `N` bit it's possible to represent all the numbers between `0` and `2^N - 1`, with a total of `2^N` possible values. Positive integers are also called number without sign, cause there is no bit to track the sign (if the number is positive, or negative). Modern digital systems, with x32 and x64 architectures, can represent integers without sign with 32, or 64 bits, or more (128, 256). Programming languages like Python, for example, allows the developer to store integer without sign (or unsigned integers) with arbitrary size, based on memory availability.

This is the natural number line that can be represented with `3` bits in the binary coding:

```
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimal:        0     1     2     3     4     5     6     7
Binary:         000   001   010   011   100   101   110   111
```

**Coding of relative numbers (signed integers) with 1-complement**: 1-complement (or one-complement) encoding is normally used to represent relative numbers, or integers with sign (including zero) within a computer's memory. Integers with sign are also called signed integers. With `N` bits, `N - 1` bits are reserved to represent the magnitude of the number and the msb (most significant bit) is used to represent the sign: `0` if the number is positive, `1` if the number is negative. With `N` bit it's possible to represent:

- all the positive integers between `+ 0` and `+ 2^(N - 1) - 1`,
- all the negative integers between `- 0` and `- 2^(N - 1) + 1`.

Why `2^(N - 1)` and not `2^N`? Because one bit is reserved to the sign. 1-complement is a strange coding, cause there are two representations for the zero: `-0` is the negative zero and `+0` is the positive zero (both represent the same number: zero). Moreover, sums and products between two, or more numbers coded with 1-complement are difficult to process, or calculate. Note that, also with 1-complement coding there is one bit for the sign (the sign bit), we can still represent `2^N` different numbers, even if zero has two representations (so in reality `2^N - 1`).

This is the relative number line that can be represented with `3` bits in the 1-complement coding:

```
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimal:        -3    -2    -1    -0    +0    +1    +2    +3
Binary:         111   110   101   100   000   001   010   011
```

**Coding of relative numbers (signed integers) with 2-complement**: 2-complement (or two-complement) encoding is normally used to represent relative numbers, or integers with sign (including zero) within a computer's memory. Integers with sign are also called signed integers. With `N` bits, `N - 1` bits are reserved to represent the magnitude of the number and the msb (most significant bit) is used to represent the sign: `0` if the number is positive, `1` if the number is negative. With `N` bit it's possible to represent:

- all the positive integers between `+ 0` and `+ 2^(N - 1) - 1`,
- all the negative integers between `- 0` and `- 2^(N - 1)`.

Why `2^(N - 1)` and not `2^N`? Because one bit is reserved to the sign. Another thing to consider is that with the 2-complement coding for the relative numbers, one more negative number can be represented than positive numbers, as this coding eliminates the double representation for zero: all 0 bits are the only possible representation for this number. This makes the coding itself much less strange and more consistent. For example, the 2-complement coding with `4` bit has one and only one representation for the zero: all bits set to `0` (`0000`). The representation of zero is unique in the 2-complement coding. Sums and products between two, or more numbers coded with 2-complement are very simple to process, because both sum and product can be executed as for the binary number. Note that, also with 2-complement coding there is one bit for the sign (the sign bit), we can still represent `2^N` different numbers.

This is the relative number line that can be represented with `3` bits in the 2-complement coding:

```
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimal:        -4    -3    -2    -1    +0    +1    +2    +3
Binary:         100   101   110   111   000   001   010   011
```

As you can see by osserving the line, here's some considerations:

- `-1` has all bits set to `1`, included the sign bit.
- The lower number (`-4` for the 2-complement coding with `3` bits) has all bits set to `0`, except the sign bit, that is `1`.
- The highest number (`+3` for the 2-complement coding with `3` bits) has all bits set to `1`, except the sign bit, that is `0`.
- `0` has one and only one representation, with all bits set to `0`.

<!-- to do - floating-point numbers with IEEE 754 -->
<!-- to do - textual data with ASCII and EASCII -->
<!-- to do - textual data with Unicode -->
<!-- to do - images with lossless coding: PNG, GIF and BMP -->
<!-- to do - images with lossy coding: JPEG and AVIF -->
<!-- to do - audios with lossless coding: WAV and AIFF -->
<!-- to do - audios with lossy coding: MP3 and AAC -->
<!-- to do - videos with lossless coding: FLAC and Lagarith -->
<!-- to do - videos with lossy coding: AVC and MPEG-4 -->
<!-- to do - metric units -->

### 00.03. Von Neumann Architecture
<!-- to do - definition of digital computer -->
<!-- to do - definition of program -->
<!-- to do - definition of process -->
<!-- to do - basic structure of a digital computer: the Von Neumann architecture -->
<!-- to do - the CPU component: ALU, CU and Registers -->
<!-- to do - the RAM component and the memory address -->
<!-- to do - the I/O Devices -->
<!-- to do - the system bus: data bus, address bus and control bus -->

### 00.04. Modern Digital Computer
<!-- to do - language definition -->
<!-- to do - machine language, low-level language, mid-level language and high-level language -->
<!-- to do - interpretation vs translation -->
<!-- to do - virtual machine definition -->
<!-- to do - multilevel machines and the layered model -->
<!-- to do - actual multilevel machines -->
<!-- to do - layer 0 overview: digital logic layer -->
<!-- to do - layer 1 overview: microarchitecture layer -->
<!-- to do - layer 2 overview: architecture layer and the ISA (Instruction Set Architecture) -->
<!-- to do - layer 3 overview: operating system machine layer -->
<!-- to do - layer 4 overview: assembler layer -->
<!-- to do - layer 5 overview: applications and problem-oriented languages layer -->

### 00.05. Architectures Types
<!-- to do - definition of CPU, processor, multiprocessor and core -->
<!-- to do - Flynn's taxonomy: SISD, SIMD, MISD and MIMD architectures -->
<!-- to do - memory architectures: Von Neumann, Harvard and Modified Harvard architectures -->
<!-- to do - parallel computing architectures: scalar processors, vector processors, array processors, multiprocessors systems, multicore systems -->
<!-- to do - processing organization: centralized systems, parallel systems and distribuited systems -->
<!-- to do - types of computers: embedded systems, personal computers, mobile and game computers, workstations, mainframes, supercomputers, clusters -->

### 00.06. History of the Multilevel Machines
<!-- to do - the birth of the microprogramming (1940s) -->
<!-- to do - the rise of the operating system (1960s) -->
<!-- to do - the expansion of the ISA (1970s) -->
<!-- to do - the elimination of the microprogramming (1980s) -->
<!-- to do - Moore's law -->

### 00.07. History of the Computer Architectures
<!-- to do - zeroth generation: mechanical computers (1642-1945) -->
<!-- to do - first generation: vacuum tubes (1945-1955) -->
<!-- to do - second generation: transistors (1955-1965) -->
<!-- to do - third generation: integrated circuits (1975-1985) -->
<!-- to do - fourth generation: VLSI (Very Large Scale Integration) (1965-Today) -->
<!-- to do - fifth generation: low-power and invisible computers (1990-Today) -->