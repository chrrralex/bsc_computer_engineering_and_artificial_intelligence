# 08. Operators

# 08.01. Overview

An operator is a symbol that specifies an operation between one, two, or more variables, literals, or entities.

An operator can be:

- unary: if it operates with only one operand;
- binary: if it operates with two operands;
- ternary: if it operates with three operands.

Python provides many types of operators:

- arithmetic;
- assignment;
- logical;
- comparison;
- identity;
- bitwise;
- membership.

In this chapter we'll going to examine all these operators.

# 08.02. Airthmetic Operators

`+` is the sum operator, it's binary and it is associative from left to right:

```python
a = 10
b = 5
c = a + b
print(c) # 15
print(a + b + c + 10) # 25
```

`-` is the difference operator, it's binary and it is associative from left to right:

```python
a = 10
b = 5
c = a - b
print(c) # 5
print(a - b - c) # 0
```

`*` is the product operator, it's binary and it is associative from left to right:

```python
a = 2
b = 3
c = a * b
print(c) # 6
print(a * c * 10) # 120
```

`/` is the floating-point quotient operator, it's binary and it is associative from left to right:

```python
a = 10.0
b = 5.0
c = a / b
print(c) # 2.0
print(a / b / c) # 1.0
```

You have to pay attention with the second operand of the quotient operator, cause it cannot be `0`. If the second operand is `0`, then the Python interpreter throws the following error:

```python
print(10 / 0)
# ERROR!
# Traceback (most recent call last):
#   File "<main.py>", line 6, in <module>
# ZeroDivisionError: division by zero
```

In Python there is another way to make a division by two numbers: the integer quotient operator (`//`):

```python
a = 10.0
b = 6.7
c = a // b
print(c) # 1.0
```

The result of an expression like  `operand1 // operand2` is always an integer, or a floating-point number without any decimal digits.

`**` is the exponentiation operator, it's binary and it is associative from left to right:

```python
a = 2
b = 3
c = a ** b
print(c) # 2^3 = 2 * 2 * 2 = 8
```

`%` is the modulus operator, it's binary and it is associative from left to right. An expressione like `operand1 % operand2` always returns an (integer, or floating-point) number that is the remainder between the division `operand1 / operand2`:

```python
a = 10.5
b = 5.2
c = a % b
print(c) # 0.5
```

# 08.03. Assignment Operators

`=` is the assignment operator and it assignes the value on the right to the lvalue (contraction of "left value") at the right. This operation overwrites any previous value stored in the variable, for this reason this process is called "destructive". Any previous value associated to the lvalue will be lost. It's a binary operator and it is associative from left to right.

```python
a = 10
b = "A string"
print(a) # 10
a = b
print(a) # "A string"
```

There are many other compound assignment operators, that combine the assigment operator (`=`) with another airthmetic/bitwise operator (like `+`, or `>>`):

- `a += b`: shortcut of `a = a + b`.
- `a -= b`: shortcut of `a = a - b`.
- `a *= b`: shortcut of `a = a * b`.
- `a /= b`: shortcut of `a = a / b`.
- `a %= b`: shortcut of `a = a % b`.
- `a //= b`: shortcut of `a = a // b`.
- `a **= b`: shortcut of `a = a ** b`.
- `a &= b`: shortcut of `a = a & b`.
- `a |= b`: shortcut of `a = a | b`.
- `a ^= b`: shortcut of `a = a ^ b`.
- `a >>= b`: shortcut of `a = a >> b`.
- `a <<= b`: shortcut of `a = a << b`.

# 08.04. Logical Operators

`and` is the logical AND (or boolean AND) operator, it's binary and it associative from left to right. It returns `True` if and only if both first and second operands are `True`, otherwise it returns `False`.

```python
print(True and True) # True
print(True and False) # False
print(False and True) # False
print(False and False) # False
```

`or` is the logical OR (or boolean OR) operator, it's binary and it associative from left to right. It returns `True` if and at least one between first and second operands are `True`, otherwise it returns `False`.

```python
print(True or True) # True
print(True or False) # True
print(False or True) # True
print(False or False) # False
```

`not` is the logical NOT (or boolean NOT) operator, it's unary. It returns `True` if and only if the operand is `False`, otherwise it returns `False`. 

```python
print(not False) # True
print(not True) # False
```

Note that all these logical operators (`and`, `or` and `not`) return always a boolean value. Often, the logical operators are used to create more complex boolean expressions (expressions return a boolean value):

```python
a = 10
c = 1000
print(a < 100 and c * 2 >= 1000) # True
```

# 08.05. Comparison Operators

`==` is the equality operator, it returns `True` if the left operand is equal to the right operand. It's binary, it associative from left to right.

```python
print(10 == 2) # False
print(10 == 10) # True
```

`!=` is the not equality operator, it returns `True` if the left operand is different to the right operand. It's binary, it associative from left to right.

```python
print(10 != 2) # True
print(10 != 10) # False
```

`>` is the greather than operator, it returns `True` if the left operand is greather than right operand. It's binary, it associative from left to right.

```python
print(10 > 2) # True
print(10 > 10) # False
```

`<` is the lower than operator, it returns `True` if the left operand is lower than the right operand. It's binary, it associative from left to right.

```python
print(10 < 100) # True
print(10 < 10) # False
```

`>=` is the greather than, or euqal to operator, it returns `True` if the left operand is grather than, or equal to the right operand. It's binary, it associative from left to right.

```python
print(10 >= 10) # True
print(10 >= 100) # False
```

`<=` is the lower than, or equal to operator, it returns `True` if the left operand is lower than, or equal to the right operand. It's binary, it associative from left to right.

```python
print(10 <= 10) # True
print(10 <= 5) # False
```

# 08.06. Identity Operators

`is` operator returns `True` if both left and right operands are the same object (both have the same value and the same data type):

```python
a = 10
b = 10
c = 10.0
print(a is b) # True
print(a is c) # False, cause c is a floating-point number and a is an integer number
```

`is not` operator returns `True` if left and right operands are different object (they have a different value, or different data type):

```python
a = 10
b = 10
c = 10.0
print(a is not b) # False
print(a is not c) # True, cause c is a floating-point number and a is an integer number
```

# 08.07. Bitwise Operators

Bitwise operators operate a bit-level. They are:

- `a & b`: it's the bitwise AND operator, a binary operator that compares at bit-level `a` and `b`. It set a bit as `1` if both corresponding bits are `1`.
- `a | b`: it's the bitwise OR operator, a binary operator that compares at bit-level `a` and `b`. It set a bit as `1` if at least one of the corresponding bits is `1`.
- `~a`: it's the bitwise NOT operator, an unary operator that executes the one-complement. It set a bit as `1` if the corresponding bit is `0`, and viceversa.
- `a ^ b`: it's the bitwise XOR operator, a binary operator that compares at bit-level `a` and `b`. It set a bit as `1` if the corresponding bits are different (one is `0` and other is `1`), otherwise it set `0`.

Here's an example:

```python
a = 10          # 1010
b = 5           # 0101

print(a & b)    # 1010 &
                # 0101 =
                # 0000

print(a | b)    # 1010 |
                # 0101 =
                # 1111

print(a ^ b)    # 1010 ^
                # 0101 =
                # 1111

print(~a)       # ~1010 =
                # 0101
```

`<<` operator is the zero-fill left shift operator and `>>` is the signed right shift operator. Both are associative from left to right and both are binary operators. `<<` shifts left by pushing zeros in from the right and let the leftmost bits fall off, meanwhile `>>` shifts right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off. Here's an example:

```python
a = 10          # 1010
print(a << 3)   # 10 << 3 = 10 * 2^3 = 80

a = 80          # 1010000
print(a >> 3)   # 80 >> 3 = 80 / 2^3 = 10
```

Note that `>>` is equivalent to the quotient between `a` and `2^p`, where `p` is the second operand of the `>>` operator. 
Note that `<<` is equivalent to the product between `a` and `2^p`, where `p` is the second operand of the `<<` operator.

# 08.08. Membership Operators

We already analyzed a bit the membership operators: `in` and `not in`. These operators works with tuple, list, string and dictionaries and both returns a boolean value.

`in` returns `True` if the element specified as the left operand is present in the element specified as the right operand (a list, tuple, or other iterable):

```python
l = [ 1, 2, 3 ]
1 in l # True
10 in l # False
```

`not in` returns `True` if the element specified as the left operand isn't present in the element specified as the right operanìd (a list, tuple, or other iterable):

```python
l = [ 1, 2, 3 ]
1 not in l # False
10 not in l # True
```
