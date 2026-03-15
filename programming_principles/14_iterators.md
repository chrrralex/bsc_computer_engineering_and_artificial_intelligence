# 14. Iterators

An iterator is an object that contains a countable number of values. An iterator is an object that can be iterated upon, meaning that you can traverse through all the values. Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods `__iter__()` and `__next__()`.

Lists, tuples, dictionaries, and sets are all iterable objects. They are iterable containers which you can get an iterator from. All these objects have a `iter()` method which is used to get an iterator:

```python
t = ("apple", "banana", "cherry")
it = iter(t)
print(next(it)) # "apple"
print(next(it)) # "banana"
print(next(it)) # "cherry"
```

If you try to invoke a fourth time the `next()` built-in function, you will get the following error:

```bash
ERROR! StopIteration
```

Even strings are iterable objects, and can return an iterator:

```python
s = "banana"
it = iter(s)
print(next(it)) # "b"
print(next(it)) # "a"
print(next(it)) # "n"
print(next(it)) # "a"
print(next(it)) # "n"
print(next(it)) # "a"
```

To create an object, or class as an iterator you have to implement the methods `__iter__()` and `__next__()` to your object. All classes have a function called `__init__()`, which allows you to do some initializing when the object is being created. The `__iter__()` method acts similar, you can do operations (initializing etc.), but must always return the iterator object itself. The `__next__()` method also allows you to do operations, and must return the next item in the sequence.

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myNumbers = MyNumbers()
it = iter(myNumbers)

print(next(it)) # 1
print(next(it)) # 2
print(next(it)) # 3
print(next(it)) # 4
print(next(it)) # 5
```

The example above would continue forever if you had enough `next()` statements, or if it was used in a for loop. To prevent the iteration from going on forever, we can use the `StopIteration` statement. In the `__next__()` method, we can add a terminating condition to raise an error if the iteration is done a specified number of times:

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    if self.a <= 5:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

myNumbers = MyNumbers()
it = iter(myNumbers)

for x in it:
  print(x) # 1, 2, 3, 4, 5
```

Generator comprehension expressions (often called generator expressions) in Python are a compact way to create generators. Remember that a generator produces values one at a time (lazily) instead of creating the whole list in memory. This makes them memory-efficient. The basic syntaxt is:

```python
(expression for item in iterable)
```

A simple example is the generation of squared numbers between `1` and `5`:

```python
squared_generator = ( x**2 for x in range(1, 6))
print(squared_generator) # <generator object <genexpr> at 0x7c041c50dd80>
```

To print each number, we must use the `for` loop:

```python
squared_generator = ( x**2 for x in range(1, 6))
for x in squared_generator:
  print(x) # 1, 4, 9, 16, 25
```

Each value is produced only when it is needed: the first iteration of the `for` loop gets the value `1` from the `squared_generator`; the second iteration of the `for` loop gets the value `2`; and so on.
