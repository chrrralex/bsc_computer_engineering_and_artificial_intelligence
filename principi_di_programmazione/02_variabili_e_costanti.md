# 02. Variabili e costanti

Una variabile e' un'area di memoria con un identificatore e un valore. L'identificatore e' una stringa che puoi usare per riferirti alla variabile senza conoscere nulla della struttura fisica della memoria. Una variabile puo' essere vista come una coppia chiave-valore in cui il valore puo' cambiare durante l'esecuzione del programma.

Puoi dichiarare una variabile usando l'operatore di assegnazione `=`:

```python
aNumber = 10
aString = "This is a string"
```

Una costante e' un'area di memoria con un identificatore e un valore che, per convenzione, non dovrebbe cambiare durante l'esecuzione del programma. Anche qui l'identificatore e' una stringa usata per riferirsi al dato senza conoscere dettagli sulla memoria. Python non ha una vera parola chiave per dichiarare una costante, ma e' una buona pratica usare lettere maiuscole per gli identificatori delle costanti:

```python
PI = 3.1415
DAYS_OF_WEEK = 7
```

Puoi dichiarare piu' variabili, ciascuna con il proprio valore, usando la seguente sintassi:

```python
a, b = 10, 5
```

La variabile `a` vale `10` e la variabile `b` vale `5`. Puoi usare la stessa sintassi anche per le costanti, ricordando pero' di usare lettere maiuscole invece che minuscole:

```python
PI, DAYS_OF_WEEK = 3.1415, 7
```