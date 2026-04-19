# 15. Dizionari

### 15.01. Panoramica

Un dizionario, spesso abbreviato in `dict`, e' una struttura dati chiave-valore che permette di associare ogni valore a una chiave specifica. Per esempio, il seguente e' un letterale di dizionario introdotto dalle parentesi graffe:

```python
person = {
    "firstName": "Christian",
    "lastName": "Atzeni",
    "age": 28
}
```

Il dizionario precedente, memorizzato nella variabile `person`, ha tre chiavi:

- `firstName`: a string containing `"Christian"`.
- `lastName`: a string containing `"Atzeni"`.
- `age`: an integer number containing `28`.

In Python 3.7 e versioni successive, i dizionari sono ordinati. In Python 3.6 e precedenti erano invece considerati non ordinati. I dizionari sono inoltre mutabili e puoi stamparli facilmente con `print()`.

```python
print(person) # { 'firstName': 'Christian', 'lastName': 'Atzeni', 'age': 28 }
```

Puoi usare l'operatore di indicizzazione `[]` per accedere a un particolare valore del dizionario:

```python
print(person["age"]) # 28
```

Puoi modificare un valore usando la chiave a sinistra dell'operatore di assegnazione:

```python
person["age"] = 30
print(person["age"]) # 30
```

Le chiavi duplicate non sono ammesse: una chiave deve essere unica. Se provi a usare la stessa chiave, il valore precedente verra' sostituito. Puoi aggiungere una nuova chiave specificandola nell'operatore di indicizzazione a sinistra dell'assegnazione:

```python
person["role"] = "Developer"
```

Se applichi `len()` a un dizionario, ottieni il numero di coppie chiave-valore memorizzate:

```python
d = {
    "a": 1,
    "b": 2,
    "c": 3
}
print(len(d)) # 3
```

Python fornisce anche la funzione built-in `dict()`, che accetta una serie di parametri con nome e restituisce il dizionario corrispondente:

```python
d = dict(a = 1, b = 2, c = 3)
print(d) # { 'a': 1, 'b': 2, 'c': 3 }
```

Infine, la funzione built-in `type()`, applicata a un dizionario, restituisce:

```bash
<class 'dict'>
```

In Python, un dizionario vuoto e' rappresentato da `{}`.

### 15.02. Leggere, aggiungere, aggiornare e rimuovere elementi

Puoi accedere a un elemento tramite l'operatore di indicizzazione `[]`:

```python
d = { "a": 1, "b": 2, "c": 3 }
print(d["a"]) # 1
```

Puoi anche ottenere un elemento usando il metodo `get()`:

```python
print(d.get("a")) # 1
```

Per ottenere la lista delle chiavi presenti nel dizionario, puoi usare il metodo `keys()`:

```python
print(d.keys()) # dict_keys([ 'a', 'b', 'c' ])
```

Come puoi vedere, il valore restituito da `keys()` e' di tipo `dict_keys`. Si tratta di una vista sul dizionario, quindi ogni modifica al dizionario si riflette anche in questa vista.

Per ottenere la lista dei valori presenti nel dizionario, puoi usare il metodo `values()`:

```python
print(d.values()) # dict_values([ 1, 2, 3 ])
```

C'e' poi il metodo `items()`, che restituisce una sequenza di tuple: in ogni tupla il primo elemento e' la chiave e il secondo e' il valore.

```python
print(d.items()) # dict_items([ ('a', 1), ('b', 2), ('c', 3) ])
```

Il valore restituito e' di tipo `dict_items`.

L'operatore `in` puo' essere usato anche con i dizionari: a sinistra specifichi la chiave, a destra il dizionario in cui vuoi verificare la sua presenza.

```python
if "a" in d:
    print("a is a key stored in d") # printed
if "e" in d:
    print("e is a key stored in d") # not printed
```

Puoi cambiare un valore usando la chiave corrispondente:

```python
d["a"] = 10
d["b"] = 20
d["c"] = 30
print(d) # { 'a': 10, 'b': 20, 'c': 30 }
```

Per cambiare uno o piu' elementi c'e' anche il metodo `update()`, che accetta un dizionario oppure un iterabile di coppie chiave-valore:

```python
d.update({ "a": 50 })
print(d) # { 'a': 50, 'b': 20, 'c': 30 }
d.update({ "b": 70, "c": 90 })
print(d) # { 'a': 50, 'b': 70, 'c': 90 }
```

Puoi aggiungere un elemento specificando la nuova chiave a sinistra dell'assegnazione:

```python
d["d"] = 110
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'd': 110 }
```

Un altro modo per aggiungere elementi e' ancora `update()`, come visto sopra:

```python
d.update({ "e": 130 })
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'e': 130 }
d.update({ "f": 150, "g": 170 })
print(d) # { 'a': 50, 'b': 70, 'c': 90, 'e': 130, 'f': 150, 'g': 170 }
```

Infine, puoi rimuovere un elemento tramite la sua chiave usando `pop()`:

```python
d.pop("g")
d.pop("a")
d.pop("c")
d.pop("f")
print(d) # { 'b': 70, 'e': 130 }
```

Se stai usando Python 3.7 o successivo, puoi usare `popitem()`, che rimuove l'ultimo elemento del dizionario:

```python
d.popitem()
print(d) # { 'b': 70 }
```

Un altro modo per rimuovere un elemento del dizionario e' usare la parola chiave `del`:

```python
del d["b"]
print(d) # {}
```

### 15.03. Iterare sui dizionari

Se provi a usare un ciclo `for` su un dizionario, ad esempio cosi':

```python
d = { "a": 1, "b": 2, "c": 3 }
for x in d:
    print(x) # a, b, c
```

la variabile `x` assumera' via via ciascuna chiave del dizionario: prima `"a"`, poi `"b"` e infine `"c"`. Per stampare le coppie chiave-valore puoi usare `items()`, come visto nel paragrafo precedente:

```python
for t in d.items():
    print(t[0] + " - " + str(t[1])) # a - 1, b - 2, c - 3
```

The previous `for` can be written also in this way:

```python
for k, v in d.items():
    print(k + " - " + str(v)) # a - 1, b - 2, c - 3
```

e l'output e' lo stesso. Nota che abbiamo usato `str()` per convertire un intero in stringa, altrimenti Python genera un errore se provi a concatenare una stringa con un intero tramite `+`.

Puoi iterare anche sulle sole chiavi usando `keys()`:

```python
for k in d.keys():
    print(k) # a, b, c
```

oppure puoi iterare sui valori usando `values()`:

```python
for v in d.values():
    print(v) # 1, 2, 3
```

### 15.04. Copiare dizionari

Non puoi copiare davvero un dizionario semplicemente scrivendo `dict2 = dict1`. In quel caso `dict2` diventa solo un riferimento a `dict1`, e le modifiche fatte a uno dei due saranno visibili anche nell'altro.

Per creare una copia puoi usare, per esempio, il metodo `copy()`:

```python
dict1 = { "a": 1, "b": 2, "c": 3 }
dict2 = dict1.copy()
dict2.update({ "a": 100, "b": 200 })
print(dict1) # { 'a': 1, 'b': 2, 'c': 3 }
print(dict2) # { 'a': 100, 'b': 200, 'c': 3 }
```

### 15.05. Metodi

`clear()` rimuove tutti gli elementi dal dizionario:

```python
d = { "a": 1, "b": 2, "c": 3 }
d.clear()
print(d) # {}
```

`fromkeys()` restituisce un dizionario con le chiavi e il valore specificati:

```python
ks = ('key1', 'key2', 'key3')
v = 0
d = dict.fromkeys(ks, v)
print(d) # { 'key1': 0, 'key2': 0, 'key3': 0 }
```

`setdefault()` restituisce il valore della chiave specificata. Se la chiave non esiste, la inserisce con il valore indicato. Ecco un esempio:

```python
car = {
  "brand": "Peugeot",
  "model": "208",
  "year": 2023
}

x = car.setdefault("model", "-")
print(x) # 208

y = car.setdefault("color", "-")
print(y) # "-"
```
