# 20. Set e frozenset

In Python, un set e' un tipo di dato iterabile, mutabile e non ordinato, ottimizzato per memorizzare valori unici. Un set e' racchiuso tra parentesi graffe. In breve:

- un set e' mutabile: puo' essere modificato aggiungendo, aggiornando o rimuovendo uno o piu' elementi,
- un set e' non ordinato: non esiste un ordine significativo degli elementi,
- un set ammette solo valori unici: tutti i duplicati vengono ignorati.

Puoi creare un set con un letterale di set in questo modo:

```python
s = { 1, 2, 3 }
print(s) # { 1, 2, 3 }
```

Se specifichi uno o piu' elementi duplicati, il set conservera' solo quelli unici:

```python
s = { 1, 2, 2, 2, 3, 3, 3 }
print(s) # { 1, 2, 3 }
```

In breve, un set elimina automaticamente i duplicati.

La funzione `len()` restituisce il numero di elementi contenuti in un set:

```python
s = { 1, 2, 3, 4, 5 }
print(len(s)) # 5
```

Le funzioni `min()` e `max()` restituiscono rispettivamente il valore minimo e il valore massimo del set:

```python
s = { 1, 2, 3 }
print(min(s)) # 1
print(max(s)) # 3
```

Puoi convertire liste e tuple in un set usando la funzione built-in `set()`:

```python
s1 = set([ 1, 2, 3 ])
s2 = set(( "a", "b", "c" ))
print(s1) # { 1, 2, 3 }
print(s2) # { "a", "b", "c" }
```

Non puoi usare le parentesi graffe vuote `{}` per indicare un set vuoto, perche' Python le interpreta come un dizionario vuoto. Per creare un set vuoto devi usare `set()`:

```python
s = set()
print(s) # set()
```

Puoi aggiungere un elemento con `add()` oppure piu' elementi con `update()`. Se provi ad aggiungere un elemento gia' presente, il set lo ignora:

```python
s = set()
s.add(1)
s.add(1)
s.add(2)
s.update([ 1, 2, 3, 4 ])
print(s) # { 1, 2, 3, 4 }
```

Puoi usare `remove()` per eliminare un elemento. Se l'elemento non esiste, Python genera un errore:

```python
s = { 10, 20, 30 }
s.remove(10)
s.remove(100) # ERROR! KeyError: 100
```

Il metodo `discard()` e' simile a `remove()`, ma se l'elemento non esiste Python non genera alcun errore:

```python
s = { 10, 20, 30 }
s.discard(10)
s.discard(100) # 100 isn't in the set, but no error is thrown
```

Puoi verificare se un elemento appartiene al set usando gli operatori `in` e `not in`:

```python
s = { 1, 2, 3 }
print(1 in s) # True
print(10 not in s) # True
print(100 in s) # False
```

Con i set puoi eseguire diverse operazioni:

- `|` is the union operator.
- `&` is the intersection operator.
- `-` is the difference operator.
- `^` is the symmetric difference operator.

Ecco alcuni esempi:

```python
a = { 1, 2, 3 }
b = { 3, 4, 5 }

print(a | b) # { 1, 2, 3, 4, 5 }
print(a & b) # { 3 }
print(a - b) # { 1, 2 }
print(a ^ b) # { 1, 2, 4, 5 }
```

Un `frozenset` e' la versione immutabile di un set: una volta creato, non puo' essere modificato. Non e' quindi possibile aggiungere, aggiornare o rimuovere elementi. Un `frozenset` continua comunque a contenere elementi unici e non ordinati, proprio come un normale set.

Puoi creare un `frozenset` con la funzione built-in `frozenset()`:

```python
fs = frozenset([ 1, 1, 2, 3, 4, 4, 5 ])
print(fs) # frozenset({ 1, 2, 3, 4, 5 })
```

Come puoi vedere, Python mostra esplicitamente che l'entita' stampata e' un `frozenset`, usando la forma `frozenset(elements)`.

Se provi ad aggiungere un elemento, ottieni un errore:

```python
fs.add(10) # ERROR! AttributeError: 'frozenset' object has no attribute 'add'
```

I `frozenset` possono essere usati con gli stessi operatori dei set:

```python
a = frozenset({ 1, 2, 3 })
b = frozenset({ 3, 4, 5 })

print(a | b) # frozenset({ 1, 2, 3, 4, 5 })
print(a & b) # frozenset({ 3 })
print(a - b) # frozenset({ 1, 2 })
print(a ^  b) # frozenset({ 1, 2, 4, 5 })
```

Essendo immutabile, a differenza di un set normale, un `frozenset` puo' essere usato come chiave in un dizionario, anche se non e' un caso particolarmente comune. Ecco un esempio:

```python
d = {
    frozenset({ 1, 2, 3 }): "Hello!"
}
print(d[frozenset({ 1, 2, 3 })]) # "Hello!"
```

Puoi creare un `frozenset` vuoto in questo modo:

```python
fs = frozenset()
print(fs) # fs = frozenset()
```

`len()`, `min()` e `max()` funzionano con un `frozenset` esattamente come funzionano con un set.
