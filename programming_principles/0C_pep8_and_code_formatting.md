# 0C. PEP 8 and Code Formatting

### 0C.01. Code formatting

Writing wokrking and tested code is really important, but another important side of the software development is to write clear, readable and understandable code. The official documentation of Python has many parts and advices created to guide the developers to write a well-formatted code. The main code of the code formatting is to make the code more clear, readable and understandable as possible. The Python documentation provides different guidelines and advices; moreover, the code should be well-documented and contain informative comments.

A well-formatted code makes debugging, testing and collaborating on a project much more efficient. Guido Van Rossum tells: _"Code is read much more often than it is written."_. Guidelines and well-formatted code makes the code-self a standard code.

### 0C.02. What is PEP 8?

PEP 8 is the Python Enhancement Proposal number 8. PEP 8 is the most important guidelines for writing Python code, cause it defines coding conventions to make Python programs readable, consistent, and maintainable. PEP 8 specifically describes style guidelines.

The most important guidelines of the PEP 8 are the following:

- Indentation: use 4 spaces per indentation level. Dont't use tabs.
- Line length: the maximum line length should be 79 characters. Long lines should be wrapped.
- Blank Lines: insert 2 blank lines before top-level functions, or classes. Insert 1 blank line between methods inside classes.
- Naming Conventions: use the `snake_case` for variables and functions, `UPPER_CASE` for contants, `PascalCase` for classes and `_underscore_prefix` for private variables and functions.
- Spaces Around Operators: use spaces around operators.
- Imports: import should be at the top of the file and one per line.
- Comments: use clear comments with a space after `#`.
- Docstrings: functions and modules should have docstrings.

### 0C.03. Naming conventions

PEP 8 defines the naming guidelines.

For variable and functions, you should use the `snake_case`:

```python
this_is_a_variable = 10

def this_is_a_function():
    pass
```

For constants, you should use the `UPPER_CASE`:

```python
PI = 3.14159
DAYS_PER_WEEK = 7
```

For classes, you should prefer the `PascalCase`:

```python
class MyClass:
    pass
```

Finally, for the private members of a module, you should use the `snake_case`, but with the underscore character (`_`) as prefix:

```python
_private_member_of_a_module = 10
```

For all identifiers of all language entities (variables, constants, functions, classes and others), use descriptive names to make the code clear what the entity represents. In particular, for functions use verbs (like `calculate_total()`, or `print_person()`). 

### 0C.04. Whitespaces

Whitespaces are very important in Python, cuase they're directly linked to the indentation. Remember that Python is a language doesn't need the end-of-line character (in other programming language, like C and C++, represented by the semicolon character, `;`).

In a function, at the top you should insert at least two empty lines to improve the readability:

```python
def calculate_total(l):


    return sum(l)
```

Also for classes:

```python
class Person:


    def __init__(self, fullName, age):
        self.fullName = fullName
        self.age = age
```

In the same file, or module, two functions (or two classes, or a function and a class) should be separated by one empty line. Two methods inside a class should be separated by one empty line.

```python
def f1():


    pass

def f2():


    pass

def f3():


    pass

class Person:


    def __init__(self, fullName, age):
        self.fullName = fullName
        self.age = age
    
    def getFullName(self):
        return self.fullName
    
    def getAge(self):
        return self.age
```

Always try to keep the length of the code line under, or at most equal to, 79 characters.

Always use at least one blank space between operand and operators:

```python
z = 2
y = 5
x = 10 + z * y
```

Avoid using blank spaces between the keyword and the `=` operator for keyword argument, or for default arguments:

```python
def f(a, b, c=10):
    pass

f(a=1, b=2, c=3)
```

Avoid using blank spaces for the range operator:

```python
l = [ 0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50 ]
l[:5]
l[3:6]
l[7:]
```

### 0C.05. Comments

Some guidelines to write efficient comments:

- Write comments for the reason, not the action. Code should describe what it does; comments should explain why something is done a certain way.
- Keep comments accurate and updated. If code changes, related comments should be reviewed and updated as well.
- Prefer clear code over excessive comments. If the code can be made more readable through better naming or structure, that is usually better than adding comments.
- Use comments to explain complex or non-obvious logic. They are most valuable when the intention of the code might not be immediately clear.
- Keep comments concise and focused. Avoid long explanations that make code harder to scan.
- Use consistent formatting. Begin comments with # followed by a space, and keep a consistent style throughout the project.
- Place comments close to the code they describe. This helps readers quickly understand the relevant section.
- Use block comments for explaining sections of code. These can describe the purpose of a group of related statements.
- Use inline comments sparingly. They should only clarify specific lines when necessary.
- Use docstrings instead of comments for modules, classes, and functions. Docstrings are intended for documentation and tooling.
- Avoid redundant or obvious comments. Comments that simply restate the code add little value.
- Remove obsolete or commented-out code. Version control systems should be used to track previous versions.
- Use markers like TODO or FIXME to indicate pending improvements or known issues.

### 0C.06. Docstrings
<!-- to do -->
