# 16. `try-except` statement

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
