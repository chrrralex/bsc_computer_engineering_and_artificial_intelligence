# 13. `for` statement

The `for` loop is an iteration construct allows the developer to iterate over a sequence, or an iterable element until it has at least one element. The syntaxt of the `for` loop is the following:

```python
for variable in iterable:
    statement1
    statement2
    ...
    statementN
```

The `for` statement is a loop with control (or check) in the head, it means that the execution flow is the following:

1. First, the condition there is evaluated by the Python interpreter. In this case, the condition is simple: the iterable, or sequence has at least one element.
2. If the condition is `True` (the iterable has at least one element), then all the statements inside the `while` loop are executed and the `variable` is the element extracted from the iterable.
3. If the condition is `False` (the iterable hasn't any element), no statement is executed and the program control pass to the next statements.

For example, the following snippet executes all statements inside the `for` loop for each element of the list `aList`:

```python
aList = [ "a", "b", "c" ]
for c in aList:
    print(c.upper())
```

As you can see, no counter (of flag) variable is required and the `for` loop handles perfectly and automatically the iterable. Let's analyze the previous lines:

1. First of all, the first line initzialize a list of three strings: `"a"`, `"b"` and `"c"`.
2. The second line specifies the `for` header: the `for` keyword after the expression `c in aList`. It means until `alist` has at least one element, the body of the `for` loop is executed and the `c` variable assumes the corresponding element value (in the order that they're specified: `"a"`, `"b"` and `"c"`).
3. When the iterable (`aList` in our case) hasn't other elements, then the program control passes after the `for` statement.

You can use the `break` statement (that is a keyword also) to quit permanently from the loop, as we have seen for the `while` loop:

```python
aList = [ "a", "b", "c", "d", "e", "f" ]
for c in aList:
    print(c.upper())
    if c == "b":
        break
```

`break` statement causes the loop to exit. In the our case, we've added an `if` statement inside the `for` loop to check if the variable `c` is equal to the string (with only one character) `"b"`: if the condition is `True`, then the `break` statement is executed and the program control passes to the next statements, after the `for` loop.

The `while` loops is useful to iterate over an iterable, or a sequence. In Python, examples of iterable types are lists and tuples. You can use the `for` loop with a tuple in the following way:

```python
t = ( 1, 2, 3, 4, 5 )
for element in t:
    print(element)
```

Another keyword used inside a loop body is the `continue` keyword. This keyword causes the current iteration to skip to a subsequent iteration. For example, in the following code two iteration are  skipped, when `element` is `2`, or when `element` is `4`:

```python
t = ( 1, 2, 3, 4, 5 )
for element in t:
    print(element)
    if (t == 2 or t == 4):
        continue
```

Loops can be used with the `range()` function also, a built-in function that returns a sequence of numbers between a min value `min` and a max value `max`, with a specific `step`. The type returned from the `range()` function is called `range` and it's a built-in data type of the Python programming language. We're going to see some examples, from the simplest to the hardest to understand. `range()` built-in function accepts three arguments:

```python
range(min, max, step)
```

- `min` is the minimum value (or start value) of the sequence. If it isn't specified, the default value is `0`.
- `max` is the maximum value (or end value) of the sequence. It always required.
- `step` is the step between two consecutive values. If it isn't specified, the default value is `1`.

Let's start. Use `range()` to get a range between min value and max value:

```python
for n in range(0, 4): # equivalent to range(4)
    print(n) # 0, 1, 2, 3
```

Use `range()` to get a range between min value and max value with a custom `step`:

```python
for n in range(0, 5, 2):
    print(n) # 0, 2, 4
```

Use `range()` to get a range between min value and max value with a custom and negative `step`:

```python
for n in range(10, 0, -1):
    print(n) # 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

Note that if you use `range()` with only one argument, it's interpreted as the max value. If you use `range()` with two arguments, the first is the min value and the second is the max value. Finally, if you use the `range()` with three arguments, first and second are min and max value and the third argument is the step.
