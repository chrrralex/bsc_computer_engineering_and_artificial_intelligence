# 23. Introduzione alle strutture dati

Le strutture dati sono modi organizzati di memorizzare e gestire i dati, in modo che possano essere accessibili e modificabili in maniera efficiente. Scegliere la struttura dati corretta influisce su prestazioni, chiarezza del codice e uso della memoria. In Python, le strutture dati built-in piu' comuni sono liste, tuple, insiemi e dizionari, ciascuna progettata per casi d'uso differenti.

A un livello generale, le strutture dati possono essere:

- **Lineari**: gli elementi sono disposti in sequenza, come nel caso di liste e tuple.
- **Non lineari**: gli elementi hanno relazioni gerarchiche o associative, come nel caso di alberi, grafi e, in senso piu' ampio, dizionari.

Le operazioni tipiche includono:

- accesso agli elementi,
- inserimento o rimozione di elementi,
- ricerca di un valore,
- iterazione su tutti gli elementi.

Strutture diverse offrono compromessi diversi in termini di tempo e spazio. Per esempio, le liste sono ottime per collezioni ordinate, i set sono ottimizzati per i controlli di appartenenza, e i dizionari associano chiavi a valori permettendo ricerche molto rapide. Nelle sezioni successive vedremo queste strutture e capiremo quando usarle.

Un **array** memorizza elementi dello stesso tipo di dato in modo compatto ed efficiente. Questo e' utile quando hai bisogno di dati numerici e vuoi un uso della memoria piu' prevedibile. L'esempio seguente crea un array di interi, aggiunge un valore e accede a un elemento tramite indice:

```python
from array import array

numbers = array("i", [10, 20, 30])
numbers.append(40)
print(numbers[1])  # 20
```

Una **lista** e' il tipo di sequenza piu' flessibile di Python e puo' contenere anche tipi di dato misti. Supporta crescita dinamica e accesso diretto per indice. L'esempio seguente aggiunge un nuovo elemento e legge il primo elemento:

```python
items = ["apple", "banana", "cherry"]
items.append("date")
print(items[0])  # apple
```

Una **coda** elabora gli elementi secondo l'ordine *first-in, first-out*. `collections.deque` e' efficiente per aggiungere e rimuovere elementi da entrambe le estremita'. L'esempio seguente inserisce in coda due nomi e poi estrae il primo. La queue e' una struttura dati basata sull'acronimo FIFO, *First In, First Out*:

```python
from collections import deque

queue = deque()
queue.append("Alice")
queue.append("Bob")
first = queue.popleft()
print(first)  # Alice
```

Uno **stack** elabora gli elementi secondo l'ordine *last-in, first-out*. Una lista Python puo' funzionare come stack usando `append()` per inserire e `pop()` per rimuovere l'elemento in cima. L'esempio seguente inserisce due valori e rimuove quello inserito per ultimo. Lo stack e' una struttura dati basata sull'acronimo LIFO, *Last In, First Out*:

```python
stack = []
stack.append(1)
stack.append(2)
top = stack.pop()
print(top)  # 2
```
