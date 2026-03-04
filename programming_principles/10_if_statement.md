# 10. `if` statement

The `if` statement is a selection statement that allows the developer to specify a boolean condition (like `a == b`, or `a >= 10`) and, in based of the returned value, the Python interpreter executes one, or more statement. A boolean condition, as we've seen in the previous chapters, is an expression that can be evaluated as `True`, or `False`.

```python
a = 10
if a > 10:
    print("a > 10")
```

Differently from other programming languages, boolean conditions in the `if` statement aren't surrounded by the round brackets, but immediately after the expression there is the colon (`:`). In Python is really important the indentation (three, or four spaces): thanks to indentation the Python interpreter recognizes the blocks of code. The previous snippet of code shows an `if` statement (a block) with only one statement: `print("a > 10")`. If the condition is `True`, then the statements inside the `if` block will be executed. If the condition is `False`, the Python interpreter executes the next statements, ignoring the statements inside the `if`. 

Note that Python doesn't use the semicolon character (`;`), like other languages, to end a statement. The new line character (`\n`) is the end of a statement in many cases, but not in all cases.

You can use the `else` keyword to complete the `if` statement (sometimes called `if...else` statement):

```python
a = 10
if a >= 20:
    print("a >= 20")
else:
    print("a < 20")
```

The previous snippet prints `"a < 20"`, cause the `a` variable has a valure lower than the integer literal `20` specified directly in the boolean condition of the `if` statement. `if` clause and `else` clause are mutually exclusive: only one between the first statement, or the second can be executed. If the condition is `True`, the statements of the `if` clause are executed; if the condition is `False`, the statements of the `else` clause are executed.

There is a third important clause you can use with the `if` statement: the `elif` clause. You can specify as many clauses as you want, in based of the problem you're trying to resolve:

```python
a = 87
if a <= 30:
    print("Level 1")
elif a <= 60:
    print("Level 2")
elif a <= 90:
    print("Level 3")
else:
    print("Level 4")
```

In the previous code, the third `elif` clause is executed, because the value of the `a` variable is lower than `90` (`a <= 90`), it's `87`. This statement is also called `if...elif...else` statement, but remember that the `else` clause is always optional.

Python provides you a very elegant syntaxt called shorthand `if`: you can specifiy the entire `if` statement ina single line of code. The syntaxt is the following:

```python
stmtIfTrue if condition else stmtIfFalse
```

If `condition` is `True`, only `stmtIfTrue` is executed; if it's `False`, only `stmtIfFalse` is executed. Here's an example:

```python
a = 300
b = 150
print("a >= b") if a > b else print("b >= a")
```

You can use the shorthand `if` syntaxt to assign a value to a variable, like in this way:

```python
a = 10
b = 20
bigger = a if a > b else b
print("Bigger is", bigger)
```