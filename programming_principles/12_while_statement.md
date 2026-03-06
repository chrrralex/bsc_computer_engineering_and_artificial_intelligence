# 12. `while` statement

The `while` loop is an iteration construct allows the developer to reapeat a block until a specified condition is `True`. The syntaxt of the `while` loop is the following:

```python
while condition:
    statement1
    statement2
    ...
    statementN
```

The `while` statement is a loop with control (or check) in the head, it means that the execution flow is the following:

1. First, the condition there is evaluated by the Python interpreter.
2. If the condition is `True`, then all the statements inside the `while` loop are executed.
3. If the condition is `False`, no statement is executed and the program control pass to the next statements.

For example, the following snippet of code prints `10` as an output:

```python
i = 0
while i < 10:
    i += 1
print(i) # 10
```

Let's analyze the previous lines:

1. First of all, the first line initzialize the `i` variable with the value `0`.
2. The second line specifies a condition: `i < 10`. It means until `i` is greather or equal to `10`, the body of the `while` loop is executed.
3. In this case, we've only one statement in the loop body: `i += 1`. This is called a step statement, cause it increments the value if the `i` variable by `1`.
4. When the `i` reaches the value `10`, the condition specified after the `while` keyword is `False`, so the loop body doesn't executed.
5. The last line prints to the standard output the `i` variable: `10`.

You can use the `break` statement (that is a keyword also) to quit permanently from the loop:

```python
counter = 10
while counter > 0:
    counter -= 1
    if counter == 5:
        break
print(counter) # 5
```

`break` statement causes the loop to exit. In the our case, we've added an `if` statement inside the `while` loop to check if the variable `counter` is equal to `5`: if the condition is `True`, then the `break` statement is executed and the program control pass to the next statements, after the `while`.

The `while` loops is useful in two cases:

- If you want to execute one, or more statements until the loop condition is `True`.
- If you want to execute one, or more statements a specific number of times.

In the first case, you can use a flag variable (or simply flag), a boolean value used in the `while` condition. In the second case, you can use a counter variable (or simply a counter), a numeric variable that is incremented, or decremented by a certain step.

Here's an example of a `while` loop with flag variable:

```python
flagVariable = bool(input("Insert a boolean value: "))
while flagVariable:
    print("You've inserted 'True'!")
    flagVariable = bool(input("Insert a boolean value: "))
```

Here's an example of a `while` loop with counter variable:

```python
aList = [ 1, 2, 3, 4, 5 ]
index = 0
while index < len(aList):
    print(aList[index])
    index += 1
```

We've used the previous `while` loop to iterate over the list `aList`, that has five elements. The `index` is a counter, a variable starting from `0` and reaching a max value of `len(aList)`, that is `5`. But when the `index` is `5`, the condition of the `while` loop is false, so Python exits from the loop.
