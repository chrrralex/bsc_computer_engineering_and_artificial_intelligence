# 05. Liste

### 05.01. Panoramica

Una lista e' una collezione ordinata con lunghezza modificabile durante l'esecuzione del programma. Una lista puo' contenere qualunque tipo di valore e ciascun elemento puo' avere il proprio tipo. In Python riconosci una lista dalla presenza delle parentesi quadre `[]`, che racchiudono gli elementi.

Puoi dichiarare una lista separando gli elementi con la virgola `,` e racchiudendoli tra parentesi quadre:

```python
aList = [1, 2, 3]
```

Una lista puo' contenere duplicati:

```python
aList = [1, 2, 3, 4, 5, 1, 2, 3]
```

Inoltre, una lista puo' contenere elementi di tipo diverso:

```python
aList = [True, "A string", 10, 10.5, 5.0 + 10j]
```

Un elemento della lista e' chiamato *elemento*. La lista e' ordinata, modificabile e ammette valori duplicati. Puoi accedere a un elemento tramite indice, cioe' un numero compreso tra `0` e la lunghezza della lista meno uno:

```python
aList = [1, 2, 3]
aList[1]  # 2
aList[0]  # 1
```

Puoi scoprire la lunghezza di una lista usando la funzione built-in `len()`:

```python
aList = [1, 2, 3]
len(aList)  # 3
```

La lunghezza di una lista e' il numero di elementi contenuti nella lista.

### 05.02. Accesso agli elementi

Considera la seguente lista:

```python
l = [1, 2, 3, 4, 5]
```

Puoi accedere a un elemento della lista usando un indice compreso tra `0` e `len(l) - 1`:

```python
l[1]  # 2
l[3]  # 4
```

Gli indici negativi partono invece dalla fine della lista:

```python
l[-1]  # 5
l[-2]  # 4
```

Puoi accedere a piu' elementi in un solo passo usando un intervallo di indici, con sintassi `[min:max]`:

- Se `min` non e' presente, il valore di default e' `0`.
- Se `max` non e' presente, il valore di default e' la fine della lista.

Ecco alcuni esempi:

```python
l[1:3]  # [2, 3]
l[:2]  # [1, 2]
l[3:]  # [4, 5]
```

Puoi usare anche indici negativi:

```python
l[-5:-3]  # [1, 2]
```

Se vuoi verificare se un elemento e' presente in una lista, puoi usare l'operatore `in`:

```python
10 in l  # False
3 in l  # True
```

L'operatore `in` restituisce sempre un valore booleano.

### 05.03. Modifica degli elementi

Per modificare un elemento di una lista, puoi usare l'operatore di indicizzazione `[]` a sinistra dell'operatore di assegnazione `=`:

```python
l[1] = 10
```

Nel caso precedente, il secondo elemento della lista diventa `10`. Puoi usare anche la sintassi di slicing:

```python
l[1:3] = [20, 30]
```

In questa riga sostituiamo due elementi: il secondo, all'indice `1`, diventa `20`, e il terzo, all'indice `2`, diventa `30`. Se specifichi piu' elementi di quelli sostituiti, i nuovi elementi vengono inseriti nella lista a partire dalla posizione indicata:

```python
l[1:2] = [10, 100, 1000, 2000]
```

Se invece sostituisci piu' elementi con un solo elemento, la lista si accorcia:

```python
l[1:3] = [10]
```

### 05.04. Aggiungere elementi

Per inserire un elemento in una lista puoi usare il metodo `append()`, che aggiunge l'elemento in fondo alla lista:

```python
l = [1, 2, 3]
l.append(4)  # [1, 2, 3, 4]
```

Un altro metodo utile e' `insert()`, che accetta due argomenti:

- il primo e' l'indice, cioe' la posizione in cui vuoi inserire l'elemento,
- il secondo e' l'elemento da inserire.

Gli elementi successivi vengono spostati a destra e la lunghezza della lista aumenta di `1`:

```python
l = [1, 2, 3]
l.insert(2, 10)  # [1, 2, 10, 3]
l.insert(0, 0)  # [0, 1, 2, 10, 3]
```

### 05.05. Rimuovere elementi

Il metodo `remove()` accetta un solo argomento: l'elemento che vuoi rimuovere dalla lista. Se l'elemento compare piu' volte, viene rimossa solo la prima occorrenza:

```python
l = [1, 2, 3, 3]
l.remove(1)  # [2, 3, 3]
l.remove(3)  # [2, 3]
```

Il metodo `pop()` rimuove anch'esso un elemento. Puo' essere usato senza argomenti, in tal caso rimuove l'ultimo elemento, oppure con un indice, nel qual caso rimuove l'elemento in quella posizione:

```python
l = [1, 2, 3]
l.pop()  # [1, 2]
l.pop(0)  # [2]
```

Python fornisce anche la parola chiave `del`, che puo' eliminare un elemento o l'intera lista:

```python
l = [1, 2, 3]
del l[0]  # [2, 3]
del l
```

Dopo `del l`, la lista non esiste piu' nel programma.

### 05.06. Ordinamento

Il metodo `sort()` cambia l'ordine della lista e la ordina alfanumericamente:

```python
l = ["orange", "banana", "kiwi", "apple"]
l.sort()  # ['apple', 'banana', 'kiwi', 'orange']
```

Per default `sort()` ordina in ordine crescente. Se vuoi un ordinamento decrescente, puoi usare il parametro `reverse=True`:

```python
l = ["orange", "banana", "kiwi", "apple"]
l.sort(reverse=True)  # ['orange', 'kiwi', 'banana', 'apple']
```

### 05.07. Copia

Se hai due liste, per esempio `l1 = [1, 2, 3]` e `l2 = ['a', 'b', 'c']`, e scrivi:

```python
l1 = l2
```

non stai creando una vera copia: `l1` e `l2` faranno riferimento alla stessa lista. Di conseguenza, una modifica fatta tramite `l2` sara' visibile anche tramite `l1`, e viceversa.

Se vuoi copiare la lista riferita da `l2` in un'altra area di memoria, puoi usare il metodo `copy()`:

```python
l1 = l2.copy()
l1[1] = 3.15
print(l1)  # ['a', 3.15, 'c']
print(l2)  # ['a', 'b', 'c']
```

Il metodo `copy()` esegue una copia superficiale della lista. Un altro modo per copiare una lista e' passarla alla funzione `list()`:

```python
l1 = list(l2)
```

Un terzo modo per fare una copia superficiale e' usare lo slicing:

```python
l1 = l2[:]
```

### 05.09. Unione

Concatenare due o piu' liste in Python e' semplice usando l'operatore `+`:

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

list1 + list2  # ["a", "b", "c", 1, 2, 3]

list3 = [True, False]
list4 = [0.0, 0.7, 0.3]

list1 + list2 + list3 + list4
```

Un altro modo e' usare il metodo `extend()`, che accetta una lista e aggiunge tutti i suoi elementi alla lista corrente:

```python
l1 = [1, 2, 3]
l2 = ["a", "b", "c"]
l1.extend(l2)  # [1, 2, 3, "a", "b", "c"]
```
