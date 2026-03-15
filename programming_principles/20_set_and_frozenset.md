# 20. Set and FrozenSet

A Python a set is an iterable, mutable, unordered data type that is optimized to store unique values. A set is enclosed by the curly brackets. In short:

- a set is mutable: its can be modified by adding, updating, or removing one, or more items;
- a set is unordered: for the purpose, doesn't mean the order of the elements in a set;
- a set allows unique value only: all duplicated values are ignored and a set stores only unique elements.

You can create a set from a set literal in this way:

```python
s = { 1, 2, 3 }
print(s) # { 1, 2, 3 }
```

If you try to specify one, or more duplicated elements, the set will consider the unique elements only:

```python
s = { 1, 2, 2, 2, 3, 3, 3 }
print(s) # { 1, 2, 3 }
```

In short, a set removes duplicated values automatically.

The `len()` returns the number of elements in a set:

```python
s = { 1, 2, 3, 4, 5 }
print(len(s)) # 5
```

The `min()` and `max()` functions return the minimum and the maximum value of the set:

```python
s = { 1, 2, 3 }
print(min(s)) # 1
print(max(s)) # 3
```

You can convert lists and tuples into a set by using the `set()` built-in function:

```python
s1 = set([ 1, 2, 3 ])
s2 = set(( "a", "b", "c" ))
print(s1) # { 1, 2, 3 }
print(s2) # { "a", "b", "c" }
```

You can't use the curly brackets without nothing inside (`{}`) to indicate an empty set, cause the Python interpreter consider it as an empty dict (a dict without any keys and values). To create an empty set, you can simply use the `set()` built-in function, like this:

```python
s = set()
print(s) # set()
```

You can add an element with `add()`, or multiple elements with `update()`. If you try to add an already-existing element, the set ignored it:

```python
s = set()
s.add(1)
s.add(1)
s.add(2)
s.update([ 1, 2, 3, 4 ])
print(s) # { 1, 2, 3, 4 }
```

You can use `remove()` to delete an element (if the element doesn't exist, Python will throw an error):

```python
s = { 10, 20, 30 }
s.remove(10)
s.remove(100) # ERROR! KeyError: 100
```

The `discard()` method is the same as `remove()`, but if the specified element doesn't exist, Python will not throw any error:

```python
s = { 10, 20, 30 }
s.discard(10)
s.discard(100) # 100 isn't in the set, but no error is thrown
```

You can check if an element is in the set by using the `in` and `not in` operators:

```python
s = { 1, 2, 3 }
print(1 in s) # True
print(10 not in s) # True
print(100 in s) # False
```

You can execute various operations with set:

- `|` is the union operator.
- `&` is the intersection operator.
- `-` is the difference operator.
- `^` is the symmetric difference operator.

Here's some examples:

```python
a = { 1, 2, 3 }
b = { 3, 4, 5 }

print(a | b) # { 1, 2, 3, 4, 5 }
print(a & b) # { 3 }
print(a - b) # { 1, 2 }
print(a ^ b) # { 1, 2, 4, 5 }
```

A frozenset is the immutable version of a set: once it's created, it cannot be modified. Once you create a frozenset, you cannot add, update, or remove any element in the frozenset. A frozetset is still stores unique, unordered elements, just like a normal set.

You can create a frozenset with the `frozenset()` built-in function:

```python
fs = frozenset([ 1, 1, 2, 3, 4, 4, 5 ])
print(fs) # frozenset({ 1, 2, 3, 4, 5 })
```

As you can see, Python always specifies the printed entity is a frozenset by using the expression `frozenset(elements)`.

If you try to add an element, you'll get an error:

```python
fs.add(10) # ERROR! AttributeError: 'frozenset' object has no attribute 'add'
```

Frozensets can be used with the set operators:

```python
a = frozenset({ 1, 2, 3 })
b = frozenset({ 3, 4, 5 })

print(a | b) # frozenset({ 1, 2, 3, 4, 5 })
print(a & b) # frozenset({ 3 })
print(a - b) # frozenset({ 1, 2 })
print(a ^  b) # frozenset({ 1, 2, 4, 5 })
```

Being an immutable type, unlike a regular set, a frozenset can be used as a key in a dictionary, although this is not often seen as a practical practice. Here's an example:

```python
d = {
    frozenset({ 1, 2, 3 }): "Hello!"
}
print(d[frozenset({ 1, 2, 3 })]) # "Hello!"
```

You can create an empty frozenset in this way:

```python
fs = frozenset()
print(fs) # fs = frozenset()
```

`len()`, `min()` and `max()` works with a frozenset exactly like they work with a set.
