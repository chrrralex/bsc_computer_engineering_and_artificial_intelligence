# 06. Tuple

### 06.01. Panoramica

Una tupla e' un tipo di collezione usato per memorizzare piu' valori. Una tupla e' una struttura dati immutabile, cioe' i suoi elementi non possono essere modificati. Una tupla e' ordinata, come le liste in Python, ed e' definita dalle parentesi tonde `()`.

```python
t = ( "apple", "banana", "cherry" )
```

Una tupla, in Python, ammette valori duplicati:

```python
t = ( "apple", "apple", "banana", "cherry", "orange", "orange" )
```

Per conoscere la lunghezza di una tupla, puoi usare la funzione built-in `len()`:

```python
t = ( 1, 2, 3, 4, 5 )
len(t) # 5
```

Se devi creare una tupla con un solo elemento, Python non la riconosce come tupla se non specifichi una virgola dopo l'elemento. Ricorda che le parentesi tonde sono usate anche per le espressioni, per questo la virgola e' necessaria:

```python
t = ( "apple", )
t = ( 1, )
not_a_tuple = (10) # Python lo riconosce come intero, non come tupla
```

Una tupla puo' contenere tipi di dato diversi:

```python
t = ( 1, True, "apple", 10.50, [ 1, 2, 3 ] )
```

Nel caso precedente, il primo elemento e' un intero, il secondo e' un valore booleano, il terzo e' una stringa, il quarto un numero floating-point e il quinto una lista.

Per controllare il tipo di una tupla, puoi usare `type()`:

```python
t = (10,0)
type(t) # <class 'tuple'>
```

Python fornisce anche la funzione built-in `tuple()`, chiamata costruttore di tuple. Accetta qualunque iterabile e restituisce una tupla con gli stessi elementi.

### 06.02. Accesso agli elementi

Come per le liste, puoi accedere a un elemento specifico di una tupla tramite indice. L'indice e' un intero compreso tra `0` e `len(t) - 1`:

```python
t = ( 10, 20, 30 )
t[0] # 10
t[2] # 30
```

Sono ammessi anche indici negativi, nel qual caso il conteggio parte dalla fine della tupla:

```python
t = ( "apple", "cherry", "orange" )
t[-1] # "orange"
```

Come per le liste, puoi usare anche gli intervalli di indici:

```python
t = ( "apple", "cherry", "orange" )
t[-3:-1] # ( "apple", "cherry" )
```

La sintassi dell'operatore di slicing e' la stessa vista per le liste. Ricorda che:

- `[n:m]` restituisce gli elementi da `n` incluso a `m` escluso.
- `[:m]` restituisce gli elementi da `0` incluso a `m` escluso.
- `[n:]` restituisce gli elementi da `n` incluso fino alla fine della tupla.
- `[:]` restituisce una copia dell'intera tupla.

Se vuoi verificare se un elemento e' presente in una tupla, puoi usare l'operatore `in`:

```python
t = ( 1, 2, 3 )
10 in t # False
3 in t # True
```

L'operatore `in` restituisce sempre un valore booleano: `True` se l'elemento e' presente, `False` altrimenti.

### 06.03. Aggiornamento degli elementi

Una volta creata, una tupla non puo' essere modificata. Le tuple sono immutabili: questo significa che non sono ammesse operazioni di aggiornamento. Un modo indiretto per cambiare un elemento di una tupla e':

- Convertire la tupla in una lista, che e' mutabile.
- Modificare l'elemento desiderato.
- Convertire di nuovo la lista aggiornata in una tupla, che e' immutabile.

Ecco un esempio:

```python
t = ( 1, 2, 3, 4, 5 )
lt = list(t)
lt[2] = 30
t = tuple(lt)
print(t) # ( 1, 2, 30, 4, 5 )
```

### 06.04. Unpacking

L'operazione di unpacking significa che ogni valore della tupla puo' essere estratto e assegnato a una variabile. La sintassi e' molto simile all'assegnazione multipla:

```python
fruits = ( "apple", "banana", "cherry" )
( green, yellow, red ) = fruits
```

Nel frammento precedente, `green` vale `"apple"`, `yellow` vale `"banana"` e `red` vale `"cherry"`.

Puoi usare l'operatore asterisco se vuoi decomporre la tupla in meno variabili rispetto al numero di elementi presenti:

```python
fruits = ( "apple", "banana", "cherry", "orange", "kiwi" )
(apple, banana, *others) = fruits
```

`apple` conterra' il primo elemento, `banana` il secondo, mentre `others` conterra' una lista con tutti gli altri elementi, da `cherry` a `kiwi`:

```python
print(apple) # "apple"
print(banana) # "banana"
print(others) # [ 'cherry', 'orange', 'kiwi' ]
```

Puoi usare l'asterisco anche in mezzo all'assegnazione. Python dedurra' automaticamente quali valori assegnare alle altre variabili:

```python
fruits = ( "apple", "banana", "cherry", "orange", "kiwi" )
(apple, *others, kiwi) = fruits
print(apple) # "apple"
print(others) # [ 'banana', 'cherry', 'orange' ]
print(kiwi) # "kiwi"
```

### 06.05. Unione

Puoi usare l'operatore `+` per unire due o piu' tuple:

```python
t1 = ( 1, 2, 3 )
t2 = ( "a", "b", "c" )
t3 = ( True, False )
print(t1 + t2) # ( 1, 2, 3, "a", "b", "c" )
print(t1 + t2 + t3) # ( 1, 2, 3, "a", "b", "c", True, False )
```

Puoi anche moltiplicare una tupla con l'operatore `*`. In questo caso il moltiplicatore deve essere un intero e l'espressione restituisce una nuova tupla con gli stessi elementi ripetuti:

```python
t = ( 1, 2 )
print(t * 3) # ( 1, 2, 1, 2, 1, 2 )
```

### 06.06. La funzione `zip()`

La funzione `zip()` ha come scopo principale creare una sequenza di tuple accoppiando, elemento per elemento, due iterabili, come due liste o due tuple. Per esempio, se hai due liste come le seguenti:

```python
l1 = [ 1, 2, 3 ]
l2 = [ "a", "b", "c" ]
```

Puoi usare la funzione `zip()` con `l1` e `l2` come argomenti posizionali, in questo modo:

```python
results = zip(l1, l2)
print(results) # [ (1, 'a'), (2, 'b'), (3, 'c') ]
```

Come puoi vedere, ogni elemento della sequenza restituita da `zip()` e' una tupla. La prima tupla contiene il primo elemento di `l1` e il primo elemento di `l2`, la seconda contiene il secondo elemento di entrambe le liste, e cosi' via.

Puoi usare `zip()` passando anche piu' di due liste:

```python
l1 = [ 1, 2, 3 ]
l2 = [ "a", "b", "c" ]
l3 = [ 0.5, 1.5, 2.5 ]

result = zip(l1, l2, l3)
print(list(result)) # [ (1, 'a', 0.5), (2, 'b', 1.5), (3, 'c', 2.5) ]
```

Ogni tupla ha un numero di elementi pari al numero di argomenti passati a `zip()`.

Finora abbiamo usato `zip()` con argomenti della stessa lunghezza. Se una delle liste ha piu' elementi, `zip()` considera sempre la lunghezza minima tra gli iterabili ricevuti, quindi gli elementi in eccesso vengono ignorati.

Per ulteriori dettagli su `zip()`, puoi consultare la documentazione ufficiale di Python.
