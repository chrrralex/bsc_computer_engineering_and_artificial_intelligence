# 01. Input and Output

You can print variable and function by using the `print()` function:

```python
print(a) # 10
print(DAYS_OF_WEEK) # 7
```

The `print()` function accepts, many other parameters:

- `sep`: is the separator of each argument passed to the function.
- `end`: is a string that terminates the print.
- `flush`: a boolean value (`True`, or `False`) specifies if the output is flushed.

`print()` is a part of the PSL (Python Standard Library). Here's an example:

```python
a, b, c = 100, 10, 1
print(a, b, c, sep=" - ", end=" - This is the end", flush = True) # 100 - 10 - 1 - This is the end
```

As you can see in the previous script, the `print()` function accepts a variable number of arguments (variables, constants, or both).

For prompting, you can use the `input()` function. It accepts a prompt string and returns the value inserted by the user via the standard input (basically the keyword):

```python
firstName = input("First name: ")
lastName = input("Last name: ")
```

Meanwhile the `print()` function prints to the standard output, the `input()` function accepts from the standard input. Tipically the standard input is the keyboard (but it can be a file, or a network connection). Standard output refers to console, or monitor (but it can be a file, or other).

Comments can be used to explain Python code. A comment can be used to make the code more readable. Comments can be used to prevent execution when testing code. In Python, any comments is introduced by the `#` character and are completely ignored by the interpreter.

You can use a single-line comment like this:

```python
# This is a comment
print("Hello, World!")
```

or you can specify a comment immediately after a line of code:

```python
print("Hello, World!") # This is a comment
```

A comment doesn't have to be text that explains the code, it can also be used to prevent Python from executing code. Here's an example:

```python
# print("Hello, World!")
print("Cheers, Mate!"
```

In Python, when you write code, you can make two types of mistakes:

- Logic error: when the code syntaxt is correct, but there is something wrong about the implemented functionality. For example, if you write the code that prompts two numbers to the user to make a division, if the user insert `0` as second number, it will occur a runtime error (division by zero). Logic errors are more difficult to recognize and, sometimes, to fix. These errors may cause the end of the program (for example, a division by zero, if it isn't handled correctly).
- Syntaxt error: when the code syntaxt is wrong and the Python interpreter returns the specific violated rule. Syntaxt errors are easy to recognize and to fix. This errors prevent the program execution.

Both errors are possibile, even if you're a professional developer.

An example of syntaxt error is when you forgive a round bracket at the end of the `print()` function:

```python
print("Hello, World!" # ERROR! SyntaxError: '(' was never closed
```

Here's an example of logic error:

```python
print(10 / 0) # ERROR! ZeroDivisionError: division by zero
```

The good news is that errors are fisiological to learn a programming language! Keep practicing and learning from mistakes!