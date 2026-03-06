# 15. Dictionaries

### 15.01. Overview

Dictionary (often contracted in dict) is a key-value data structure allows the developer to associate each value to a particular key. For example, the following is a dictionary literal and it's introduced by the curly brackets:

```python
person = {
    "firstName": "Christian",
    "lastName": "Atzeni",
    "age": 28
}
```

The previous dictionary, stored in the `person` variable, has three keys:

- `firstName`: a string containing `"Christian"`.
- `lastName`: a string containing `"Atzeni"`.
- `age`: an integer number containing `28`.

In Python version 3.7 (or higher), dictionaries are ordered. In Python 3.6 and earlier, dictionaries are unordered. It means that the items have a defined order, and that order will not change. Dictionaries are mutable (or changeable) and you can easily prints a dict with the built-in `print()` function.

```python
print(person) # { 'firstName': 'Christian', 'lastName': 'Atzeni', 'age': 28 }
```

You can use the subscript operator (the square brackets `[]`) to access to a particular property of the dict:

```python
print(person["age"]) # 28
```

You can change a value by using the subscript operator (with the key of the value to modify inside it) at the left of the assignment operator:

```python
person["age"] = 30
print(person["age"]) # 30
```

Duplicates keys, in a dict, aren't allowed. A key must be unique: if you try to use the same key, the previous value will be replaced. You can add a new key by specifying it inside the subscript operator, at the left of the assignment operator:

```python
person["role"] = "Developer"
```

If you apply the `len()` built-in function with a dict, it returns the length of the dict, which is the number of items stored in the dictionary:

```python
d = {
    "a": 1,
    "b": 2,
    "c": 3
}
print(len(d)) # 3
```

Python provides the `dict()` built-in function, that accepts a set of named parameters and returns the resulting dictionary:

```python
d = dict(a = 1, b = 2, c = 3)
print(d) # { 'a': 1, 'b': 2, 'c': 3 }
```

Finally, to finish this small overview, the `type()` built-in function, applied to a dict, returns the following output:

```bash
<class 'dict'>
```

### 15.02. Read, Add, Update and Remove Items
<!-- to do -->

### 15.03. Loop Dictionaries
<!-- to do -->

### 15.04. Copy Dictionaries
<!-- to do -->

### 15.05. Methods
<!-- to do -->
