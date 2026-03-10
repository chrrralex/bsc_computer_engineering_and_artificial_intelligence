# 17. Functions

### 17.01. What is a Function?

A function is a block of code you can isolate and execute wherever you want in the program. A function is also called procedure, routine, or subroutine. In general:

- A function is a group of statements that executes a task and returns a value.
- A procedure is a group of statements that executes a task without returning any value.

In Python we'll use the term function for both functions and procedures. You can see a function as a black-box:

- It accepts zero, one, or more inputs called parameters (or formal parameters).
- It executes a task by one, or more statements. A function is block of code.
- It can return an output, or terminates his execution without returning any value.

For example, in Python you can define a function with the `def` keyword:

```python
def sum(a, b):
    return a + b
```

The `sum()` function accepts two inputs, called parameters (or formal parameters): `a` and `b`. The `sum()` function has only one statement:

```python
return a + b
```

The expression `a + b` is a sum between the two formal parameters and the `return` keyword returns an output from the execution of the `sum()` function: the sum between `a` and `b`.

You can invoke, or call, the `sum()` function by passing (with the correct order, and type) the arguments (also called actual parameters) to the function in this way:

```python
print(sum(10, 20)) # 30
```

### 17.02. Stack and Activation Record

The stack is a portion of the memory allocated for the program used to store information about the called function during the execution. Stack is a data structures based on a list and it has the following properties:

- It has a finite size. The length of a stack is the number of elements (or records) stored in it.
- Insert operation is tipically called "push" and it consists of adding an element to the top of the stack (last element).
- Remove operation is tipically called "pop" and it consists of removing an element to the top of the stack (last element).
- A stack is a LIFO data structure: LIFO is the acronym of "Last In, First Out". The last element you add to the stack is the first element you cam remove from it.

All informations about a function invocation takes the name of AR (Activation Record), or SF (Stack Frame). An AR includes the following data:

- Arguments (or actual parameters) passed to the function at the function call.
- Local variables, which are variables defined directly into the function.
- A reserved memory for the return value.
- The returning address from the function. This is the address where is located the statement immediately after the function call, in the program.
- Dynamic link: this is a link to the previous AR.
- Other informations about the stack.

If you have three function, `func1()`, `func2()` and `func3()` defined as you can see here:

```python
def func1():
    print("Hello!")

def func2(a):
    print(a + 10)

def func3(a, b):
    return a * b
```

and if you invoke the previous functions in this way:

```python
func1()
func2(10)
func3(10, 5)
```

the following happens:

1. At the first line, the function call of `func1()` adds an AR to the stack. It doesn't return any value and it doesn't accept any argument.
2. `func1()` is executed, the AR is removed from the stack, then control returns to the main program that invoked it.
3. At the second line, the function call of `func2()` adds an AR to the stack. It doesn't return any value, but it accepts one argument.
4. `func2()` is executed, the AR is removed from the stack, then control returns to the main program that invoked it.
5. At the third line, the function call of `func3()` adds an AR to the stack. It returns a value (the sum between the two parameters), but it accepts one argument.
6. `func3()` is executed, the AR is removed from the stack, then control returns to the main program that invoked it.

Note that, at each moment, the stack has 0, or 1 AR. At any moment, only one AR is "active". But, what happens to the stack if we have the following code?

```python
def func3(a, b):
    return a * b

def func2(a):
    return func3(a, 10)

def func1():
    func2(10)

func1()
```

1. `func1()` is called.
2. An AR for `func1()` is added to the stack.
3. `func1()` starts his execution, but it calls the `func2()` function. At this moment, we've only one AR: the one for `func1()`.
4. `func2()` is called.
5. An AR for `func2()` is added to the stack. At this moment, we've two AR: one for `func1()` and another for `func2()`. Only the `func2()` AR is active.
6. `func2()` starts his execution, but it calls the `func3()` function.
7. `func3()` is called.
8. An AR for `func3()` is added to the stack. At this moment, we've three AR: one for `func1()`, another for `func2()` and a third for `func3()`. Only the `func3()` AR is active.
9. `func3()` finishes his execution, then returns a value. The AR of `func3()` is removed.
10. `func2()` resumes its execution.
11. `func2()` finishes his execution, then returns a value. The AR of `func2()` is removed.
12. `func1()` resumes its execution.
13. `func1()` finishes his execution, it doesn't return any value. The AR of `func1()` is removed.

In practice the stack becomes longer or shorter depending on the number of functions invoked.

### 17.03. Function Signature

In Python, a function signature describes how a function is defined, specifically. The function signature is composed by:

- Function identifier (the name of the function).
- The parameters it accepts (not only their identifiers, but the order, eventually their default values and their types also).
- The return type.

All these information describes how the function should be called. For example, if we have a function like this:

```python
def f():
    print("Hello!")
```

Its signature is `f()`. If we've another function like this:

```python
def f(a, b):
    print(a + b)
```

Its signature is `f(a, b)`. An other example with a default value (we'll cover the default values later):

```python
def greet(name, message = "Hello!"):
    print(message, name)
```

the signature is `greet(name, message = "Hello!")`.

If you don't respect the function signature, you could get an error. The most common error you can see if you try to call a function with an incorrect list of arguments is the `TypeError`. Python interpreter throws a `TypeError` if you try to invoke a function with:

- wrong number of arguments;
- you use a non-existing keyword (or name) for a named argument;
- you pass one, or more arguments with incorrect type.

You should pay attention to how you invoke a function based on its signature.

### 17.04. Function definition

A function definition consists in two parts:

- The keyword `def` followed by the function signature (the function identifier and its parameters).
- The body of the function, that is the statements located into the function block.

For example, we can define a function called `sum()` in this way:

```python
def sum(a, b):
    result = a + b
    return result
```

`sum` is the identifier. `a, b`, into the round brackets, is the list of the parameters (also called formal parameters). It means that the `sum()` function accepts two parameters and into it `a` refers the first parameter and `b` refers the second parameter. After the colon (`:`), we have the function body, composed by two statements:

```python
result = a + b
return result
```

As we'll see later, `result` is a local variable of the function, a variable that exists only into the function (it isn't visible to other function, or in the main program).

### 17.05. Function invocation

You can invoke a function specifying its name, followed by the round brackets and passing zero, one, or more parameters. You should pay attention to respect the function signature (number, types and order of the formal parameters specified in the function declaration). For example, if you want to call the `sum()` function defined in the previous paragraph, you can write something like this:

```python
sum(10, 5) # 15
```

The following calls are all wrongs:

```python
sum() # few arguments
sum(5) # few arguments
sum(10, 15, 20) # too many arguments
sum(10, "15") # logical error: + cannot handle different types (like an integer and a string)
```

Remember: you should pay attention to how a function should be called in terms of parameters, their order, their types, their default values and their names. In the following paragraph we'll see many other properties of the functions in Python.

### 17.06. Positional Parameters

Normally, when you define a function and declare the parameters list, Python uses the positional parameters. Positional parameters means that the parameters list has an order and each parameter in that list defines how the function can be called. For example, if you have a function called `max()` defined in the following code:

```python
def max(a, b, c):
    m = a
    if b > m:
        m = b
    if c > m:
        m = c
    return m
```

you can invoke the function in this way:

```python
print(max(10, 20, 30)) # 30
```

The binding of the positional parameters exploits the order of the parameters. In our case:

- the integer literal `10` is binded to the formal parameter `a`;
- the integer literal `20` is binded to the formal parameter `b`;
- and the integer literal `30` is binded to the formal parameter `c`.

`m`, in the previous function, is a local variable, only visible ed usable into the `max()` function.

The positional parameters has a greather impact when the parameters have different types, like in this case:

```python
def func(a, b):
    print("Str is: " + b, a)

func(10, "Hello!") # Str is: Hello! 10
```

In the previous function, the integer literal `10` is binded with the `a` formal parameter, meanwhile the string literal `"Hello!"` is binded with the `b` formal parameter. What happens if we exchange the two literals?

```python
func("Hello!", 10) # ERROR! TypeError: can only concatenate str (not "int") to str
```

Python, during execution, will throw a `TypeError`, cause the Python interpreter cannot convert automatically an integer literal (in our case, `10`) in a string. For this reason it's very important to respect the order and type expected for each parameter specified in the function parameter list.

### 17.07. Keyword Parameters

A convenient alternative to the positional parameters are the named parameters (also called keyword parameter). Positional and named parameters are very similar when you define a function: both are a list of identifiers, separated by the comma (`,`). But the difference is in how the function is called:

```python
def greet(firstName, lastName):
    print("Hello, " + firstName + " " + lastName + "!")

# calling greet() by using positional parameters
greet("Christian", "Atzeni") # "Hello, Christian Atzeni!"

# calling greet() by using named parameters
greet(firstName = "Christian", lastName = "Atzeni") # "Hello, Christian Atzeni!"
```

The syntaxt to follow when you call a function by using the named parameters is `key = value`, where `key` is the identifier specified in the parameters list (in the function declaration), meanwhile the `value` is a literal, or a variable. When you use the named parameter, all expected parameter are required. But you can call a function specifying a different order. For example, both the following calls are valid:

```python
greet(firstName = "Christian", lastName = "Atzeni")
greet(lastName = "Atzeni", firstName = "Christian")
```

But you pay attention to how you pass value for a specific parameter. A simple example, the following code produces a `TypeError`:

```python
greet("Atzeni", firstName = "Christian") # ERROR! TypeError: greet() got multiple values for argument 'firstName'
```

The first argument we've passed, the string literal `"Atzeni"`, is binded to the first formal parameters `firstName`. But immediately after we use the named parameter for `firstName`: this cause a multiple-value assignment to the `firstName` parameter, among other things, leaving the lastName parameter empty.

Python docs refers to the named parameters with the term kwargs (contraction of  keyword arguments).

### 17.08. Default Parameters

You can set a default value for one, or more parameters. Dwefault parameters are also called optional parameters, cause when you try to call the function you can pass, or not these parameters. For example, this is the `sum()` function we've already shown previous, but with default parameters:

```python
def sum(a = 0, b = 0):
    return a + b
```

You can call `sum()` in one of the following ways:

```python
sum() # a = 0, b = 0
sum(10) # a = 10, b = 0
sum(10, 20) # a = 10, b = 20
sum(a = 10, b = 20) # a = 10, b = 20
sum(b = 20) # a = 0, b = 20
```

If you don't pass any value, the default parameter assumes the default value automatically.

### 17.09. Mixing Keyword and Positional Parameters

You can use both positional and named parameters. You can use their with default parameters also. Here's an example:

```python
def sum(a = 0, b = 0):
    return a + b

sum() # using default parameters for both a and b
sum(10) # using positional parameter for a, default parameter for b
sum(10, 20) # using positional parameters for both a and b
sum(a = 10, b = 20) # using named parameters for both a and b
sum(b = 20) # using named parameter for b and default parameter for a
sum(b = 20, a = 10) # using named parameter for both a and b, but in different order
```

If your intention is to allow positional-only parameters, you can use the slash operator (`/`). This operator must be used at the end of the parameters list. Positional-only parameters must be passed by position, not by keyword. Here's an example:

```python
def func(a, b, c, /):
    print(a, b, c)

func(10, 20, 30) # correct
func(a = 10, 20, 30) # incorrect: you cannot use named parameters in a positional-only parameters function
```

If your intention is to allow keyword-only parameters, you can use the star operator (`*`). This operator must be used at the start of the parameters list. Keyword-only parameters must be passed by name, not by position. Here's an example:

```python
def func(*, a, b, c):
    print(a, b, c)

func(10, c = 20, b = 30) # incorrect: you cannot use positional parameters in a keyword-only parameters function
func(a = 10, b = 20, c = 30) # correct
```

Finally, you can mix positional-only and named-only parameters. The rules are two:

- Immediately after the positional-only parameters must be present the slash operator (`/`).
- Immediately before the keyword-only parameters must be present the star operator (`*`).

The following version of the `sum()` function has six parameters:

```python
def sum(a, b, c, /, *, d, e, f):
    return a + b + c + d + e + f
```

The first three parameters are positional-only parameters, meanwhile the last three parameters are keyword-only parameters. It means when you invoke `sum()`:

- `a`, `b` and `c` must be used as positional-only parameters;
- `d`, `e` and `f` must be used as keyword-only parameters.

You can invoke the `sum()` function in this way:

```python
sum(10, 20, 30, f = 60, d = 40, e = 50)
```

If you try to use keyword-only parameters for the first three parameters, Python will throw an error similar to `SyntaxError: positional argument follows keyword argument`. If you try to use positional-only parameters for the last three parameters, Python will throw an error similar to `TypeError: sum() takes 3 positional arguments but 6 were given`.

### 17.10. Arbitrary Positional and Keyword Arguments with `*args` and `**kwargs`

In most common programming language there isn't any functionality about var args (contraction of variable arguments). Variable arguments means you can pass zero, one, or more arguments to the function and it can handle it without any problem. This functionality is also called arbitrary positional arguments. In Python, to create a function with arbitrary positional arguments you can use `*args` in this way:

```python
def printNumbers(*args):
    for n in args:
        print(n)

printNumbers()
printNumbers(10) # 10
printNumbers(10, 20) # 10, 20
printNumbers(10, 20, 30) # 10, 20, 30
printNumbers(10, 20, 30, 40, 50, 60, 70) # 10, 20, 30, 40, 50, 60, 70
```

To create a function that accepts an arbitrary positional arguments, you must use the star operator as prefix with the identifier you can use inside the function to refer the arguments list. In the previous snippet, we've used `args` as identifier, but it can be different. For example, the previous function can be modified in this way:

```python
def printNumbers(*numbers):
    for n in numbers:
        print(n)
```

You can invoke the function with zero, one, or more parameters:

```python
printNumbers()
printNumbers(10) # 10
printNumbers(10, 20) # 10, 20
printNumbers(10, 20, 30) # 10, 20, 30
printNumbers(10, 20, 30, 40, 50, 60, 70) # 10, 20, 30, 40, 50, 60, 70
```

`*numbers` is a tuple containing all actual parameters passed to the function at the invocation.

If you want to exploit the arbitrary keyword arguments (also called arbitrary named parameters), the prefix for the identifier specified into the round brackets is a double-star operator (`**`). For example, you can define a function with `**kwargs` parameter in this way:

```python
def printNumbers(**kwargs):
    for k, n in kwargs.items():
        print(k + ": " + str(n))
```

Now, `printNumbers()` accepts arbitrary keyword arguments, it means you can pass zero, one, or more named parameters by exploiting the syntaxt `key = value`. Each pair is separated from the next with the comma (`,`). You can call the `printNumbers()` function in one of the following way:

```python
printNumbers()
printNumbers(a = 10) # a: 10
printNumbers(a = 10, b = 20) # a: 10, b: 20
printNumbers(a = 10, b = 20, c = 30) # a: 10, b: 20, c: 30
```

`**kewargs` is a dict where the keys are the identifiers of the named parameters, meanwhile the values are the value of the named parameters.

Can you mix `*args` with `**kwargs`? Absolutely yes! You can use both `*args` and `**kwargs` in the same parameters list, but there are some rules you need to follow:

- First, you must specify the regular parameters (positional, or named).
- Second, you can specify the `*args` identifier for arbitrary positional parameters.
- Third, you can specify the `**kwargs` identifier for arbitrary keyword parameters.

Here's an example:

```python
def func(p1, p2, p3, *args, **kwargs):
    pass
```

You can invoke `func()` in so many ways:

```python
func(10, 20, 30) # only expected positional arguments
func(10, 20, 30, "a", "b", "c") # expected positional arguments with *args: "a", "b" and "c" are part of the *args parameter
func(10, 20, 30, "a", "b", "c", a = 10.5, b = 20.5) # expected positional arguments with *args and **kwargs: "a", "b" and "c" are part of the *args parameter, meanwhile a = 10.5 and b = 20.5 are part of the **kwargs parameter
```

There is another syntaxt called arguments unpacking you can use in Python. If you have a list like this:

```python
l = [ 1, 2, 3 ]
```

and a function defined like this:

```python
def func(a, b, c):
    pass
```

You can use the star operator before the `l` identifier of the list to unpack all elements of the list (`1`, `2` and `3`) to bind automatically `a` parameter with the first element of `l` (`1`), `b` parameter with second element of `l` (`2`) and `c` parameter with third element of `l` (`3`).

```python
func(*l)
```

The length of the list must be the same of the length of the parameters list (in our case, the length must be `3`). If you try to use a list with more elements, Python will throw an error:

```python
l = [ 1, 2, 3, 4 ] # l has 4 elements
func(*l) # ERROR! TypeError: func() takes 3 positional arguments but 4 were given
```

The same principle you can use with named parameters by using the double-star operator (`**`). If you have a function defined like this:

```python
def func(a, b, c):
    pass
```

and a dict defined like this:

```python
d = { "a": 1, "b": 2, "c": 3 }
```

you can use `**` before the identifier of the dict, `d`, to unpack the key-value pairs: each key of the dict must be equal to the identifier of the paramter and each value of the dict is the value of each parameter.

```python
func(**d)
```

### 17.11. Function Metadata

Function metadata is information about a function, not the function’s execution itself. Python automatically stores several attributes about every function. Remember that every things, in Python, is an object; Python is an OOP (Object-Oriented Programming) programming language, as we'll see in the next chapter. Most important attributes about a function are:

- `__name__`: function name;
- `__doc__`: documentation (docstring);
- `__module__`: module where it was defined;
- `__defaults__`: default arguments;
- `__annotations__`: annotations (type hints).

For example, if we have the following function:

```python
def greet(name: str = "Guest") -> str:
    """Return a greeting message."""
    return f"Hello, {name}!"
```

we can access its function metadata with these lines of code:

```python
print(greet.__name__) # greet
print(greet.__doc__) # Return a greeting message.
print(greet.__module__) # __main__
print(greet.__defaults__) # ( 'Guest', )
print(greet.__annotations__) # { 'name': <class 'str'>, 'return': <class 'str'> }
```

Note that `greet.__defaults__` is a tuple and `greet.__annotations__` is a dict.

### 17.12. Lambda Functions

A lambda function in Python is a small anonymous function. An anonymous function is a function without a name, specified inline of the code. It is usually used for short, simple operations that you don't want to define with a full def function.

To create a simple lamba function you must follow this syntaxt:

```python
lambda arguments: expression
```

where:

- `lambda` is the Python keyword for the lambda function;
- `arguments` is the parameters list (identifiers separated by the comma `,`, without any round brackets);
- `expression` is a valid Python expression, or statement that returns a value from the lambda function.

To understend in a better way the lambda function, cosider the following `add()` function defined normally:

```python
def add(a, b):
    return a + b
```

We can easily convert the previous function in a lambda function in this way:

```python
add = lambda a, b: a + b
```

A lambda function can be assigned to a variable, in our case the variable called `add`. You can invoke the lambda function like a normal function:

```python
print(add(10, 20)) # 30
```

A lambda function with one parameter is more shorter:

```python
square = lambda x: x**2
print(square(3)) # 9
print(square(10)) # 100
```

If you surround the lambda function with the round brackets, you can invoke it directly inline, by passing all the expected arguments inside the round brackets. Something like this:

```python
print((lambda a, b: a + b)(10, 20))
```

A lambda function used in this way can also used in any other expression where the return value of the lambda function is the expected in the expression.

Lambda functions have some limitations:

- a lambda function cannot have more than one statement;
- a lambda function cannot include loops (like `while`, or `for`), or assignments;
- a lambda function is designed to be ready-to-read: if it's too long, the code may results difficult to read.

### 17.13. Recursive Functions
<!-- to do -->

### 17.14. Generator Functions and the `yeld` Keyword: a short introduction

Generators are functions that can pause and resume their execution. When a generator function is called, it returns a generator object, which is an iterator. The code inside the function is not executed yet, it is only compiled. The function only executes when you iterate over the generator. Generators use the `yeld` keyword to return a value at a specific execution, not the `return` keyword.

Here's an example:

```python
def generator():
  yield 1
  yield 2
  yield 3

for value in generator():
  print(value) # 1, 2, 3
```

Let's analyze what happens with the previous code:

1. The first time the `generator()` function is called, it returns `1` (`yeld 1`).
2. The second time the `generator()` function is called, it returns `2` (`yeld 2`).
3. The second time the `generator()` function is called, it returns `3` (`yeld 3`).
4. At this point, `generetor()` function finished their values, so the `for` loop ends.

The `yield` keyword is what makes a function a generator in Python. When yield is encountered, the function's state is saved, and the value is returned. The next time the generator is called, it continues from where it left off.

This was just a simple introduction to generators. For more information, consult the official Python documentation directly, which is certainly much more exhaustive.

### 17.15. Global and Local Variables

A global variable is a variable defined outside any function, tipically at the start of the file. A global variable has a scope extended to the entire program, from the line where it's defined to the end. For example, the variable `x` defined in the following snippet is a global variable, cause it's visible and usable by all defined functions:

```python
x = 10

def f1():
    print(x)

f1() # 10 - global x is visible into f1()

def f2():
    print(x)

x = 5

f2() # 5 - global x, after it is changed, is visible into f2()
```

You can define a variable with the same identifier in a function: in this case, the global variable is shadowed by the local variable. A local variable (defined into a function) has a scope extended only to the function where it's defined, from the line of its delcaration to the end of the function. Here's another example:

```python
x = 10

def f1():
    x = 50
    print(x)

f1() # 50 - local x of f1() shadows global x, so 50 is printed to the standard output

print(x) # 10

def f2():
    x = 100
    print(x) # 100

f2() # 100 - local x of f2() shadows global x, so 100 is printed to the standard output

x = 20

print(x) # 20
```

In the first line we define a variable called `x`, a global variable. Into the `f1()` function another variable called `x` is defined: this is a local variable and it hasn't nothing to do with the global `x` variable. So, when we call `f1()`, the `50` value is printed to the standard output. Same topic about the `f2()` function: a local `x` variable is defined and its value is `100`, so when we call `f2()`, `100` is printed to the standard output. The last line overwrite the global `x` variable value with `20`, and the last `print()` prints to the standard output the `20` value.

To summarize:

- A global variable is a variable visible from the line it's defined to the end of the file. It has a global scope.
- A local variable is a variable visible from the line it's defined to the end of the function, or the block. It has a local scope.

Another examples of local variable are the variables defined in the header of a `for` loop:

```python
for i in range(5):
    print(i)
```

The `i` variable is visible only into the `for` block.

Python has a keyword to allow the developer to refer to a global variable instead of a local variable. The keyword is `global` and you can use it before the identifier of the global variable. This is an example:

```python
x = 100

print(x) # 100

def f1():
    global x
    x = 200

f1()

print(x) # 200
```

We've defined the `x` global variable with the value `100` at the first line. Into the `f1()` function, we have used `global` keyword, so into the `f1()` function any ref with the `x` identifier is, really, the global variable `x`, defined at the first line. In the next line of code, we changed the variable of the `x` variable with the value `200`, and after we call `f1()`. The last line of code prints `200` (the new value of the global `x` variable, modified by the `f1()` function).
