# 0A. Python CLI

### 0A.01. Python an PIP versions

In this section we'are going to see some Python commands that can be used directly in a console, or a CLI (Command-Line Interface), like zsh, bash, csh, or any other console.

You can see the Python version in this way:

```bash
python -v
# or
python --version
```

You can see the PIP version with the following command:

```bash
pip -v
# or
pip --version
```

### 0A.02. Execute a program with Python

If you have a file called `main.py` (a source code written in Python, with the `.py` extension), you can use this command:

```bash
python main.py
```

### 0A.03. Install and uninstall packages

You can install an external package by using the `pip install` command:

```bash
pip install <packageName>
```

For example, if you want to install an external package called `cowsay`, you can use the following command:

```python
pip install cowsay
```

Pip will install not only the `cowsay` package, but all its dependencies also.

If you want to uninstall a package, you can use the `pip uninstall` command:

```bash
pip uninstall <packageName>
```

For example, if you want to remove the `cowsay` package from your system, you can use the following comand:

```bash
pip uninstall cowsay
```

Pip will uninstall not only the `cowsay` package, but all its depndencies also (if they aren't used by another package).

You can upgrade an external package by using the flag `--upgrade` before the package name:

```bash
pip install --upgrade <packageName>
```

For example:

```bash
pip install --upgrade cowsay
```

If you want a list of the installed Python packages, you can use:

```bash
pip list
```

If you want details informations about a specific Python package, you can use the `pip show` command, that has the following syntaxt:

```bash
pip show <packageName>
```

An example:

```bash
pip show cowsay
```

But how pip works? A Python package is an external Python library from your Python installation that you can add to you current installation with pip. pip is the official and the most common package manager for Python. It's based on the PyPI, the official repository of the Python packages: it's a very extended repository and in it you can find so many packages. Which are the main factors you should consider to install a packages?

- Community support and popularity.
- Frequency of updates.
- Documentation and ease of use.

### 0A.04 Use a package with the `import` keyword

In a Python program, you can import and use a package by the `import` statement:

```python
import math
```

After the previous line of code, you can use `math` identifier to access to all the variables, functions and other entities specified in the `math` module. Previous is the basic syntaxt of the `import` statement.

You can import more modules in a single line of code by separating with a comma (`,`):

```python
import math, random
```

You can rename a module by using the `as` keyword, that allows you to use an alias for a specific module:

```python
import numpy as np
```

You can import a specific item (a global variable, a constant, or a module) specified in a module by using the `from` keyword, in this way:

```python
from math import sqrt
```

You can specify more than one item by using the comma (`,`):

```python
from math import sqrt, pi
```

Another syntaxt used in Python is with the star operator (`*`): it means all items. If you want to import all items of the `math` package in your program, you can write something like this:

```python
from math import *
```

You can use both `from` and `as` in the same statement:

```python
from math import sqrt as square_root
```

In a Python program, the dot symbol (`.`) refers the current module (the current folder), meanwhile the double-dot (`..`) refers the parent module (the parent folder). You can import all modules specified in the current folder with the following statement:

```python
from . import * 
```

You can import all modules specified in the parent folder with the following statement:

```python
from .. import *
```

You can import a specific module also:

```python
from . import <moduleName>
from .. import <moduleName>
```

or a list of modules:

```python
from . import <moduleName>, <moduleName>, ..., <moduleName>
from .. import <moduleName>, <moduleName>, ..., <moduleName>
```

### 0A.05. Virtual environments with Python

Particular important are VENV (Virtual ENVironment). A virtual environment in Python is an isolated environment on your computer, where you can run and test your Python projects. It allows you to manage project-specific dependencies without interfering with other projects or the original Python installation. Think of a virtual environment as a separate "container" for each Python project.

Each enviroment:

- Has its own Python interpreter.
- Has its own set of installed packages.
- Is isolated from other virtual environments.
- Can have different versions of the same package.

Using virtual environments is important because:

- It prevents package version conflicts between projects.
- Makes projects more portable and reproducible.
- Keeps your system Python installation clean.
- Allows testing with different Python versions.

You can create a VENV with the following command:

```bash
python -m venv .venv
```

It creates a folder called `.venv` where all packages and dependencies are stored. To use a VENV, first you must activate it:

```bash
source .venv/bin/activate # for Linux, or Mac OS
.venv\Scripts\activate # for Windows
```

To deactivate a VENV:

```bash
deactivate
```

After you've activated the VENV, you can install one, or more packages:

```bash
pip install cowsay
```

Where `cowsay` is the package name. If you want a list of all installed packages in a specific VENV, you can use the following command:

```bash
pip freeze > requirements.txt
```

It creates (or modify, if it already exists) a file called `requirements.txt` in which each line specify a package with a version.
