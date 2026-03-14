# 21. Modules

A module is a code library where you have one, or more exportable entitites. For "entities", in this case, we means entities of the programming language. You can see a module like a file containing a set of functions, classes and others things you want to include in your application.

Python, at runtime, creates automatically a module when it sees a file with the `.py` extensions. For example, if in you have, in your current working directory, a file called `greetings.py`, Python will see it like a module called `greetings`. In this file, you can create one, or more functions:

```python
def sayHello():
    print("Hello!")
```

You can create global variables also:

```python
GREETING_POSTFIX = "!\n"

def sayHello():
    print("Hello" + GREETING_POSTFIX)
```

In the previous example, we created a global variable called `GREETING_POSTFIX`. You can create any variable you want in a module, of any types (lists, tuples, dicts, instances and so on).

In another file, for example in you `main.py` file, you can use the `greetings` module through the `import` keyword:

```python
import greetings
```

Next of the previous line, you can access to all members specified into the `greetings` module by using a very similar syntaxt to method invocation for the objects: the name fo the module, followed by the dot symbol (`.`), followed by the name of the global variable, or the function yoiu want to use:

```python
import greetings

print(greetings.GREETING_POSTFIX) # "!\n"
greetings.sayHello() # "Hello!\n"
```

The `import` statement allows you to use an alias for a specific module, by using the `as` keyword followed by the alias of the module:

```python
import greetings as grtns
```

After the previous line of code, the `greetings` module will be available in your file with the name `grtns`: `grtns.GREETING_POSTFIX` and `grtns.sayHello()` are both valid and Python will access correctly to each memeber of the `greetings` module.

Python has a very extended system of modules, many of these are a part of the PSL (Python Standard Library). For example: `math`, `os` and `sys` are all modules you can import without installing it via pip, cause they're already installed when you download and install a Python distribution on your local machine. You can import these modules simply by using the `import` keyword:

```python
import os
import sys
import math
```

If you don't know what a module contains, you can use the `dir()` built-in function. `dir()` returns a list of all avaialable identifiers for a module passed as an argument. For example, if you don't know the `math` module, you can have an overview with `dir()` in this way:

```python
import math

dir(math) # ['__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'acos', ... ]
```

You can use `dir()` in all modules, also created by you.

You can import only a specific member of a module with a right combination of `from` keyword and `import` keyword:

```python
from greetings import sayHello

sayHello() # "Hello!\n" 
```

As you can see, in the previous example we can directly use `sayHello()`, without using `greetings.`, cause we've imported the memeber `sayHello()` with a `from` statement. You can specify more than one member:

```python
from greetings import GREETING_POSTFIX, sayHello
```

With `from`, you can also rename one, or more members exported from a module using `as`, as we've seen in the examples before:

```python
from math import sqrt as s, pow as p

print(s(4))
print(p(4, 2))
```
