# 17. Comprensione di liste

La *list comprehension* offre una sintassi piu' corta quando vuoi creare una nuova lista a partire dai valori di una lista esistente. Per esempio: data una lista `fruits`, vuoi ottenere una nuova lista contenente solo i frutti che hanno la lettera `"a"` nel nome. Senza list comprehension dovresti scrivere un ciclo `for` con un test condizionale al suo interno:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = []

for x in fruits:
  if "a" in x:
    newlist.append(x)

print(newlist)
```

Con la list comprehension puoi fare tutto questo in una sola riga di codice:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

Una list comprehension ha la seguente sintassi:

```python
[expression for item in iterable if condition]
```

dove:

- `expression` e' una valida espressione Python usata per trasformare ciascun elemento,
- `item` e' il nome della variabile che assume ciascun valore dell'iterabile,
- `iterable` e' la lista o, piu' in generale, l'oggetto iterabile su cui vuoi iterare,
- `condition` e' una condizione booleana usata per filtrare gli elementi dell'iterabile. E' opzionale e puo' essere omessa.

Vediamo ora alcuni esempi, dal piu' semplice al piu' articolato. La lista originale e' la seguente:

```python
l = [1, 2, 3, 4, 5]
```

**Esempio 1**: creare una lista a partire da un'altra lista.

```python
newl = [e for e in l]
print(newl)  # [1, 2, 3, 4, 5]
```

**Esempio 2**: creare una lista in cui ogni elemento e' moltiplicato per `2`.

```python
newl = [e * 2 for e in l]
print(newl)  # [2, 4, 6, 8, 10]
```

**Esempio 3**: creare una lista contenente solo i numeri pari.

```python
newl = [e for e in l if e % 2 == 0]
print(newl)  # [2, 4]
```

**Esempio 4**: creare una lista contenente solo i numeri pari, ma moltiplicati per `2`.

```python
newl = [e * 2 for e in l if e % 2 == 0]
print(newl)  # [4, 8]
```

**Esempio 5**: creare una lista contenente solo i numeri pari, ma elevati al quadrato.

```python
newl = [e**2 for e in l if e % 2 == 0]
print(newl)  # [4, 16]
```

**Esempio 6**: creare una lista in cui ogni elemento e' la stringa `"even"` oppure `"odd"` in base al valore dell'elemento. Questo esempio usa la sintassi `if` inline:

```python
newl = ["even" if e % 2 == 0 else "odd" for e in l]
print(newl)  # ["odd", "even", "odd", "even", "odd"]
```

**Esempio 7**: usare piu' `for` dentro una list comprehension. Nel seguente esempio invochiamo due volte la funzione `range()`. Il codice seguente:

```python
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs)  # [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]
```

e' equivalente al seguente codice scritto in forma estesa:

```python
pairs = []
for x in range(3):
  for y in range(3):
    pairs.append((x, y))
print(pairs)  # [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]
```
