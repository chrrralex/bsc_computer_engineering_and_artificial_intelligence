# 16. Istruzione `try-except`

### 16.01. Panoramica

Come altri linguaggi di programmazione, per esempio PHP e Java, Python include un costrutto per la gestione degli errori chiamato `try-except-finally`. Vedremo la forma base di questo costrutto e, progressivamente, analizzeremo le clausole che si possono usare con questa importante istruzione.

Normalmente, quando si verifica un errore durante l'esecuzione del programma, l'interprete Python lo segnala e termina il programma. Grazie al blocco `try-except-finally`, puoi intercettare uno o piu' tipi di errore ed eseguire codice specifico per gestirli, correggerli o seguire un altro percorso di esecuzione.

Partiamo dalla forma base del blocco `try-except-finally`. Dopo la parola chiave `try` ci sono le istruzioni che potrebbero generare uno o piu' errori. Dopo `except` ci sono le istruzioni usate per gestire l'errore intercettato:

```python
try:
    # statements could throw one, or more errors
    print(x) # This is an error: x isn't declared
except:
    # statement used to catch one, or more errors
    print("An error occurred")
```

La seguente riga:

```python
print(x)
```

prova a stampare la variabile `x`, ma la variabile non e' stata dichiarata nello script. Quando l'interprete esegue questa riga, viene generato un errore. Tuttavia la riga si trova dentro un blocco `try-except`, quindi la clausola `except` intercetta l'errore e viene eseguito il codice di gestione.

```python
print("An error occurred")
```

Puoi usare piu' di una clausola `except` per intercettare errori diversi. Per esempio, il seguente frammento stampa `"Variable x is not defined"` se viene sollevato un `NameError`:

```python
try:
    print(x) # This is an error: x isn't declared
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
```

### 16.02. Clausole di `try-except-finally`

Puoi usare la clausola `else`. Le istruzioni al suo interno vengono eseguite solo se non si e' verificato alcun errore:

```python
try:
    print(10) # Ok, no error here!
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
else:
    print("No error!")
```

Il codice precedente stampa `"No error!"` perche' `print(10)` non genera alcun errore. La clausola `else` e' opzionale.

Un'altra clausola utile e' `finally`. Se specificata, viene eseguita comunque, sia che il blocco `try` generi un errore sia che non lo generi. In pratica viene eseguita alla fine del flusso di gestione.

```python
try:
    print(x) # This is an error: x isn't declared
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
else:
    print("No error!")
finally:
    print("Executed anyway")
```

Il frammento precedente stampa sullo standard output le seguenti stringhe:

```python
Variable x is not defined
Executed anyway
```

Come sviluppatore Python puoi anche decidere di sollevare un errore quando si verifica una certa condizione. Per farlo usi la parola chiave `raise`:

```python
x = -1
if x < 0:
  raise Exception("Sorry, no numbers below zero")
```

La parola chiave `raise` viene usata per sollevare un'eccezione. Puoi definire sia il tipo di errore sia il messaggio associato:

```python
x = "hello"
if x != 10:
  raise TypeError("x != 10")
```

### 16.03. Eccezioni ed errori

Durante l'esecuzione di un programma possono verificarsi, in generale, due tipi di situazioni:

- Errore: un problema che si verifica durante l'esecuzione e causa il fallimento del programma.
- Eccezione: un problema che si verifica durante l'esecuzione e che puo' essere gestito dal codice o dall'utente.

Mentre gli errori possono bloccare il programma, le eccezioni possono spesso essere gestite, per esempio con `try-except-finally`. Un esempio comune e' `ZeroDivisionError`, che si verifica quando nel codice compare una divisione per `0`, come `10 / 0`.

### 16.04. Gerarchia delle eccezioni in Python

La gerarchia delle eccezioni e' l'albero di tutte le eccezioni built-in di Python. Tutte ereditano dalla classe base `BaseException`, che e' il genitore comune di errori ed eccezioni. Tra i figli piu' comuni di `BaseException` troviamo:

- `Exception`: is the base class of the most common user-level errors. It has so many children, classes like `ArithmeticError` and `LookupError`.
- `GeneratorExit`: raised when a generator is closed (e.g., when `close()` is called or it is garbage collected).
- `KeyboardInterrupt`: raised when the user interrupts program execution, usually by pressing Ctrl+C, or Ctrl+Z.
- `SystemExit`: raised when the program exits, typically via `sys.exit()`.

### 16.05. Definire e sollevare una propria eccezione

Puoi definire una tua eccezione personalizzata sfruttando la programmazione a oggetti. In Python e' sufficiente creare una classe che estenda `Exception`. Per esempio:

```python
class MyCustomError(Exception):
    pass
```

Successivamente, magari in un'altra parte del programma o dentro una funzione, puoi sollevare questa eccezione con `raise`:

```python
raise MyCustomError("Something went wrong")
```

Puoi poi intercettarla con `try-except-finally`:

```python
try:
    raise MyCustomError()
except MyCustomError as error:
    print(error)
else:
    print("No error occurred")
finally:
    print("That's it!")
```

Il codice precedente stampa le seguenti due righe:

```bash
Something went wrong
That's it!
```

### 16.06. Accedere ai dati dell'eccezione

Nel frammento precedente abbiamo usato una forma particolare della clausola `except`, con questa sintassi:

```python
except ExceptionName as identifier:
```

dove:

- `ExceptionName` is the name of the exception type (`ZeroDivisionError`, or `TypeError`, or `IndexError`, or other).
- `identifier` is the object that represents the data about the raised exception.

Questa forma della clausola `except` ti permette di accedere ai dati dell'eccezione. Puoi catturare i dettagli usando la parola chiave `as`:

```python
try:
    x = int("abc")
except ValueError as error:
    print(error) # invalid literal for int() with base 10: 'abc'
```

Puoi usare `str(error)` per ottenere una descrizione leggibile dell'errore. `repr(error)` fornisce una rappresentazione piu' dettagliata. Un attributo particolarmente utile e' `error.args`, una tupla contenente tutti gli argomenti passati all'eccezione:

```python
try:
    x = int("abc")
except ValueError as error:
    print(error.args) # ("invalid literal for int() with base 10: 'abc'",)
```

Puoi usare `error.args` anche con una eccezione personalizzata:

```python
class MyCustomError(Exception):
    pass

try:
    raise MyCustomError("Hello!", 1, 3.15, True)
except MyCustomError as error:
    print(error.args) # ('Hello!', 1, 3.15, True)
```

Nota che tutti gli argomenti vengono passati tra parentesi tonde nel punto in cui sollevi l'eccezione.
