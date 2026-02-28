# 04. Literals

A literal is a value directly hardcoded into the source code. A literal has an own type. For example, `10` is an integer literal, meanwhile `"Hi!"` is a string literal.

An integer literal is an integer value. `int` data type allows both positive and negative numbers in the Python programming language:

```python
x = 100
y= +100 # positive number, with optional +
z = -7 # negative number, mandatory -
```

A floating point literal is a floating-point value. `float` data type allows both positive and negative numbers in the Python programming language:

```python
x = 10.5
y = 10. # optional decimal part, default is 0
z = .5 # optional integer part, default is 0
```

Python stores floating-point values by using the IEEE 754 standard:

- A single precision floating-point number has 32 bits (23 for mantissa, 1 for sign, 8 for exponent).
- A double precision floating-point number has 64 bits (52 for mantissa, 1 for sign, 11 for exponent).
- A quadruple precision floating-point number has 128 bits (112 for mantissa, 1 for sign, 15 for exponent).

You can specify floating-point literals with the exponential (or scientific) notation:

```python
10.5E3 # with uppercase E
10.5e3 # with lowercase e
.5e2 # without integer part
10.e7 # without decimal part
```

Into the numbers, especially for long numbers, you can use the underscore (`_`) to make the code more readable:

```python
1_000
1_500_000
10_000.10_23_24
```

Python supports the complex number also. A complex number is a number with a real part and a imaginary part. The imaginary part always ends with `j`. A complex number cannot have any real part.

```python
10 + 5j # both integer value, Python consider anyway floating-point numbers
10.5 + 2.7j # both floating-point value
.2 + .5j # noth with decimal part only
```

A string literal is a characters collection directly hardcoded into the code. A string can be enclosed in double, or single quotation marks:

```python
"This is a string"
'This is a string also'
```

You can use the truple double, or single quotation marks to enclose a string for preserving spaces and format:

```python
"""
This is
        a string
        with spaces.
"""
'''
This is
        a string
        with spaces
    also.
'''
```

Boolean literals are only two: `True`, or `False`. `True` is a truth value, while `False` is a falsity value.

```python
True
False
```

Remember that the first letter of the `True` and `False` literals are always specified in uppercase in Python.
