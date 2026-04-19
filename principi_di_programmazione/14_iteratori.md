# 14. Iteratori

Un iteratore e' un oggetto che contiene un numero contabile di valori. Un iteratore e' un oggetto su cui e' possibile iterare, cioe' attraversare uno alla volta tutti i valori. Tecnicamente, in Python, un iteratore e' un oggetto che implementa il protocollo degli iteratori, composto dai metodi `__iter__()` e `__next__()`.

Liste, tuple, dizionari e set sono tutti oggetti iterabili. Sono contenitori iterabili da cui puoi ottenere un iteratore. Tutti questi oggetti possono essere passati alla funzione `iter()`, usata proprio per ottenere un iteratore:

```python
t = ("apple", "banana", "cherry")
it = iter(t)
print(next(it)) # "apple"
print(next(it)) # "banana"
print(next(it)) # "cherry"
```

Se provi a invocare una quarta volta la funzione built-in `next()`, otterrai il seguente errore:

```bash
ERROR! StopIteration
```

Anche le stringhe sono oggetti iterabili e possono restituire un iteratore:

```python
s = "banana"
it = iter(s)
print(next(it)) # "b"
print(next(it)) # "a"
print(next(it)) # "n"
print(next(it)) # "a"
print(next(it)) # "n"
print(next(it)) # "a"
```

Per creare un oggetto, o una classe, che si comporti come iteratore, devi implementare i metodi `__iter__()` e `__next__()`. Tutte le classi hanno un metodo `__init__()` che permette di inizializzare l'oggetto quando viene creato. Il metodo `__iter__()` ha un ruolo simile, ma deve sempre restituire l'oggetto iteratore stesso. Il metodo `__next__()` deve invece restituire l'elemento successivo della sequenza.

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    x = self.a
    self.a += 1
    return x

myNumbers = MyNumbers()
it = iter(myNumbers)

print(next(it)) # 1
print(next(it)) # 2
print(next(it)) # 3
print(next(it)) # 4
print(next(it)) # 5
```

L'esempio precedente continuerebbe indefinitamente se avessi abbastanza chiamate a `next()`, oppure se lo usassi in un ciclo `for`. Per evitare che l'iterazione prosegua all'infinito, possiamo usare `StopIteration`. Nel metodo `__next__()` possiamo aggiungere una condizione di terminazione che sollevi questa eccezione quando l'iterazione deve finire:

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self

  def __next__(self):
    if self.a <= 5:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

myNumbers = MyNumbers()
it = iter(myNumbers)

for x in it:
  print(x) # 1, 2, 3, 4, 5
```

Le *generator expressions* sono un modo compatto per creare generatori. Ricorda che un generatore produce i valori uno alla volta, in modo lazy, invece di costruire subito l'intera lista in memoria. Questo li rende efficienti dal punto di vista della memoria. La sintassi di base e':

```python
(expression for item in iterable)
```

Un esempio semplice e' la generazione dei quadrati dei numeri tra `1` e `5`:

```python
squared_generator = ( x**2 for x in range(1, 6))
print(squared_generator) # <generator object <genexpr> at 0x7c041c50dd80>
```

Per stampare ogni numero, dobbiamo usare un ciclo `for`:

```python
squared_generator = ( x**2 for x in range(1, 6))
for x in squared_generator:
  print(x) # 1, 4, 9, 16, 25
```

Ogni valore viene prodotto solo quando serve: la prima iterazione del `for` ottiene il primo valore dal generatore, la seconda iterazione il secondo, e cosi' via.
