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
