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
<!-- to do -->

### 17.07. Keyword Parameters
<!-- to do -->

### 17.08. Default Parameters
<!-- to do -->

### 17.09. Mixing Keyword and Positional Parameters
<!-- to do -->

### 17.10. Positional-Only and Keyword-Only Arguments
<!-- to do -->

### 17.11. Mixing Positional-Only and Keyword-Only Arguments
<!-- to do -->

### 17.12. Arbitrary Positional Arguments with `*args`
<!-- to do -->

### 17.13. Arbitrary Keyword Arguments with `**kwargs`
<!-- to do -->

### 17.14. Using both `*args` and `**kwargs`
<!-- to do -->

### 17.15. Function Metadata
<!-- to do -->

### 17.16. Decorators
<!-- to do -->

### 17.17. Lambda Functions
<!-- to do -->

### 17.18. Recursive Functions
<!-- to do -->

### 17.19. Generator Functions and the `yeld` Keyword
<!-- to do -->

### 17.20. Global and Local Variables
<!-- to do -->

### 17.21. Variable Shadowing and the `global` Keyword
<!-- to do -->
