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

**Coding of decimal numbers (floating-point numbers) with IEEE 754**: IEEE 754 (where IEEE is the acronym of Institute of Electrical and Electronics Engineers) is the most common used standard to represent decimal numbers in a digital system. Decimal numbers are also konwn as floating-point number. Originally enstabilished in 1985, IEEE 754 defines how a floting-point number with a specific precision should be represented and how the airthmetic between two, or more floating-point numbers works in a digital system. The IEEE 754 defines the various formats, interchange formats, rounding rules and various arithmetic operations (sum and product included). Standards defines the exception handling also, like division by `0`. The last update of the IEEE 754 happens in 2020 by the ISO (International Standardization for Organization) and it's called ISO/IEC 60559:2020.

Before analyzing the IEEE 754 standard, we talk about the scientific (or exponential) notation. This notation follows the following rule:

```
M * B^N
```

where:

- `M` is called mantissa.
- `B` is the base of the positional numeric system used to represent the number (for binary system, `B = 2`; for decimal system, `B = 10`).
- `N` is called exponent.

The previous notation is often abbreviated in `MeN`, or `MEN`. The decimal number is the result of the following operation: `M * B^N`. 

A floating-point number compliant with the IEEE 754 standard can have different formats, the three most used formats are:

- Single-precision floating-point number: uses 32 bits, or 4 Bytes, organized in this way:
    - `S`: `1` bit for the sign, called sign bit. It's equal to `1` if the mantissa is negative, `0` if the mantissa is positive.
    - `M`: `23` bits for the mantissa. The mantissa is part of a number in scientific notation, or a floating-point number, consisting of its significant digits. A mantissa is called normalised where it's one with only one 1 to the left of the decimal.
    - `E`: `8` bits for the exponent. The exponent is the number by which the mantissa must be multiplied. This number appears as an exponent of the base of the number represented (2 in the case of the binary system, 10 in the case of the decimal system).
- Double-precision floating-point number: uses 64 bits, or 8 Bytes, organized in this way:
    - `S`: `1` bit for the sign, called sign bit. It's equal to `1` if the mantissa is negative, `0` if the mantissa is positive.
    - `M`: `52` bits for the mantissa. The mantissa is part of a number in scientific notation, or a floating-point number, consisting of its significant digits. A mantissa is called normalised where it's one with only one 1 to the left of the decimal.
    - `E`: `11` bits for the exponent. The exponent is the number by which the mantissa must be multiplied. This number appears as an exponent of the base of the number represented (2 in the case of the binary system, 10 in the case of the decimal system).
- Quadruple-precision floating-point number: uses 64 bits, or 8 Bytes, organized in this way:
    - `S`: `1` bit for the sign, called sign bit. It's equal to `1` if the mantissa is negative, `0` if the mantissa is positive.
    - `M`: `113` bits for the mantissa. The mantissa is part of a number in scientific notation, or a floating-point number, consisting of its significant digits. A mantissa is called normalised where it's one with only one 1 to the left of the decimal.
    - `E`: `15` bits for the exponent. The exponent is the number by which the mantissa must be multiplied. This number appears as an exponent of the base of the number represented (2 in the case of the binary system, 10 in the case of the decimal system).

In the IEEE 754 standard, some values are particular:

- The `0` number is represented with all bits of `M` set to `0` and all bits of `E` set to `0`.
- The `Infinity` quantity is represented with all bits of `M` set to `0` and all bits of `E` set to `1`. This quantity tipically represent an overflow, cause the bits are not enough to represent the result, or the number.
- The `NaN` (Not a Number) case is represented with `M` different from `0` and all bits of `E` set to `1`. This value represent an error during a calculation.
- A denormalised mantissa has `M` different from `0` and the exponent `E` has all bits set to `0`. In this case, the number doesn't have an assumed leading one before the binary point.

**ASCII and EASCII**: ASCII (American Standard Code for Information Interchange) is a `7` bits standard created in the 1963 by the ANSI (American National Standards Institute) for representing a particular set of `95` (English language focused) printable and `33` control characters, for a total of `128` code points. A valid ASCII binary string consists in a `7` bits. Each combination of these `7` bits is a number between `0` and `2^7 - 1`, or between `0` and `127`: each number is called code point and it identifies a specific character uniquely. A variant of the ASCII coding is the EASCII (Extended ASCII). It extends the length of a code point from `7` to `8` bits, so it can represent numbers between `0` and `2^8 - 1`, or between `0` and `255`.

**Unicode and UTF-8**: Unicode, also called TUS (The Unicode Standard) is a character encoding standard maintained by the Unicode Consortium and designed to support the use of text all of the world's writing systems. Unicode has a very high number of code points. Unicode supports Chinese, Arabic, Japanese characters, emoji, many mathematical and cultural symbols and many other types of characters. It is truly a universal encoding that is updated daily by the Unicode Consortium.

Unicode defines two mapping methods: the UTF (Unicode Transformation Format) encodings, and the UCS (Universal Coded character Set) encodings. An encoding maps (possibly a subset of) the range of Unicode code points to sequences of values in some fixed-size range, called code units. All UTF encodings map code points to a unique sequence of bytes. The numbers in the names of the encodings indicate the number of bits per code unit (for UTF encodings) or the number of bytes per code unit (for UCS encodings and UTF-1). There are the following UTF encodings used by Unicode:

- UTF-8 (Uniform Transformation Format, 8 bits): it uses 8 bits units per code point, and has maximal compatibility with ASCII. Each code point can have from one, to four units. This is the most common used encoding for the web documents.
- UTF-16 (Uniform Transformation Format, 16 bits): it uses 16 bits units per code point.
- UTF-32 (Uniform Transformation Format, 32 bits): it uses 32 bits units per code point.

**Lossless coding for images**: PNG, GIF, and BMP are image formats that use lossless compression (or no compression in the case of BMP), meaning no information is lost during storage. PNG supports high-quality images and transparency with efficient compression. GIF supports up to 256 colors and simple animations. BMP typically stores raw pixel data and is mainly used for compatibility rather than compression efficiency.

**Lossy coding for images**: JPEG and AVIF are image formats that use lossy compression to significantly reduce file size by removing less perceptible visual details. JPEG is widely used for photographs due to its good compression-performance tradeoff. AVIF provides higher compression efficiency than JPEG with better image quality at smaller sizes. Both formats are commonly used for web and multimedia applications.

**Lossless coding for audios**: WAV and AIFF are lossless audio formats that store uncompressed or minimally compressed digital audio signals. They preserve the original recording quality without any loss of information. These formats are commonly used in professional audio editing and production environments. However, they require significantly more storage space compared to compressed formats.

**Lossy coding for audios**: MP3 and AAC are lossy audio compression formats designed to reduce file size by removing perceptually less important sound information. MP3 is one of the most widely used audio formats for music distribution. AAC provides better sound quality than MP3 at similar bitrates and is widely used in streaming services and mobile devices. Both formats are optimized for efficient storage and transmission.

**Lossless coding for videos**: FLAC and Lagarith are lossless compression codecs that preserve the original data without degradation. FLAC is primarily used for lossless audio compression, while Lagarith is used for lossless video compression in editing workflows. These codecs maintain exact original quality but produce larger files than lossy formats. They are commonly used in archival storage and professional media processing.

**Lossy coding for videos**: AVC (H.264) and MPEG-4 are lossy video compression standards designed to efficiently reduce video file size while maintaining acceptable visual quality. AVC is widely used in streaming platforms, Blu-ray discs, and video conferencing applications. MPEG-4 supports multimedia compression for video, audio, and interactive content. These codecs enable efficient transmission and storage of digital video.

### 00.03. Von Neumann Architecture

**Digital Computer**: a digital computer is a digital systems, a general purposes and electronic device that processes digital signals. A digital signal is a signal that can assume a specific set of values, or discrete values: a digital computer uses the binary system with binary digits (`0` and `1`) to represent data and instructions. A digital computer operates with `0` and `1` digits and processes one, or more programs during his lifecycle. It performs logical and arithmetic operations (like sum, comparison, logical AND, logical OR, logical NOT and some others). A digital computer is an automatic electronic device: it produces accurate and repeatable results. Moreover, a digital computer is a deterministic machine: the same inputs cause the same outputs. A digital computer cannot be a stochastic system (probability based).

**Program and Process**: program and process have an intimate relationship, very important both in the context of computer architecture and in the context of operating systems.

A program is an ordered set of instructions stored by the main memory of the system. A memory is an electronic device that allows the digital system to execute one, or more programs by storing each through certain physical principles, which electronics exploits to store bits. Remember that, in a computer (and digital systems in general), all is considered a bit, or a group of bits. A program is a static entity normally stored in the secondary memory (like HD -Hard Disk-, or SSD -Solid State Disk-). A program is an ordered set of machine-level or high-level instructions stored in memory and executed by the CPU to accomplish a computation or control operation.

A process is a dynamic entity stored in the main memory (also called central memory) of the computer that can assume different statuses during its execution. A process is a program in execution: a program is the blueprint, meanwhile the processs it's his instance. A program can be executed more than one times. Moreover, multiple processes can arise from a program and they're multiple instances of the same program, but which describe a different execution of the same. The CPU, the brain of the computer, executes the each instructions of the program.

**Von Neumann Architecture**: Von Neumann architecture is a computer design, proposed in 1945 by the Hungarian and American mathematician, physicist, computer scientist and engineer Jhon Von Neumann. This architecture is characterized by a shared memory and a shared system bus for both data and instructions. The followin figure shows how a typical Von Neumann system is organized:

<!-- to add -->
*In Figure: a typical Von Neumann system*

As you can see by osserving the figure, the CPU is composed by CU (Control Unit), ALU (Arithmetic-Logic Unit) and registers. Two of the most important registers are PC (Program Counter) and IR (Instruction Register): the first contains a pointer (a memory address) to the next instruction to execute, the second contains the current instruction in the execution phase. The CU is an internal component of the CPU that controls the CPU's interface with the outside and governs the signals inside it. The ALU is the internal component of the CPU that performs calculation, like logical AND, arithmetic sum, and so on.

The Von Neumann architecture is the foundation of the modern digital systems. All modern devices are based on the Von Neumann architecture. The key concepts of this architecture are:

- First of all, both data and instructions are stored into the same memory, called main (or central) memory. Program can be modified exactly like data. There is one space only for both data and instructions. The main memory is also called RAM (Random Access Memory): a memory that provides a fast and direct access to each memory cell, or location.
- A system bus allows the direct communication between CPU and memory (and viceversa) and between the CPU and the various I/O devices (and viceversa). System bus is the backbone of the entire system and it has three types of buses:
  - Address bus: it carries memory addresses (for read and write operations). It also carries the addresses of external memories, or devices that can be treated as memories.
  - Data bus: it carries data that the CPU requests, or delivers to a specific peripheral, or to memory.
  - Control bus: it carries control signals to govern communications, or to detect any malfunctions.
- CPU fetch the program from the memory, instruction by instruction, and execute it. CPU execute one instruction a time and it uses the PC register to track the next instruction to execute. The PC is a small and quick register directly accessible by the ALU, the internal component of the CPU that performs calculations. Instructions are executed one after another and the execution is controlled by the PC register.

In the next chapters we'll analyze in detail how each component of the Von Neumann architecture.

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

**Birth of the Microprogramming (1940s)**: in the late 1940s and early 1950s, microprogramming was introduced (notably by Maurice Wilkes) as a technique to simplify CPU control unit design. Instead of implementing complex control logic entirely in hardware, instructions were interpreted through sequences of simpler microinstructions stored in a control memory. This approach made processor design more flexible and easier to modify or extend. Microprogramming became widely used in early complex instruction set processors (CISC).

<!-- to do -  -->

**Birth of the Operating System (1960s)**: during the 1960s, the OS (Operating System) emerged as a key software layer between hardware and users. Systems like *IBM OS/360* introduced concepts such as multiprogramming, job scheduling, and memory management. Operating systems enabled efficient sharing of expensive computing resources among multiple users and programs. This marked the transition from single-program execution to structured system-level software environments.

**Expansion of the ISA (1970s)**: in the 1970s, many processors adopted increasingly complex Instruction Set Architectures (ISAs), characteristic of the CISC design philosophy. Manufacturers expanded instruction sets to support higher-level programming constructs and reduce program size. Architectures such as the early *x86* family exemplified this trend. This expansion aimed to shift complexity from software into hardware through richer machine instructions.

**Elimination of the Microprogramming (1980s)**: in the mid-1980s, the rise of RISC architectures reduced the reliance on microprogramming by favoring simpler instructions executed directly by hardwired control logic. Projects such as *MIPS* and *SPARC* demonstrated that simplified instruction sets could achieve higher performance through efficient pipelining. Although microprogramming was not completely eliminated, its role decreased in many new processor designs. Modern CPUs still use microcode internally for compatibility and complex instruction handling.

**Moore's Law**: formulated by Gordon Moore in 1965, observed that the number of transistors on an integrated circuit roughly doubles every 18–24 months. This trend has driven exponential growth in computing performance while reducing cost per transistor. It enabled the development of increasingly complex processors, memory systems, and integrated computing devices. Although its pace has slowed in recent years, Moore’s Law remains a central concept in semiconductor evolution.

### 00.07. History of the Computer Architectures

**Zeroth Generation - Mechanical Computers (1642-1945)**: the zeroth generation includes mechanical and electromechanical computing devices built before electronic computers. Notable examples include the *Pascaline* by Blaise Pascal (1642), Charles Babbage’s *Analytical Engine* (conceptual but foundational), and the *Harvard Mark I* (1944), an electromechanical programmable computer. These machines relied on gears, relays, and mechanical motion rather than electronic components. They established the basic principles of automated calculation and programmable computation.

**First Generation - Vacuum Tubes (1945-1955)**: the first generation of computers used vacuum tubes for circuitry and magnetic drums for memory. Iconic machines include *ENIAC* (1945), one of the first general-purpose electronic computers, *EDVAC*, which introduced the stored-program concept, and *UNIVAC I*, the first commercial computer in the United States. These systems were very large, consumed significant power, and generated considerable heat. Programming was performed using machine language and punched cards.

**Second Generation - Transistors (1955-1965)**: the second generation replaced vacuum tubes with transistors, making computers smaller, faster, and more reliable. Important examples include the *IBM 1401*, widely used for business applications, and the *IBM 7090*, designed for scientific computation. Magnetic core memory became standard, and higher-level programming languages such as FORTRAN and COBOL were introduced. This generation marked the transition toward more practical commercial computing systems.

**Third Generation - Integrated Circuits (1965-1985)**: the third generation introduced integrated circuits (ICs), allowing multiple transistors to be placed on a single chip and greatly improving performance and reliability. Representative machines include the *IBM System/360*, which standardized compatible computer families, and the *DEC PDP-8*, an influential minicomputer. Operating systems became more advanced, supporting multiprogramming and time-sharing. Computers became more accessible to universities and businesses.

**Four Generation - Very Large Scale Integration (1985-Today)**: the fourth generation is characterized by Very Large Scale Integration (VLSI), enabling thousands to millions of transistors on a single chip and leading to the development of microprocessors. Iconic systems include the *Intel 4004* (1971), the first commercial microprocessor, and early personal computers like the *Apple II* and *IBM PC*. This generation made personal computing widespread and dramatically reduced cost and size. Modern desktops, laptops, and servers are based on this technology.

**Five Generation - Low Power and Invisible Computers (1990-Today)**: the fifth generation focuses on low-power, highly integrated, and often invisible computing embedded into everyday environments. Examples include smartphones powered by ARM-based processors, embedded systems in IoT devices, and wearable computers such as smartwatches. Advances in parallel processing, AI acceleration, and mobile computing characterize this era. Computing has become pervasive, networked, and integrated seamlessly into daily life.