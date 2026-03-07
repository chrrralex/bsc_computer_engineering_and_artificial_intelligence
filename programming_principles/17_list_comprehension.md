# 17. List Comprehension

List comprehension offers a shorter syntax when you want to create a new list based on the values of an existing list. For example: based on a list `fruits`, you want a new list, containing only the fruits with the letter "a" in the name. Without list comprehension you will have to write a for statement with a conditional test inside:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = []

for x in fruits:
  if "a" in x:
    newlist.append(x)

print(newlist)
```

With list comprehension you can do all that with only one line of code:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

A list comprehension has the following syntaxt:

```python
[expression for item in iterable if condition]
```

where:
- `expression` is a valid Python expression used to manipulate each element;
- `item` is the variable name that assumes each value of the list;
- `iterable` is the list you want to iterate;
- `condition` is a boolean condition used to filter elements of the `iterable`. It's optional and it can be omitted.

In the following we're going to see some examples, fromt easiest to harder. The original list is:

```python
l = [ 1, 2, 3, 4, 5 ]
```

Example #1: create a list from another list.

```python
newl = [e for e in l]
print(newl) # [ 1, 2, 3, 4, 5 ]
```

Example #2: create a list from another list, where each element is multiplied with `2`.

```python
newl = [e * 2 for e in l]
print(newl) # [ 2, 4, 6, 8, 10 ]
```

Example #3: create a list from another list, with only even numbers.

```python
newl = [e for e in l if e % 2 == 0]
print(newl) # [ 2, 4 ]
```

Example #4: create a list from another list, with only even numbers, but multiplied with `2`.

```python
newl = [e * 2 for e in l if e % 2 == 0]
print(newl) # [ 4, 8 ]
```

Example #5: create a list from another list, with only even numbers, but they are squared.

```python
newl = [e**2 for e in l if e % 2 == 0]
print(newl) # [ 4, 16 ]
```

Example #6: create a list from another list in which each element is `"even"`, or `"odd"` in based of the element. This example uses the inline `if` syntaxt to reach the goal.

```python
newl = ["even" if e % 2 == 0 else "odd" for e in l]
print(newl) # [ "odd", "even", "odd", "even", "odd" ]
```

Example #7: more `for` inside a list comprehension. In the following example we invoke for two times the `range()` function. The following code:

```python
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs) # [ (0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2) ]
```

is equivalent to the following:

```python
pairs = []
for x in range(3):
    for y in range(3):
        pairs.append((x, y))
print(pairs) # [ (0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2) ]
```
