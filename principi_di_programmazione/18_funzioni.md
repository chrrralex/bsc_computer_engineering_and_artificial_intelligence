# 18. Funzioni

### 18.01. Che cos'e' una funzione?

Una funzione e' un blocco di codice che puoi isolare ed eseguire in uno o piu' punti del programma. In generale:

- una funzione esegue un compito e puo' restituire un valore,
- una procedura esegue un compito senza restituire un valore.

In Python si usa normalmente il termine funzione per entrambi i casi. Una funzione puo' essere vista come una scatola nera:

- accetta zero, uno o piu' input, chiamati parametri,
- esegue un compito tramite una o piu' istruzioni,
- puo' restituire un risultato oppure terminare senza restituire nulla.

Per esempio, in Python puoi definire una funzione con la parola chiave `def`:

```python
def sum(a, b):
    return a + b
```

La funzione `sum()` accetta due parametri, `a` e `b`, ed esegue una somma. La parola chiave `return` restituisce il risultato dell'espressione.

Puoi invocare la funzione passando gli argomenti in questo modo:

```python
print(sum(10, 20))  # 30
```

### 18.02. Stack e record di attivazione

Lo stack e' una porzione di memoria usata per memorizzare informazioni sulle funzioni chiamate durante l'esecuzione. Lo stack e' una struttura dati di tipo LIFO, cioe' "Last In, First Out": l'ultimo elemento inserito e' il primo a essere rimosso.

Le informazioni associate a una chiamata di funzione prendono il nome di AR (Activation Record) oppure SF (Stack Frame). Un record di attivazione contiene tipicamente:

- gli argomenti passati alla funzione,
- le variabili locali,
- lo spazio per l'eventuale valore di ritorno,
- l'indirizzo a cui il controllo deve tornare,
- il collegamento al record precedente,
- altre informazioni di supporto.

Se hai tre funzioni come queste:

```python
def func1():
    print("Hello!")

def func2(a):
    print(a + 10)

def func3(a, b):
    return a * b
```

quando le invochi, Python aggiunge e rimuove i relativi record dallo stack man mano che le funzioni iniziano e terminano la propria esecuzione. Se una funzione chiama un'altra funzione, sullo stack possono coesistere piu' record, ma in ogni istante solo l'ultimo e' quello attivo.

### 18.03. Firma di una funzione

In Python la firma di una funzione descrive come la funzione e' definita. La firma comprende:

- il nome della funzione,
- i parametri che accetta,
- il tipo di ritorno, se annotato.

Per esempio:

```python
def f():
    print("Hello!")
```

ha firma `f()`, mentre:

```python
def f(a, b):
    print(a + b)
```

ha firma `f(a, b)`.

Un altro esempio, con valore di default:

```python
def greet(name, message="Hello!"):
    print(message, name)
```

ha firma `greet(name, message="Hello!")`.

Se non rispetti la firma di una funzione, puoi ottenere un `TypeError`, per esempio se passi il numero sbagliato di argomenti o nomi di parametri inesistenti.

### 18.04. Definizione di funzione

Una definizione di funzione e' composta da due parti:

- la parola chiave `def` seguita dalla firma,
- il corpo della funzione, cioe' il blocco di istruzioni indentato.

Per esempio:

```python
def sum(a, b):
    result = a + b
    return result
```

`sum` e' il nome della funzione. `a` e `b` sono i parametri formali. `result` e' una variabile locale, visibile solo all'interno della funzione.

### 18.05. Invocazione di funzione

Per invocare una funzione, specifichi il suo nome seguito da parentesi tonde e dagli eventuali argomenti. Per esempio:

```python
sum(10, 5)  # 15
```

Le seguenti chiamate sono scorrette:

```python
sum()  # pochi argomenti
sum(5)  # pochi argomenti
sum(10, 15, 20)  # troppi argomenti
sum(10, "15")  # errore logico
```

Quando chiami una funzione devi sempre rispettare numero, ordine, tipo e nome dei parametri previsti.

### 18.06. Parametri posizionali

Normalmente Python usa parametri posizionali: il valore del primo argomento viene associato al primo parametro, il secondo al secondo, e cosi' via.

```python
def max(a, b, c):
    m = a
    if b > m:
        m = b
    if c > m:
        m = c
    return m

print(max(10, 20, 30))  # 30
```

L'associazione dipende dall'ordine. Se i tipi previsti sono diversi, scambiare gli argomenti puo' causare errori.

### 18.07. Parametri con nome

Un'alternativa comoda ai parametri posizionali sono i parametri con nome, o keyword arguments.

```python
def greet(firstName, lastName):
    print("Hello, " + firstName + " " + lastName + "!")

greet("Christian", "Atzeni")
greet(firstName="Christian", lastName="Atzeni")
```

Con i parametri con nome puoi anche cambiare l'ordine degli argomenti:

```python
greet(lastName="Atzeni", firstName="Christian")
```

Devi pero' evitare di assegnare due volte lo stesso parametro, altrimenti Python genera un `TypeError`.

### 18.08. Parametri con valore di default

Puoi assegnare un valore di default a uno o piu' parametri. In questo caso il parametro diventa opzionale.

```python
def sum(a=0, b=0):
    return a + b
```

La funzione puo' essere chiamata in diversi modi:

```python
sum()  # a = 0, b = 0
sum(10)  # a = 10, b = 0
sum(10, 20)  # a = 10, b = 20
sum(a=10, b=20)
sum(b=20)
```

### 18.09. Mischiare parametri posizionali e con nome

Puoi usare insieme parametri posizionali, keyword arguments e valori di default.

```python
def sum(a=0, b=0):
    return a + b
```

Inoltre, Python permette di definire:

- parametri solo posizionali, usando `/`,
- parametri solo per nome, usando `*`.

Esempio di parametri solo posizionali:

```python
def func(a, b, c, /):
    print(a, b, c)
```

Esempio di parametri solo keyword:

```python
def func(*, a, b, c):
    print(a, b, c)
```

Puoi anche combinarli nella stessa funzione.

### 18.10. `*args`, `**kwargs` e unpacking degli argomenti

Python supporta gli argomenti arbitrari. Con `*args` puoi ricevere un numero variabile di argomenti posizionali:

```python
def printNumbers(*args):
    for n in args:
        print(n)
```

`args` e' una tupla contenente tutti gli argomenti posizionali passati alla funzione.

Con `**kwargs` puoi ricevere un numero variabile di argomenti con nome:

```python
def printNumbers(**kwargs):
    for k, n in kwargs.items():
        print(k + ": " + str(n))
```

`kwargs` e' un dizionario in cui le chiavi sono i nomi dei parametri e i valori sono i valori associati.

Puoi anche usare `*args` e `**kwargs` insieme:

```python
def func(p1, p2, p3, *args, **kwargs):
    pass
```

Python supporta anche l'unpacking degli argomenti. Per esempio, se hai:

```python
l = [1, 2, 3]

def func(a, b, c):
    pass
```

puoi scrivere:

```python
func(*l)
```

Allo stesso modo, con un dizionario:

```python
d = {"a": 1, "b": 2, "c": 3}
func(**d)
```

### 18.11. Metadati delle funzioni

I metadati di una funzione sono informazioni sulla funzione stessa, non sulla sua esecuzione. In Python, ogni funzione possiede attributi come:

- `__name__`: il nome,
- `__doc__`: la docstring,
- `__module__`: il modulo in cui e' stata definita,
- `__defaults__`: i valori di default,
- `__annotations__`: le annotazioni.

Per esempio:

```python
def greet(name: str = "Guest") -> str:
    """Return a greeting message."""
    return f"Hello, {name}!"

print(greet.__name__)
print(greet.__doc__)
print(greet.__module__)
print(greet.__defaults__)
print(greet.__annotations__)
```

### 18.12. Funzioni lambda

Una funzione lambda in Python e' una piccola funzione anonima, cioe' senza nome, definita inline. La sintassi base e':

```python
lambda arguments: expression
```

Per esempio, la seguente funzione:

```python
def add(a, b):
    return a + b
```

puo' essere riscritta come:

```python
add = lambda a, b: a + b
```

Una lambda puo' essere invocata come una normale funzione:

```python
print(add(10, 20))  # 30
```

Le lambda sono comode per operazioni brevi, ma hanno alcune limitazioni: possono contenere una sola espressione e non sono adatte a logiche articolate.

### 18.13. Funzioni ricorsive

Una funzione ricorsiva e' una funzione che chiama se stessa. La ricorsione e' utile quando un problema puo' essere scomposto in sottoproblemi piu' piccoli dello stesso tipo. Ogni funzione ricorsiva ha due parti fondamentali:

- il caso base, che ferma la ricorsione,
- il caso ricorsivo, in cui la funzione chiama se stessa con un problema piu' piccolo.

Un esempio classico e' il fattoriale:

```python
def factorial_recursive(n):
    if n <= 1:
        return 1
    else:
        return n * factorial_recursive(n - 1)
```

La versione iterativa corrispondente e':

```python
def factorial_iterative(n):
    f = 1
    while n >= 1:
        f *= n
        n -= 1
    return f
```

Nel caso ricorsivo, Python usa sempre lo stack per memorizzare le chiamate in sospeso. Quando il caso base viene raggiunto, le chiamate si risolvono in ordine inverso.

### 18.14. Funzioni generatrici e parola chiave `yield`

I generatori sono funzioni che possono sospendere e riprendere la propria esecuzione. Quando una funzione generatrice viene chiamata, restituisce un oggetto generatore, che e' un iteratore. Il codice della funzione non viene eseguito subito: l'esecuzione avviene solo quando il generatore viene iterato.

I generatori usano la parola chiave `yield`, non `return`.

```python
def generator():
    yield 1
    yield 2
    yield 3

for value in generator():
    print(value)
```

Ogni volta che Python incontra `yield`, restituisce un valore e salva lo stato della funzione, che potra' riprendere dal punto successivo.

### 18.15. Variabili globali e locali

Una variabile globale e' definita fuori da qualsiasi funzione, tipicamente all'inizio del file. Una variabile locale e' invece definita all'interno di una funzione o di un blocco.

```python
x = 10

def f1():
    print(x)
```

In questo caso `x` e' globale ed e' visibile dentro `f1()`. Se all'interno di una funzione definisci una variabile con lo stesso nome, la variabile locale oscura quella globale:

```python
x = 10

def f1():
    x = 50
    print(x)

f1()  # 50
print(x)  # 10
```

Python mette a disposizione la parola chiave `global` per riferirti esplicitamente a una variabile globale dall'interno di una funzione:

```python
x = 100

def f1():
    global x
    x = 200

f1()
print(x)  # 200
```

Le variabili definite nell'intestazione di un ciclo `for` sono anch'esse variabili locali al relativo contesto.
