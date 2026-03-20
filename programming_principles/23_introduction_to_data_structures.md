# 23. Introduction to Data Structures

Data structures are organized ways to store and manage data so that it can be accessed and modified efficiently. Choosing the right data structure affects performance, code clarity, and memory usage. In Python, the most common built-in data structures are lists, tuples, sets, and dictionaries, each designed for different use cases.

At a high level, data structures can be:

- Linear: elements are arranged in a sequence (e.g., lists, tuples).
- Non-linear: elements have hierarchical or associative relationships (e.g., trees, graphs, dictionaries).

Typical operations include:

- Accessing elements
- Inserting or removing elements
- Searching for a value
- Iterating over all elements

Different structures provide different time and space trade-offs. For example, lists are great for ordered collections, sets are optimized for membership checks, and dictionaries map keys to values for fast lookups. In the next sections, we will explore these structures and learn when to use each one.

An array stores elements of the same data type in a compact, efficient way. This is useful when you need numeric data and want predictable memory usage. The example creates an integer array, appends a value, and accesses an element by index.

```python
from array import array

numbers = array("i", [10, 20, 30])
numbers.append(40)
print(numbers[1])  # 20
```

A list is Python’s most flexible sequence type and can hold mixed data types. It supports dynamic growth and direct indexing. The example appends a new item and reads the first element.

```python
items = ["apple", "banana", "cherry"]
items.append("date")
print(items[0])  # apple
```

A queue processes elements in first-in, first-out order. `collections.deque` is efficient for adding and removing items from both ends. The example enqueues two names and dequeues the first one. Queue is a data structure based on the FIFO (First In, First Out) acronym.

```python
from collections import deque

queue = deque()
queue.append("Alice")
queue.append("Bob")
first = queue.popleft()
print(first)  # Alice
```

A stack processes elements in last-in, first-out order. A Python list can act as a stack with `append()` to push and `pop()` to remove the top. The example pushes two values and pops the most recent one. Stack is a data structure based on the LIFO (Last In, First Out) acronym.

```python
stack = []
stack.append(1)
stack.append(2)
top = stack.pop()
print(top)  # 2
```
