# 10. Istruzione `if`

L'istruzione `if` e' un'istruzione di selezione che permette allo sviluppatore di specificare una condizione booleana, come `a == b` oppure `a >= 10`, e, in base al valore restituito, l'interprete Python esegue una o piu' istruzioni. Una condizione booleana e' un'espressione che puo' essere valutata come `True` oppure `False`.

```python
a = 10
if a > 10:
    print("a > 10")
```

Diversamente da altri linguaggi di programmazione, in Python le condizioni booleane dell'istruzione `if` non sono racchiuse tra parentesi tonde: subito dopo l'espressione compare invece il carattere `:`. In Python l'indentazione e' molto importante, perche' e' proprio grazie all'indentazione che l'interprete riconosce i blocchi di codice. Lo snippet precedente mostra un blocco `if` con una sola istruzione: `print("a > 10")`. Se la condizione e' `True`, vengono eseguite le istruzioni interne al blocco `if`; se la condizione e' `False`, l'interprete passa oltre e ignora quel blocco.

Si noti che Python non usa il punto e virgola `;` per terminare le istruzioni, come avviene in altri linguaggi. Nella maggior parte dei casi il terminatore di istruzione e' semplicemente il cambio di riga.

Puoi usare la parola chiave `else` per completare l'istruzione `if`, ottenendo una struttura `if...else`:

```python
a = 10
if a >= 20:
    print("a >= 20")
else:
    print("a < 20")
```

Lo snippet precedente stampa `"a < 20"`, perche' la variabile `a` ha un valore minore del letterale intero `20` usato nella condizione. La clausola `if` e la clausola `else` sono mutuamente esclusive: ne viene eseguita solo una. Se la condizione e' `True`, viene eseguito il blocco `if`; se la condizione e' `False`, viene eseguito il blocco `else`.

Esiste poi una terza clausola molto importante che puoi usare con `if`: la clausola `elif`. Puoi specificarne quante ne vuoi, in base al problema che stai cercando di risolvere:

```python
a = 87
if a <= 30:
    print("Level 1")
elif a <= 60:
    print("Level 2")
elif a <= 90:
    print("Level 3")
else:
    print("Level 4")
```

Nel codice precedente viene eseguita la terza clausola `elif`, perche' il valore della variabile `a` e' minore o uguale a `90`, infatti vale `87`. Questa struttura e' spesso chiamata `if...elif...else`, ma ricorda che la clausola `else` resta sempre facoltativa.

Python fornisce anche una sintassi molto elegante chiamata **shorthand if**, che permette di scrivere un'intera selezione in una sola riga. La sintassi e' la seguente:

```python
stmtIfTrue if condition else stmtIfFalse
```

Se `condition` e' `True`, viene eseguito solo `stmtIfTrue`; se e' `False`, viene eseguito solo `stmtIfFalse`. Ecco un esempio:

```python
a = 300
b = 150
print("a >= b") if a > b else print("b >= a")
```

Puoi usare questa sintassi compatta anche per assegnare un valore a una variabile:

```python
a = 10
b = 20
bigger = a if a > b else b
print("Bigger is", bigger)
```