# 06. Tuples

# 06.01. Overview

A tuple is a collection type used to store multiple values. A tuple is an unchangeable data structure, it means the elements cannot be modified. A tuple is an ordered data structure, like lists in Python. A tuple is defined by the round brackets `()`.

```python
t = ( "apple", "banana", "cherry" )
```

A tuple, in Python, allows duplicate values:

```python
t = ( "apple", "apple", "banana", "cherry", "orange", "orange" )
```

To discover the length of a tuple, you can use the `len()` built-in function in Python:

```python
t = ( 1, 2, 3, 4, 5 )
len(t) # 5
```

If you need to create a tuple with only one element, Python doesn't recognize it as a tuple if a comma after the element is not specified. Remember that the round brackets are used for expressions also, for this reason you must specify the comma (`,`) immediately after the element:

```python
t = ( "apple", )
t = ( 1, )
not_a_tuple = (10) # Python recognize it as an integer number, not as a tuple
```

A tuple can contain different data types:

```python
t = ( 1, True, "apple", 10.50, [ 1, 2, 3 ] )
```

In the previous case, the first item is an integer number, the second is a boolean value, the third is a floating-point number and the fourth is a list.

To inspect the data type of a tuple, you can use `type()`:

```python
t = (10,0)
type(t) # <class 'tuple'>
```

Python provides the `tuple()` built-in function, also called tuple constructor. It accepts any iterable (like the `list()` function) and returns a tuple with the same elements of the passed iterable.

# 06.02. Item Access

Like a list, you can access to a specific item of a tuple by using an index. The index is an integer value between `0` and `len(t) - 1`, where `t` is the considered tuple:

```python
t = ( 10, 20, 30 )
t[0] # 10
t[2] # 20
```

Negative values are allowed and in this case the count starts from the end of the tuple:

```python
t = ( "apple", "cherry", "orange" )
t[-1] # "orange"
```

Like lists, you can use the range of indexes also:

```python
t = ( "apple", "cherry", "orange" )
t[-3:-1] # ( "apple", "cherry" )
```

The syntaxt of the range operator is the same as we saw for lists. Remember that:

- `[n:m]` returns the elements from `n` included to `m` exluded.
- `[:m]` returns the elements from `0` included to `m` exluded.
- `[n:]` returns the elements from `n` included to `len(t) -  1` included.
- `[:]` returns a copy of the entire tuple.

If you want to check if an item is present in a tuple, you can use the `in` operator:

```python
t = ( 1, 2, 3 )
10 in t # False
3 in t # True
```

Note that the `in` operator always returns a boolean value: `True` if the element is present, `False` otherwise.

# 06.03. Item Update

Once a tuple is created, you cannot change any values. Tuples are uncheangable (or immutable): it means no update operation are allowed. One of the "garbage" ways to change an item of a tuple is:

- Convert a tuple into a list, that is mutable.
- Change the item.
- Convert the updated list into a tuple, that is immutable.

Here's an example:

```python
t = ( 1, 2, 3, 4, 5 )
lt = list(t)
lt[2] = 30
t = tuple(lt)
print(t) # ( 1, 2, 30, 4, 5 )
```

# 06.04. Unpacking

The unpack operation means that each value of the tuple can be decomposed from the tuple-self. The syntaxt is very similar to multiple assignment in the case of variables, or constants:

```python
fruits = ( "apple", "banana", "cherry" )
( green, yellow, red ) = fruits
```

In the previous snippet of code, `green` variable has the value `"apple"`, `yellow` variable has the value `"banana"` and `red` value has the value `"cherry"`.

You can use the asterisk (or star) operator if you want to unpack less than the elements present into the tuple. For example, in the following snippet:

```python
fruits = ( "apple", "banana", "cherry", "orange", "kiwi" )
(apple, banana, *others) = fruits
```

`apple` contains the first element, `banana` the second element and `others` contains a list with all other elements (from `cherry` to `kiwi`):

```python
print(apple) # "apple"
print(banana) # "banana"
print(others) # [ 'cherry', 'orange', 'kiwi' ]
```

You can use the asterisk operator even in the middle. Python will automatically infer values ​​for each variable:

```python
fruits = ( "apple", "banana", "cherry", "orange", "kiwi" )
(apple, *others, kiwi) = fruits
print(apple) # "apple"
print(others) # [ 'banana', 'cherry', 'orange' ]
print(kiwi) # "kiwi"
```

# 06.05 Joining

You can use the plus operator (`+`) to join two, or more tuples:

```python
t1 = ( 1, 2, 3 )
t2 = ( "a", "b", "c" )
t3 = ( True, False )
print(t1 + t2) # ( 1, 2, 3, "a", "b", "c" )
print(t1 + t2 + t3) # ( 1, 2, 3, "a", "b", "c", True, False )
```

You can also multiply a tuple with the asterisk operator (`*`). In this case, the ultiplier must be an integer value and the expression returns a new tuple with the same elements, but repeated:

```python
t = ( 1, 2 )
print(t * 3) # ( 1, 2, 1, 2, 1, 2 )
```