# 05. Lists

### 05.01. Overview

A list is on ordered collection with mutable length during the program execution. A list can contain anything and each element has the own type. In Python, you can recognize a list by the presence of the square brackets (`[]`), which enclose the elements.

You can declare a list by separating the elements with the comma (`,`) and enclosing all elements with the square brackets (`[]`):

```python
aList = [ 1, 2, 3 ]
```

A list can contain duplicates:

```python
aList = [ 1, 2, 3, 4, 5, 1, 2, 3 ]
```

Moreover, a list can contain elements with different type:

```python
aList = [ True, "A string", 10, 10.5, 5.0 + 10j ]
```

An item of the list is called element. The list is ordered, changeable and duplicate values are allowed. You can access to a particular list item with the index, a number between `0` and the length of the list:

```python
aList = [ 1, 2, 3 ]
aList[1] # 2
aList[0] # 1
```

You can discover the length of a list by using the `len()` built-in function:

```python
aList = [ 1, 2, 3 ]
len(aList) # 3
```

The length of a list is the number of elements contained in a list.

### 05.02 Item Access

Consider you have this list:

```python
l = [ 1, 2, 3, 4, 5 ]
```

You can access to a list item by using an index between `0` and `len(aList) - 1`:

```python
l[1] # 2
l[3] # 4
```

Negative indexes starting from the end of the list:

```python
l[-1] # 5
l[-2] # 4
```

You can access more items in a single step by using the range of indexes, which has the `[min:max]` syntaxt:

- If `min` is not present, the default is `0` (start of the list). This index is included in the range.
- If `max` is not present, the default is `len(l) - 1` (end of the list). This index is excluded from the range.

Both are optional. Here's an example:

```python
l[1:3] # [ 2, 3 ]
l[:2] # [ 1, 2 ]
l[3:] # [ 4, 5 ]
```

You can use the negative indexes also:

```python
l[-5:-3] # [ 1, 2, 3 ]
```

If you want to check if an item is present in a list, you can use the `in` operator:

```python
10 in l # False
3 in l # True
```

Note that the `in` operator always returns a boolean value: `True` if the element is present, `False` otherwise.

### 05.03 Item Update

To modify a list item, you can use the subscript operator (`[]`) on the left part of the equal operator (`=`), in this way:

```python
l[1] = 10
```

In the previous snippet, the second element of the list became `10`. You can use the range syntaxt also:

```python
l[1:3] = [ 20, 30 ] 
```

In the previous line, we set two elements: the second element (index `1`) became `20` and the third element (index `2`) became `30`. If you specify more items, the new items will be inserted in the list at the specified position:

```python
l[1:2] = [ 10, 100, 1000, 2000 ]
```

In the previous case the elements `100`, `1000` and `2000` will be inserted after the `10` element. You can replace more elements with only one element in the following way, providing less elements than expected: 

```python
l[1:3] = [ 10 ]
```

The third element will be removed from the list.

### 05.04 Add Item

To insert an element in a list, you can use the `append()` function. This function must be specified after a dot, between the list identifier and the function name, cause the function is really a method (a method of the `list` data type). This method appends an element at the end of the list:

```python
l = [ 1, 2, 3 ]
l.append(4) # [ 1, 2, 3, 4 ]
```

Another useful method is `insert()`, that accepts two arguments:

- The first argument is the index, the position where you want to add the element.
- The second argument is the element.

All the next elements will be moved one position to the right and the length of the list will increased by `1`:

```python
l = [ 1, 2, 3 ]
l.insert(2, 10) # [ 1, 2, 10, 3 ]
l.insert(0, 0) # [ 0, 1, 2, 10, 3 ]
```

### 05.05 Remove Item

The `remove()` method accepts only one argument: the element you want to remove from the list. If there are two, or more elements, this method removes only the first occurence:

```python
l = [ 1, 2, 3, 3 ]
l.remove(1) # [ 2, 3, 3 ]
l.remove(3) # [ 2, 3 ]
```

When you use `remove()` method, if the element is present in the list, the length will decreased by `1`.

The `pop()` method also remove an element. It can be used in two way: without any argument (in this case it removes the last element of the list) and with an index (in this case it removes the specified element):

```python
l = [ 1, 2, 3 ]
l.pop() # [ 1, 2 ]
l.pop(0) # [ 2 ]
```

Python provides a powerful keyword to delete not only an element, but the entire list also: the `del` keyword. You can specifiy the element (or more) in this way:

```python
l = [ 1, 2, 3 ]
del l[0] # [ 2, 3 ]
del l
```

After the `del l` statement, you will not be able to use the list. The list no longer exists in the code.

### 05.06 Sorting

The `sort()` method change the order of the list. It sorts the list alphanumerically:

```python
l = [ "orange", "banana", "kiwi", "apple" ]
l.sort() # [ 'apple', 'banana', 'kiwi', 'orange' ]
```

By default, the `sort()` method orders the list in ascending order. If you want to order the list in descending order, you can use the `reverse` parameter and set it to `True`: it's a boolean specifies the list must be ordered in descending order.

```python
l = [ "orange", "banana", "kiwi", "apple" ]
l.sort(reverse = True) # [ 'orange', 'kiwi', 'banana', 'apple' ]
```

### 05.07 Copying

If you have two lists, `l1 = [ 1, 2, 3 ]` and `l2 = [ 'a', 'b', 'c' ]`, and you try to write the following statement:

```python
l1 = l2
```

There is a problem: both `l1` and `l2` identifiers are linked to the same list, that is `[ 'a', 'b', 'c' ]`. This means that `l1` and `l2` contain the memory address where the list is stored. In this way, any change made by using `l2` identifier is automatically visible by using the `l1` identifier (and viceversa).

If you want to copy the list linked to `l2` identifier in another portion of memory (linked to `l1`), you can use the `copy()` method:

```python
l1 = l2.copy()
l1[1] = 3.15
print(l1) # [ 'a', 3.15, 'c' ]
print(l2) # [ 'a', 'b', 'c' ]
```

The `copy()` method performs a superficial copy of the list. Another way to copy a list, is to pass the list-self as argument to the `list()` method:

```python
l1 = list(l2)
```

In this way, the `list()` method will create another instance of the same list.

A third way to made a superficial copy of the list is the range (or slice) operator:

```python
l1 = l2[:]
```

### 05.09 Joining

Concatenating two, or more list in Python is easy by using the plus operator (`+`):

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

list1 + list2 # [ "a", "b", "c", 1, 2, 3 ]

list3 = [ True, False ]
list4 = [ .0, .7, .3 ]

list1 + list2 + list3 + list4 # [ 'a', 'b', 'c', 1, 2, 3, True, False, 0.0, 0.7, 0.3 ]
```

Another way is to use the `extend()` method, that accepts a list. This method add all elements present in the accepted list to the elements present in the current list:

```python
l1 = [ 1, 2, 3 ]
l2 = [ "a", "b", "c" ]
l1.extend(l2) # [ 1, 2, 3, "a", "b", "c" ]
```
