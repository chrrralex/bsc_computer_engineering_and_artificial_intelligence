# 03. Tipi di dato

Python ha i seguenti tipi di dato:

- Tipi testuali: `str`.
- Tipi numerici: `int`, `float`, `complex`.
- Tipi sequenza: `list`, `tuple`, `range`.
- Tipi mapping: `dict`.
- Tipi insieme: `set`, `frozenset`.
- Tipo booleano: `bool`.
- Tipi binari: `bytes`, `bytearray`, `memoryview`.
- Tipo nullo: `NoneType`, il cui valore e' `None`.

La funzione `type()` accetta un letterale, una variabile o una costante e mostra il relativo tipo di dato:

```python
a = 10
print(type(a))  # <class 'int'>

b = "A string"
print(type(b))  # <class 'str'>

c = False
print(type(c))  # <class 'bool'>

d = [1, 2, 3]
print(type(d))  # <class 'list'>
```

Python mette a disposizione anche diverse funzioni built-in, anch'esse parte della PSL:

- `int()` converte in `int`.
- `bool()` converte in `bool`.
- `float()` converte in `float`.
- `str()` converte in `str`.
- `complex()` converte in `complex`.
- `range()` produce un intervallo di valori.
- `list()` crea una `list`.
- `dict()` crea un `dict`.
- `set()` crea un `set`.
- `bytes()` produce una sequenza di byte.
- `frozenset()` crea un `frozenset`.
- `bytearray()` e `memoryview()` sono usati soprattutto in contesti di ottimizzazione e gestione efficiente dei dati binari.

Un caso d'uso molto comune di `int()` si ha quando chiedi all'utente di inserire la propria eta':

```python
age = int(input("Your age: "))
print(age)
```