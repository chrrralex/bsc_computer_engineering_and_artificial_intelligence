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

In Python, an empty dictionary is represented by curly brackets: `{}`. An empty dictionary is a dict that hasn't any items.

### 15.02. Read, Add, Update and Remove Items

You can access to an item by using the subscript operator, represented by the square brackets (`[]`):

```python
d = { "a": 1, "b": 2, "c": 3 }
print(d["a"]) # 1
```

You can also get an item by using the `get()` method directly from the dict:

```python
print(d.get("a")) # 1
```

To get the list of the keys stored in a dict, you can use the `keys()` method:

```python
print(d.keys()) # dict_keys([ 'a', 'b', 'c' ])
```

As you can see, the value returned from the `keys()` method is of the `dict_keys` type. The list of the keys is a view of the dictionary, meaning that any changes done to the dictionary will be reflected in the keys list.

To get the list of the values stored in a dict, you can use the `values()` method:

```python
print(d.values()) # dict_values([ 1, 2, 3 ])
```

There is another method, `items()`. This method returns a list of tuples: each first value of the tuple is the dictionary key, meanwhile each second value of the tuple is the dictionary value.

```python
print(d.items()) # dict_items([ ('a', 1), ('b', 2), ('c', 3) ])
```

The returned value is of the `dict_items` data type.

The `in` operator can be used with a dictionaries also: on its left you can specify the dict key and on its right the dict where you want to check if the key exists. Here's an example:

```python
if "a" in d:
    print("a is a key stored in d") # printed
if "e" in d:
    print("e is a key stored in d") # not printed
```

You can change a value by using the corrisponding key, specifying the key into  the subscript operator:

```python
d["a"] = 10
d["b"] = 20
d["c"] = 30
print(d) # { 'a': 10, 'b': 20, 'c': 30 }
```

To change an item, there is the `update()` method also: it accepts a dictionary, or an iterable object with key-value pairs as an argument. Thanks to the `update()` method, you can change more items in a single step. Here's an example:

```python
d.update({ "a": 50 })
print(d) # { 'a': 50, 'b': 20, 'c': 30 }
d.update({ "b": 70, "c": 90 })
print(d) # { 'a': 50, 'b': 70, 'c': 90 }
```

You can add an item by specifying the new key into the subscript operator, on the left of the assignment operator, like this:

```python
d["d"] = 110
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'd': 110 }
```

Another way to add an item is through the `update()` method, in the same way we've shown before:

```python
d.update({ "e": 130 })
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'e': 130 }
d.update({ "f": 150, "g": 170 })
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'e': 130, 'f': 150, 'g': 170 }
```

Finally, you can remove an item through its key, by using the `pop()` method, in this way:

```python
d.pop("g")
d.pop("a")
d.pop("c")
d.pop("f")
print(d) # { 'b': 70, 'e': 130 }
```

If you're using a Python version higher, or equal to 3.7, you can use the `popitem()` method: this removes the last item specified in the dictionary. Here's an example:

```python
d.popitem()
print(d) # { 'b': 70 }
```

Another way to remove a dict item is the `del` keyword:

```python
del d["b"]
print(d) # {}
```

### 15.03. Loop Dictionaries

If you try to use a `for` loop over a dictionary, like this:

```python
d = { "a": 1, "b": 2, "c": 3 }
for x in d:
    print(x) # a, b, c
```

Happens that the `x` variable assumes each key of the dictionary: first the `"a"` variable, second the `"b"` and finally the `"c"`. To prints the key-value pairs you can use the `items()` method, as we've seen in the previous paragraph:

```python
for t in d.items():
    print(t[0] + " - " + str(t[1])) # a - 1, b - 2, c - 3
```

The previous `for` can be written also in this way:

```python
for k, v in d.items():
    print(k + " - " + str(v)) # a - 1, b - 2, c - 3
```

and the output is the same. Note that we've used the `str()` method to convert an integer value to a string value (Python interpreter throws an error if you try to concatenate a string with an integer value through the `+` operator).

You can iterate over the keys also by using the `keys()` method:

```python
for k in d.keys():
    print(x) # a, b, c
```

or you can iterate over the values also by using the `values()` method:

```python
for v in d.values():
    print(v) # 1, 2, 3
```

### 15.04. Copy Dictionaries

You cannot copy a dictionary simply by typing `dict2 = dict1`, where `dict1` and `dict2` are two dictionaries. The expression `dict1 = dict2` means that `dict2` will only be a reference to `dict1`, and changes made in `dict1` will automatically also be made in `dict2`. This is not a copy.

There are ways to make a copy, one way is to use the built-in Dictionary method `copy()`:

```python
dict1 = { "a": 1, "b": 2, "c": 3 }
dict2 = dict1.copy()
dict2.update({ "a": 100, "b": 200 })
print(dict1) # { 'a': 1, 'b': 2, 'c': 3 }
print(dict2) # { 'a': 100, 'b': 200, 'c': 3 }
```

### 15.05. Methods

`clear()` removes all the elements from the dictionary:

```python
d = { "a": 1, "b": 2, "c": 3 }
d.clear()
print(d) # {}
```

`fromkeys()` returns a dictionary with the specified keys and value:

```python
ks = ('key1', 'key2', 'key3')
v = 0
d = dict.fromkeys(x, y)
print(d) # { 'key1': 0, 'key2': 0, 'key3': 0 }
```

`setdefault()` returns the value of the specified key. If the key does not exist: insert the key, with the specified value. Here's an example:

```python
car = {
  "brand": "Peugeot",
  "model": "208",
  "year": 2023
}

x = car.setdefault("model", "-")
print(x) # 208

y = car.setdefault("color", "-")
print(y) # "-"
```
