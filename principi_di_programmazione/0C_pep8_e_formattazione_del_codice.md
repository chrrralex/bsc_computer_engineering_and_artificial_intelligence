# 0C. PEP 8 e formattazione del codice

### 0C.01. Formattazione del codice

Scrivere codice funzionante e testato e' fondamentale, ma un altro aspetto importante dello sviluppo software e' scrivere codice chiaro, leggibile e comprensibile. La documentazione ufficiale di Python contiene molte indicazioni pensate per guidare gli sviluppatori nella scrittura di codice ben formattato. L'obiettivo principale della formattazione e' rendere il codice il piu' possibile chiaro e leggibile. Inoltre, il codice dovrebbe essere ben documentato e contenere commenti informativi.

Un codice ben formattato rende molto piu' efficienti debugging, test e collaborazione. Guido Van Rossum ha detto: _"Code is read much more often than it is written."_. Seguire linee guida comuni aiuta a rendere il codice piu' standard e uniforme.

### 0C.02. Che cos'e' PEP 8?

PEP 8 e' la Python Enhancement Proposal numero 8. E' la guida di stile piu' importante per il codice Python, perche' definisce convenzioni che rendono i programmi leggibili, coerenti e manutenibili.

Le linee guida piu' importanti di PEP 8 sono le seguenti:

- Indentation: use 4 spaces per indentation level. Dont't use tabs.
- Line length: the maximum line length should be 79 characters. Long lines should be wrapped.
- Blank Lines: insert 2 blank lines before top-level functions, or classes. Insert 1 blank line between methods inside classes.
- Naming Conventions: use the `snake_case` for variables and functions, `UPPER_CASE` for contants, `PascalCase` for classes and `_underscore_prefix` for private variables and functions.
- Spaces Around Operators: use spaces around operators.
- Imports: import should be at the top of the file and one per line.
- Comments: use clear comments with a space after `#`.
- Docstrings: functions and modules should have docstrings.

### 0C.03. Convenzioni sui nomi

PEP 8 definisce anche convenzioni per i nomi.

Per variabili e funzioni, dovresti usare `snake_case`:

```python
this_is_a_variable = 10

def this_is_a_function():
    pass
```

Per le costanti, dovresti usare `UPPER_CASE`:

```python
PI = 3.14159
DAYS_PER_WEEK = 7
```

Per le classi, e' preferibile `PascalCase`:

```python
class MyClass:
    pass
```

Infine, per i membri privati di un modulo, e' consigliato usare `snake_case` con prefisso `_`:

```python
_private_member_of_a_module = 10
```

Per tutti gli identificatori del linguaggio, usa nomi descrittivi che rendano chiaro cosa rappresenta ciascuna entita'. In particolare, per le funzioni e' utile usare verbi, come `calculate_total()` o `print_person()`.

### 0C.04. Spazi bianchi

Gli spazi bianchi sono molto importanti in Python, perche' sono strettamente legati all'indentazione. Ricorda che Python non richiede un terminatore di riga come il punto e virgola di altri linguaggi.

In un file, le funzioni di alto livello dovrebbero essere separate da righe vuote per migliorare la leggibilita':

```python
def calculate_total(l):


    return sum(l)
```

Lo stesso vale per le classi:

```python
class Person:


    def __init__(self, fullName, age):
        self.fullName = fullName
        self.age = age
```

Nello stesso file o modulo, funzioni e classi dovrebbero essere separate in modo coerente, e i metodi all'interno di una classe dovrebbero essere intervallati da una riga vuota.

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

Cerca sempre di mantenere la lunghezza delle righe entro 79 caratteri.

Usa almeno uno spazio intorno agli operatori:

```python
z = 2
y = 5
x = 10 + z * y
```

Evita spazi inutili intorno a `=` negli argomenti con nome o nei parametri con valore di default:

```python
def f(a, b, c=10):
    pass

f(a=1, b=2, c=3)
```

Evita spazi nello slicing:

```python
l = [ 0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50 ]
l[:5]
l[3:6]
l[7:]
```

### 0C.05. Commenti

Alcune linee guida per scrivere commenti efficaci:

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

### 0C.06. Docstring

Le docstring sono il modo standard con cui Python documenta moduli, classi, funzioni e metodi. Le docstring sono stringhe letterali, normalmente scritte con triple virgolette, che l'interprete rende disponibili tramite l'attributo `__doc__`.

Per esempio, se hai la seguente funzione:

```python
def f():
    pass
```

Puoi aggiungere una docstring subito dopo l'intestazione della funzione:

```python
def f():
    """ This is a docstring """
    pass
```

Se poi accedi a `__doc__`, otterrai questo risultato:

```python
print(f.__doc__) # This is a docstring
```

Per default, `__doc__` prende la stringa immediatamente successiva all'intestazione di una funzione, classe, metodo o all'inizio del modulo. Per esempio, se hai un modulo `mymodule.py` con questo codice:

```python
""" This is a module docstring """

def f():
    """ This is a function docstring """

class MyClass:
    """ This is a class docstring """

    def my_method():
        """ This is a method docstring """
```

Puoi accedere alla documentazione del modulo usando `__doc__` sui vari membri:

```python
import mymodule

print(mymodule.__doc__) # This is a module docstring
print(mymodule.f.__doc__) # This is a function docstring
print(mymodule.MyClass.__doc__) # This is a class docstring
print(mymodule.MyClass.my_method.__doc__) # This is a method docstring
```

La funzione built-in `help()` svolge un ruolo analogo: restituisce la documentazione dell'oggetto passato come argomento. Per esempio:

```python
help(mymodule)
help(mymodule.f)
help(mymodule.MyClass)
help(mymodule.MyClass.my_method)
```

In sintesi, le docstring sono stringhe letterali usate per documentare moduli, classi, funzioni e metodi e hanno le seguenti proprieta':

- They appear as the first statement inside the object.
- They are written with triple quotes `"""`.
- They describe what the code does and how to use it.
- They are accessible through `help()` and the `__doc__` attribute.

Scrivere docstring e' una best practice fondamentale quando sviluppi moduli o librerie. Le indicazioni piu' importanti, basate su PEP 257, sono:

- Write docstrings for public modules, classes, and functions.
- Place the docstring immediately after the definition.
- Use triple double quotes `"""`.
- Start with a short one-line summary.
- Use the imperative mood (e.g., `"Return the sum"`, not `"Returns the sum"`).
- End the summary with a period.
- Keep the summary short (one line).
- Add more details in the following lines if needed.
- Explain parameters and return values when necessary.
- Focus on what the function does, not how it works internally.
