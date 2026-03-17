# 21. Modules

### 21.01. Overview

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

### 21.02. Public and private members

In a module, you may have some functions, or variables you can use only in the module itself. To make a function of a module a private function, or to make a variable of a module a private variable, you can use the underscor character (`_`) as prefix of each private variable, or function. For example, if you have a module in a file called `examples.py` like this:

```python
a = 10 # this is a public variable

_b = # this is a private variable

def f(): # this is a public function
    pass

def _g(): # this is a private function
    pass
```

you can use the `from examples import *` statement and try to use each member of the imported module in another file, for example in a file called `main.py`:

```python
from examples import *

print(a) # it's ok, cause a is a public variable
print(_b) # it's an error, cause _b is a private variable: ERROR! NameError: name '_b' is not defined

f() # it's ok, cause f() is a public function
_g() # it's an error, cause _b is a private function: ERROR! NameError: name '_g' is not defined
```

Private members have an effect only if the module is imported by `from examples import *` statement. If you import `_b` and `_g()` explicitly, they're available in your code:

```python
from examples import _b, _g

print(_b) # no problem, cause _b is imported explicitly
_g() # no problem, cause _g() is imported explicitly
```

### 21.03. Where modules are located in Python

But in which way Python be able to find and load one, or more modules in your current program? `sys.path` (from the `sys` module, you can import in your program with the `import sys` statement) is a list of directories Python searches when importing modules. You can print its content in the following way:

```python
import sys
print(sys.path)
```

If you want a custom directory (maybe where you store your one, or more modules), you can directly modify the `sys.path` variable. For example, if in your current working directory there is a folder called `modules/`, you can add this folder to the `sys.path` variable in this way:

```python
import sys
sys.path.append("./modules/")
```

By default, the `sys.path` variable contains the string `""`: it means all modules created in your current working directory (assuming it's the root directoy of the project) are visible in your module. This is the default in Python.

`PYTHONPATH` is a system environment variable that adds directories to Python's module search path. These directories are automatically added to `sys.path` when Python starts. Another way to include your custom modules stored in one, or more custom directories is to change the `PYTHONPATH` variable in one of these way:

```bash
export PYTHONPATH=/modules # in Linux, or OS X
set PYTHONPATH=C:\modules # in Windows
```

A third way to whitelist your custom modules is through the `.pth` files. `.pth` files are configuration files used to add directories to Python's module search path. They are typically located in site-packages directories. A `.pth` file may have the following content:

```python
/modules
```

When Python starts, it reads .pth files and adds those paths to `sys.path`.

`sys.prefix` indicates the root directory of the Python installation or virtual environment. You can print the content of `sys.prefix` in this way:

```python
import sys
print(sys.prefix)
```

### 21.04. Scopes and Namespaces

A scope of a variable, or a function is the region of a program where a variable is accessible (visible and usable). Python has four main scopes:

- Local scope: extended from the line where the variable is declared to the end of the block. For example, a variable defined inside the function, or its arguments have a local scope (they're visible and usable until the end of the function). Often, the local scope is also called the function scope, or the block scope. Also the variables declared in the `for` loop have a local scope, limited to the `for` loop self.
- Global scope: extended from the line where the variable is delcared to the end of the file. Remember that, in Python, a file is a module also. Often, the global scope is also called module scope. If you define a global variable at the top of the file, immediately after the `import` statements, the variable is visible and usable in all the module, from start to the end of the file. It means one, or more functions can access and modify the global variables.
- Built-in scope: Python has a very extended standard library and so many functions and utilities are avaialble in your module. The built-in module is composed by all functions, constants and others entitites you can access directly in a Python CLI. Functions like `len()`, `min()`, `max()`, `dir()` and so on are all parts of the built-in scope. The elements you can access in the built-in scope depends on the Python installation: it's different from Python 2 to Python 3 (we've always used Python 3 and it's strongly recommended to use).

Here's an example:

```python
x = 10 # this is a global variable (module scope)

def f(z): # arguments are all local variable of the function (function scope)
    y = 100 # this is a local variable of the function (function scope)
    return y + z

for i in range(3): # range() is a built-in function (built-in scope), always callable 
    print(i) # i is a local variable of the for loop (block scope)
```

You can create a nested function in Python, where you can define other variables. Often, this scope is known as enclosing scope, that indicates the variables defined inside the nested function are visible and usable only in the nested function. Here's an example:

```python
def f():
    x = 10 # local variable of f
    def nested_f():
        y = 20 # local variable of y
        return y
    return nested_f() + x

print(f()) # 30
```

In the previous example we have declared two variables in the code: `x` has a function scope, extended to `f()` only; `y` has a nested function scope, extended to `nested_f()` only.

You can see the previous scopes as namespaces. A namespace is a logical container where all variable indetifiers and function identifiers (but classes and other language entities) are visible. Just like scopes, Python introduces at least 3 different levels of namespaces:

- Global namespaces: all identifiers visible and usable in the current module that are global. Global variables and standard functions are some examples of parts of the global namespace.
- Local namespaces: all identifiers visible and usable in the current function, or current block. Local variables and local functions (nested functions) inside a function are a examples of parts of the local namespace.
- Built-in namespace: it's always present and it's composed by all identifiers you can access directly via the Python CLI. It's defined by the current Python installation you're using in your system. 

Python allowes the developer  to know all identifiers binded to the current namespace by using the following three functions:

- `locals()` returns a dictionary where the key is the Python identifier of the language entity and the value is its value. All keys are available in the local namespace.
- `globals()` returns a dictionary where the key is the Python identifier of the language entity and the value is its value. All keys are available in the global namespace.
- `builtin` module, a collection of functions and utilities used to inspect the built-in namespace.

For example, you can use the previous in the following way:

```python
print(locals()) # prints all member of the local namespace
print(locals()) # prints all member of the local namespace

import builtin
print(builtin.__dir__) # prints all member of the builtin namespace
```

### 21.05. Name Conflicts

A name conflict happens when two variables, functions, or modules have the same name, causing Python to use the wrong one or hide another.

A local variable can hide a global variable with the same name:

```python
x = 10

def func():
    x = 5 # local variable x hides global variable x
    print(x)

func() # 5
print(x) # 10
```

If you use the same name as a built-in function, you hide it:

```python
len = 10
print(len) # 10
print(len([ 1, 2, 3 ])) # ERROR! TypeError: 'int' object is not callable
```

If a file has the same name as a standard module, Python may import the wrong one. For example, if you have a module called `math.py` in the current working directory, the following statement will import your `math` module (not the `math` module provided by Python during its installation):

```python
import math # this is your module, not the Python module (part of the Python STandard Library)
```

Two imported objects may share the same name:

```python
from math import sqrt
from cmath import sqrt # this module uses sqrt() function from cmath module
```

### 21.06. The `os` module

A particularly important module in Python is the `os` module. The `os` module allows the developer to work with files, directories, environment variables and system information. Thanks to the `os` module, you can:

- Operate with the file system of your local machine, by creating, updating, or removing files and directories.
- Create a custom path (relative, or absolute), or manipulate existent paths.
- Operate with environment variables of your local machine, by creating, updating, or removing env vars.
- Handle one, or more processes of the system.

The `os` module is platform-independent: it means the code necessary to carry out a task is independent if you're using Windows, Mac OS X, or Linux.

To use the `os` module you must first import the module:

```python
import os
```

To get the current working directory, use the `getcwd()` function:

```python
os.getcwd()
```

You can change the current working directory of the Python script with `chdir()`:

```python
os.chdir("/scripts/python")
```
To list the files in the current directory, use `listdir()`:

```python
os.listdir()
```

To create a directory, use `mkdir()`:

```python
os.mkdir("my_new_folder")
```

To create a nested directory with `mkdirs()`, exploits the rules of the relative, or absolute paths of your system. For example, the following lines create a parent directory called `parent` and a child directory called `child`:

```python
os.mkdirs("parent/child")
```

You can remove a directory with `rmdir()`:

```python
os.rmdir("my_new_folder")
```

To rename a file, use `rename()`:

```python
os.rename("old.txt", "new.txt")
```

To delete a file, use `remove()`:

```python
os.remove("new.txt")
```

You can join two (or more) paths by using the `join()` function:

```python
os.path.join("path1", "path2")
```

If you want to check if a file, or a directory exists in your system, you can use the `exists()` function:

```python
os.path.exists("my_file.txt")
```

`isdir()` and `isfile()` methods of `os.path` returns a boolean: `True` if the file, or directory exists; `False` otherwise.

```python
os.path.isfile("my_file.txt")
os.path.isdir("parent")
```

`os.path.isabs()` returns `True` if the specified path is an absolute path:

```python
os.path.isabs("/bin")
```

`os.path.samefile()` accepts two arguments and it returns `True` if the two arguments represent the same file:

```python
os.path.samefile("/bin/an_executable", "/bin/an_executable")
```

The `os.path` submodule contains two constant particularly useful to the path handling:

- `os.curdir`: returns the symbol of the current operating system used to represent the current directory.
- `os.pardir`: returns the symbol of the current operating system used to represent the parent directory.

For example, in Linux and Solaris operating systems these sumbols are `.` for the current directory and `..` for the parent directory. To write portable system (a best practice!) you should always use these constants instead of directly the symbols like `.` and `..`.

You can access to the environment variable of your system with the `os.environ` submodule.

```python
os.environ["HOME"]
```

To create a new variable, you can specify its name in the subscript operator and its value after the assignment operator:

```python
os.environ["NEW_ENV_VAR"] = "This is a new env var"
```

`os.name` returns the name of the operating system installed on your system, meanwhile through the `os.system()` function you can execute a subprocess, as if you were inside a shell. For example, the following statement:

```python
os.system("ls")
```

executes the `ls` command to list files and directories in the current working directory.

### 21.07. The `pathlib` module
 <!-- to do -->