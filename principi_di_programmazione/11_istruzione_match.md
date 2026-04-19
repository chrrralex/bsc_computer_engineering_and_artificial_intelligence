# 11. Istruzione `match`

L'istruzione `match` e' un'istruzione di selezione multipla, molto simile alla `switch` proposta da molti altri linguaggi di programmazione, come C, C++, Java e PHP.

L'istruzione `match` ha la seguente sintassi:

```python
match expression:
    case value1:
        statement1
        statement2
        ...
        statementN
    case value2:
        statement1
        statement2
        ...
        statementN
    ...
    case valueN:
        statement1
        statement2
        ...
        statementN
```

Dopo la parola chiave `match` c'e' un'espressione. Questa espressione puo' essere valutata, per esempio, come intero, booleano oppure stringa. All'interno del blocco `match` ci sono molte clausole `case`: ciascuna clausola specifica, dopo la parola chiave `case`, un valore da confrontare con `expression`. All'interno di ogni blocco `case` ci sono una o piu' istruzioni. L'interprete Python prima valuta `expression`; poi confronta il risultato con ciascun valore specificato dopo ogni `case`; infine esegue il blocco associato al primo valore che corrisponde all'espressione.

```python
a = 10
match a + 10:
    case 10:
        print("expression is 10")
    case 20:
        print("expression is 20")
    case 30:
        print("expression is 30")
```

Lo snippet precedente produce il seguente output:

```text
expression is 20
```

Se hai bisogno di eseguire una o piu' azioni nel caso in cui non ci sia alcuna corrispondenza, puoi usare il carattere underscore `_`, che rappresenta il caso di default:

```python
a = 10
b = 50 + a
match b:
    case 10:
        print("expression is 10")
    case 20:
        print("expression is 20")
    case 30:
        print("expression is 30")
    case _:
        print("b is", b)
```

Il codice precedente produce in output la stringa `"b is 60"`, perche' il valore `60`, cioe' `50 + a`, non corrisponde a nessuno dei valori specificati nei vari `case`.

L'istruzione `match` permette anche di combinare piu' valori grazie all'operatore pipe `|`:

```python
day = 4
match day:
    case 1 | 2 | 3 | 4 | 5:
        print("Today is a weekday")
    case 6 | 7:
        print("Happy weekend!")
```

Nel codice precedente, se il valore di `day` e' `1`, `2`, `3`, `4` oppure `5`, viene eseguita la prima clausola `case` e l'output del programma e' `"Today is a weekday"`; se invece il valore e' `6` oppure `7`, viene eseguita la seconda clausola e l'output e' `"Happy weekend!"`.
