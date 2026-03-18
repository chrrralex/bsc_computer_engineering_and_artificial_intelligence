# 16. `try-except` statement

### 16.01. Overview

Like other programming languages (for example, PHP and Java), Python includes a construct for the error handling called `try-except-finally`. We're going to see the basic form of this construct and, progressively, we'll analyze the caluses can be used with this important statement.

Normally, when an error occurs during the program execution, the Python interpreter catches the error and prints an output starting with `"ERROR! ..."` to explain the error, then it exits from the program. Thanks to the `try-except-finally` block, you can catch one, or more type of errors and you can execute a specific code to try to fix the error, or to take another specific path (such as, for example, having the user re-enter an input).

Let's start to see the basic form of the `try-excpet-finally` block. After the `try` keyword, there are the statements could causes one, or more errors. After the `catch` keyword there are one, or more statements to handle the caught error:

```python
try:
    # statements could throw one, or more errors
    print(x) # This is an error: x isn't declared
except:
    # statement used to catch one, or more errors
    print("An error occurred")
```

The following line:

```python
print(x)
```

Tries to print to the standard output the `x` variable, but this variable isn't declared in the script. So, when the Python interpreter executes this line, it will throw an error. But this line is inside a `try-except` block, so the `except` clause will catch the error and the statements to handle the error, in our case this statement:

```python
print("An error occurred")
```

will be executed. You can use more than one `except` clause to catch more than one error during the execution. For example, the following snippet prints on the standard output the message `"Variable x is not defined"` in case of a `NameError` is thrown:

```python
try:
    print(x) # This is an error: x isn't declared
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
```

### 16.02. Clauses of the `try-except-finally` statement

You can use the `else` clause. The statements inside this clause are executed only if no error was thrown:

```python
try:
    print(10) # Ok, no error here!
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
else:
    print("No error!")
```

The previous code prints `"No error!"` on the standard output, cause the `print(10)` statement doesn't throw any error (it simply prints an integer literal). The `else` clause is optional.

Another clause you can use is `finally`. This clause, if specified, will be executed regardless if the try block raises an error or not. In practice, it is executed at the end of the entire try block (if there are no errors), or possibly the except block of the captured error. But it is executed anyway.

```python
try:
    print(x) # This is an error: x isn't declared
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
else:
    print("No error!")
finally:
    print("Executed anyway")
```

The previous snippet of code prints on the standard output the following strings:

```python
Variable x is not defined
Executed anyway
```

As a Python developer you can choose to throw an errpr if a condition occurs. To throw (or raise) an error, use the `raise` keyword. Here's an example:

```python
x = -1
if x < 0:
  raise Exception("Sorry, no numbers below zero")
```

The `raise` keyword is used to raise an exception. You can define what kind of error to raise, and the text to print to the user:

```python
x = "hello"
if x != 10:
  raise TypeError("x != 10")
```

### 16.03. Exceptions and Errors

During the program execution, at runtime, two types of situations can be happen:

- Error: is a problem occurs during the program execution that cause it to faill.
- Exception: is a problem occurs during the program execution that can be resolved by repeating an action, or directly by the Python code, or in other ways, that sometimes only partially stop a functionality.

Meanwhile errors cause the program fail, exception can be successfully handled, for example with the `try-except-finally` statement we've seen in the previous paragraphs. A common example of exception is the `ZeroDivisionError`, that happens when in your Python code appears a division by `0`, like `10 / 0`.

### 16.04. Exception Hierarchy in Python

The exception hierarchy is a tree of all built-in exceptions in Python. All exceptions inherit from the base class `BaseException`, the parent of all errors and exceptions classes. Common children of the `BaseException` are:

- `Exception`: is the base class of the most common user-level errors. It has so many children, classes like `ArithmeticError` and `LookupError`.
- `GeneratorExit`: raised when a generator is closed (e.g., when `close()` is called or it is garbage collected).
- `KeyboardInterrupt`: raised when the user interrupts program execution, usually by pressing Ctrl+C, or Ctrl+Z.
- `SystemExit`: raised when the program exits, typically via `sys.exit()`.

### 16.05. Define and raise your own Exception

You can define your custom exception thanks to the OOP (Object-Oriented Programming) paradigm, that in Python allows the developer to create one, or more classes extending the `Exception` base class. For example, the following code defines a new type of exception through a class called `MyCustomError`, that extends the `Exception` base class:

```python
class MyCustomError(Exception):
    pass
```

Next, maybe in another portion of the program, or inside a function, you can raise the previous exception by using the `raise` keyword:

```python
raise MyCustomError("Something went wrong")
```

And you can catch the raised custom exception with the `try-except-finally` statement:

```python
try:
    raise MyCustomError()
except MyCustomError as error:
    print(error)
else:
    print("No error occurred")
finally:
    print("That's it!")
```

The previous code prints the following two lines of output:

```bash
Something went wrong
That's it!
```

### 16.06. Accessing the Exception data

In the previous snippet of code we've used a particular form of the `except` clause, that follows this syntaxt:

```python
except ExceptionName as identifier:
```

where:

- `ExceptionName` is the name of the exception type (`ZeroDivisionError`, or `TypeError`, or `IndexError`, or other).
- `identifier` is the object that represents the data about the raised exception.

This form of the `except` clause allows you to access the data of the exception. You can capture exception details using the `as` keyword in the `except` clause. For example:

```python
try:
    x = int("abc")
except ValueError as error:
    print(error) # invalid literal for int() with base 10: 'abc'
```

You can use `str(error)` for a human-readable string about the error. The `repr(error)` returns a detailed error. A particular attribute you can access of the `error` object in the previous example is `error.args`, a tuple containing all the argument passed to the exception:

```python
try:
    x = int("abc")
except ValueError as error:
    print(error.args) # ("invalid literal for int() with base 10: 'abc'",)
```

You can also use `error.args` with a custom exception:

```python
class MyCustomError(Exception):
    pass

try:
    raise MyCustomError("Hello!", 1, 3.15, True)
except MyCustomError as error:
    print(error.args) # ('Hello!', 1, 3.15, True)
```

Note that all arguments are passed inside the round brackets, where you raise the exception.
