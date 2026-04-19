# 01. Input e output

Puoi stampare variabili e costanti usando la funzione `print()`:

```python
print(a)  # 10
print(DAYS_OF_WEEK)  # 7
```

La funzione `print()` accetta anche molti altri parametri:

- `sep`: e' il separatore tra gli argomenti passati alla funzione.
- `end`: e' la stringa che conclude la stampa.
- `flush`: e' un valore booleano, `True` oppure `False`, che specifica se il buffer di output deve essere svuotato immediatamente.

`print()` fa parte della PSL, cioe' della *Python Standard Library*. Ecco un esempio:

```python
a, b, c = 100, 10, 1
print(a, b, c, sep=" - ", end=" - This is the end", flush=True)
```

L'output del codice precedente e' il seguente:

```text
100 - 10 - 1 - This is the end
```

Come puoi vedere, la funzione `print()` accetta un numero variabile di argomenti, che possono essere variabili, costanti o entrambi.

Per acquisire dati dall'utente puoi usare la funzione `input()`. Accetta una stringa di prompt e restituisce il valore inserito dall'utente tramite lo standard input, cioe' tipicamente la tastiera:

```python
firstName = input("First name: ")
lastName = input("Last name: ")
```

Mentre `print()` scrive sullo standard output, `input()` legge dallo standard input. Tipicamente lo standard input e' la tastiera, ma puo' anche essere un file o una connessione di rete. Lo standard output si riferisce normalmente alla console o al monitor, ma puo' anch'esso essere reindirizzato verso un file o un'altra destinazione.

I commenti possono essere usati per spiegare il codice Python, renderlo piu' leggibile oppure impedire temporaneamente l'esecuzione di certe istruzioni durante i test. In Python, ogni commento e' introdotto dal carattere `#` ed e' completamente ignorato dall'interprete.

Puoi usare un commento su una singola riga in questo modo:

```python
# This is a comment
print("Hello, World!")
```

Oppure puoi scrivere un commento subito dopo una riga di codice:

```python
print("Hello, World!")  # This is a comment
```

Un commento non deve necessariamente spiegare il codice: puo' anche essere usato per impedire a Python di eseguire una certa istruzione. Ecco un esempio:

```python
# print("Hello, World!")
print("Cheers, Mate!")
```

In Python, quando scrivi codice, puoi commettere due tipi principali di errore:

- **Errore logico**: quando la sintassi del codice e' corretta, ma la funzionalita' implementata e' sbagliata. Per esempio, se scrivi un programma che chiede due numeri all'utente per eseguire una divisione, e l'utente inserisce `0` come secondo numero, si verifica un errore a runtime, cioe' una divisione per zero. Gli errori logici sono piu' difficili da riconoscere e talvolta anche da correggere.
- **Errore di sintassi**: quando la sintassi del codice e' sbagliata e l'interprete Python segnala la regola violata. Gli errori di sintassi sono in genere piu' facili da riconoscere e correggere, ma impediscono l'esecuzione del programma.

Entrambi i tipi di errore sono possibili, anche se sei uno sviluppatore esperto.

Un esempio di errore di sintassi si ha quando dimentichi una parentesi tonda alla fine della funzione `print()`:

```python
print("Hello, World!"  # ERROR! SyntaxError: '(' was never closed
```

Ecco invece un esempio di errore logico o, piu' precisamente, di errore a runtime:

```python
print(10 / 0)  # ERROR! ZeroDivisionError: division by zero
```

La buona notizia e' che gli errori sono fisiologici quando si impara un linguaggio di programmazione. Continuare a esercitarsi e imparare dagli errori fa parte del processo.