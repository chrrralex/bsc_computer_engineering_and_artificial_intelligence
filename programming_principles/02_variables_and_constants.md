# 01. Variables and Constants

A variable is a memory area with an identifier and a value. The identifier is a string you can use to refer to the variable without knowing anything about memory structure. A variable is a couple key-value where the value can change during the program execution.

You can declare a variable by using the assignment operator (=):

```python
aNumber = 10
aString = "This is a string"
```

A constant is a memory area with an identifier and a value that cannot change during the program execution. The identifier is a string you can use to refer to the variable without knowing anything about memory structure. Python hasn't a real keyword to declare a costant, but it's a best practice to use the uppercase for the constant identifiers:

```python
PI = 3.1415
DAYS_OF_WEEK = 7
```

You can declare multiple variable, each with the own value by using the following syntaxt:

```python
a, b = 10, 5
```

The `a` variable is equal to `10` and the `b` variable is equal to `5`. You can use the same syntaxt for the constant, but remember to use the uppercase instead of the lowercase:

```python
PI, DAYS_OF_WEEK = 3.1415, 7
```