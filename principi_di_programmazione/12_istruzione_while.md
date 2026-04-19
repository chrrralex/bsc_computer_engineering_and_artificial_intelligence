# 12. Istruzione `while`

Il ciclo `while` e' un costrutto iterativo che permette allo sviluppatore di ripetere un blocco di istruzioni finche' una certa condizione risulta `True`. La sintassi del ciclo `while` e' la seguente:

```python
while condition:
    statement1
    statement2
    ...
    statementN
```

L'istruzione `while` e' un ciclo con controllo in testa. Questo significa che il flusso di esecuzione e' il seguente:

1. Per prima cosa, l'interprete Python valuta la condizione.
2. Se la condizione e' `True`, vengono eseguite tutte le istruzioni contenute nel blocco `while`.
3. Se la condizione e' `False`, nessuna istruzione del blocco viene eseguita e il controllo passa alle istruzioni successive.

Per esempio, il seguente snippet stampa `10` in output:

```python
i = 0
while i < 10:
    i += 1
print(i)  # 10
```

Analizziamo le righe precedenti:

1. La prima riga inizializza la variabile `i` con il valore `0`.
2. La seconda riga specifica la condizione `i < 10`.
3. In questo caso, nel corpo del ciclo abbiamo una sola istruzione: `i += 1`. Questa e' chiamata istruzione di passo, perche' incrementa il valore della variabile `i` di `1`.
4. Quando `i` raggiunge il valore `10`, la condizione dopo la parola chiave `while` diventa `False`, quindi il corpo del ciclo non viene piu' eseguito.
5. L'ultima riga stampa il valore della variabile `i`, cioe' `10`.

Puoi usare anche l'istruzione `break`, che e' anch'essa una parola chiave, per uscire permanentemente dal ciclo:

```python
counter = 10
while counter > 0:
    counter -= 1
    if counter == 5:
        break
print(counter)  # 5
```

L'istruzione `break` forza l'uscita dal ciclo. Nel nostro caso abbiamo aggiunto una istruzione `if` dentro il ciclo `while` per controllare se la variabile `counter` e' uguale a `5`: se la condizione e' `True`, viene eseguito `break` e il controllo passa alle istruzioni successive al ciclo.

Il ciclo `while` e' utile principalmente in due casi:

- Se vuoi eseguire una o piu' istruzioni finche' una condizione rimane `True`.
- Se vuoi eseguire una o piu' istruzioni un certo numero di volte.

Nel primo caso puoi usare una **flag**, cioe' una variabile booleana usata nella condizione del `while`. Nel secondo caso puoi usare un **contatore**, cioe' una variabile numerica incrementata o decrementata di un certo passo.

Ecco un esempio di ciclo `while` con variabile flag:

```python
flagVariable = bool(input("Insert a boolean value: "))
while flagVariable:
    print("You've inserted 'True'!")
    flagVariable = bool(input("Insert a boolean value: "))
```

Ecco invece un esempio di ciclo `while` con variabile contatore:

```python
aList = [1, 2, 3, 4, 5]
index = 0
while index < len(aList):
    print(aList[index])
    index += 1
```

Nel codice precedente abbiamo usato il ciclo `while` per iterare sulla lista `aList`, che contiene cinque elementi. La variabile `index` e' un contatore che parte da `0` e arriva fino a `len(aList)`, cioe' `5`. Quando `index` diventa `5`, la condizione del ciclo e' falsa e Python esce dal `while`.
