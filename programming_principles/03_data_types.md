# 02. Data Types

Python has the following data types:

- Text types: `str` (string).
- Numeric types: `int` (integer numbers), `float` (floating-point numbers), `complex` (complex numbers).
- Sequence types: `list`, `tuple` and `range`.
- Mapping types: `dict`.
- Set types: `set` and `frozenset`.
- Boolean types: `boolean`.
- Binary types: `bytes`, `bytearray` and `memoryview`.
- None types: `None`.

The `type()` function accepts a literal, variable, or constant and print its data type:

```python
a = 10
print(type(a)) # <class 'int'>

b = "A string"
print(type(b)) # <class 'str'>

c = False
print(type(c)) # <class 'bool'>

d = [1, 2, 3]
print(type(d)) # <class 'list'>
```

Python has some other built-in functions, parts of the PSL:

- `int()` converts to `int`.
- `bool()` converts to `bool`.
- `float()` converts to `float`.
- `str()` converts to `str`.
- `complex()` converts to `complex`.
- `range()` produces a range of values.
- `list()` creates a `list`.
- `dict()` creates a `dict`.
- `set()` creates a `set`.
- `bytes()` produces a serie of bytes.
- `frozenset()` create a `frozenset`.
- `bytearray()` and `memoryview()` are used to optimization.

A common use case where you tipically use the `int()` function when you prompt the age of the user:

```python
age = int(input("Your age: "))
print(age)
```