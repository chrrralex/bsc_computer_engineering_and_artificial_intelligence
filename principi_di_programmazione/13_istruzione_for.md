# 13. Istruzione `for`

Il ciclo `for` e' un costrutto iterativo che permette allo sviluppatore di iterare su una sequenza o su un qualunque oggetto iterabile finche' esso contiene elementi. La sintassi del ciclo `for` e' la seguente:

```python
for variable in iterable:
    statement1
    statement2
    ...
    statementN
```

L'istruzione `for` e' un ciclo con controllo in testa. Questo significa che il flusso di esecuzione e' il seguente:

1. Per prima cosa, l'interprete Python verifica se l'iterabile contiene almeno un elemento.
2. Se la risposta e' positiva, esegue il blocco del `for` e la variabile assume il valore dell'elemento corrente estratto dall'iterabile.
3. Se l'iterabile non contiene elementi, nessuna istruzione del blocco viene eseguita e il controllo passa alle istruzioni successive.

Per esempio, il seguente snippet esegue tutte le istruzioni del blocco `for` per ciascun elemento della lista `aList`:

```python
aList = ["a", "b", "c"]
for c in aList:
    print(c.upper())
```

Come puoi vedere, non e' richiesta alcuna variabile contatore o flag: il ciclo `for` gestisce l'iterabile in modo automatico. Analizziamo le righe precedenti:

1. La prima riga inizializza una lista di tre stringhe: `"a"`, `"b"` e `"c"`.
2. La seconda riga specifica l'intestazione del `for`: l'espressione `c in aList` indica che, finche' `aList` contiene elementi, il corpo del ciclo verra' eseguito e la variabile `c` assumera' a turno il valore dei vari elementi.
3. Quando l'iterabile, in questo caso `aList`, non ha piu' elementi da fornire, il controllo passa oltre il ciclo `for`.

Puoi usare anche l'istruzione `break`, come gia' visto per il ciclo `while`, per uscire definitivamente dal ciclo:

```python
aList = ["a", "b", "c", "d", "e", "f"]
for c in aList:
    print(c.upper())
    if c == "b":
        break
```

L'istruzione `break` provoca l'uscita immediata dal ciclo. Nel nostro caso abbiamo aggiunto una istruzione `if` all'interno del `for` per controllare se la variabile `c` e' uguale alla stringa `"b"`: se la condizione e' `True`, viene eseguito `break` e il controllo passa alle istruzioni successive al ciclo.

Il ciclo `for` e' molto utile per iterare su un iterabile o su una sequenza. In Python, esempi di tipi iterabili sono le liste e le tuple. Puoi usare il ciclo `for` con una tupla in questo modo:

```python
t = (1, 2, 3, 4, 5)
for element in t:
    print(element)
```

Un'altra parola chiave usata nei cicli e' `continue`. Questa istruzione fa saltare immediatamente all'iterazione successiva, senza eseguire le istruzioni rimanenti del corpo del ciclo. Per esempio, nel seguente codice vengono saltate le iterazioni in cui `element` vale `2` oppure `4`:

```python
t = (1, 2, 3, 4, 5)
for element in t:
    if element == 2 or element == 4:
        continue
    print(element)
```

I cicli possono essere usati anche con la funzione `range()`, una funzione built-in che restituisce una sequenza di numeri tra un valore minimo `min` e un valore massimo `max`, con un certo passo `step`. Il tipo restituito da `range()` si chiama `range` ed e' un tipo built-in del linguaggio Python. La funzione `range()` accetta tre argomenti:

```python
range(min, max, step)
```

- `min` e' il valore minimo, o valore iniziale, della sequenza. Se non e' specificato, il valore di default e' `0`.
- `max` e' il valore massimo, o valore finale, della sequenza. E' sempre richiesto.
- `step` e' il passo tra due valori consecutivi. Se non e' specificato, il valore di default e' `1`.

Vediamo alcuni esempi. Usa `range()` per ottenere una sequenza tra un valore minimo e un valore massimo:

```python
for n in range(0, 4):  # equivalente a range(4)
    print(n)  # 0, 1, 2, 3
```

Usa `range()` per ottenere una sequenza con un `step` personalizzato:

```python
for n in range(0, 5, 2):
    print(n)  # 0, 2, 4
```

Usa `range()` per ottenere una sequenza con un `step` personalizzato e negativo:

```python
for n in range(10, 0, -1):
    print(n)  # 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

Nota che se usi `range()` con un solo argomento, quell'argomento viene interpretato come valore massimo. Se usi `range()` con due argomenti, il primo e' il valore minimo e il secondo e' il valore massimo. Infine, se usi `range()` con tre argomenti, il terzo rappresenta il passo.
