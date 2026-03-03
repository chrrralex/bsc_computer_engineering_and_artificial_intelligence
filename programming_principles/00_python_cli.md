# 00. Python CLI

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

If you have a file called `main.py` (a source code written in Python, with the `.py` extension), you can use this command:

```bash
python main.py
```

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
