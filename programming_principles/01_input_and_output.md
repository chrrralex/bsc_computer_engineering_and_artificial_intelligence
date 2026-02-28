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