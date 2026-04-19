# 09. Espressioni

In questo capitolo vedremo una serie di espressioni, progressivamente piu' complesse, per capire la precedenza degli operatori.

Esempio 1: una semplice operazione aritmetica, cioe' una somma. Questa e' una delle espressioni piu' semplici che puoi scrivere in Python: un operatore con due operandi.

```python
10 + 5
# Step 1: 10 + 5 =
# Result: 15
```

Esempio 2: uso di piu' operatori aritmetici. L'operatore `*` ha precedenza piu' alta di `+` e `-`. Analogamente, `/` ha precedenza piu' alta di `+` e `-`.

```python
10 + 5 * 3
# Step 1: 10 + (5 * 3) =
# Step 2: 10 + 15 =
# Result: 25

10 + 20 / 5 / 2 * 3
# Step 1: 10 + (20 / 5) / 2 * 3 =
# Step 2: 10 + (4 / 2) * 3 =
# Step 3: 10 + (2 * 3) =
# Step 4: 10 + 6 =
# Result: 16.0
```

Esempio 3: un'espressione con operatori aritmetici e di confronto. Gli operatori aritmetici hanno precedenza piu' alta degli operatori di confronto, come `>` o `>=`.

```python
10 * 5 - 2 >= 10 + 9 / 3
# Step 1: (10 * 5) - 2 >= 10 + (9 / 3) =
# Step 2: (50 - 2) >= (10 + 3.0) =
# Step 3: 48.0 >= 13.0 =
# Step 4: True
```

Esempio 4: un'espressione con operatori aritmetici, di confronto e booleani. Gli operatori booleani hanno precedenza piu' bassa rispetto agli operatori di confronto, che a loro volta hanno precedenza piu' bassa rispetto agli operatori aritmetici.

```python
a = 15
10 + 5 > 3 and 15 == a
# Step 1: (10 + 5) > 3 and (15 == a)
# Step 2: (15 > 3) and True
# Step 3: True and True
# Result: True
```

Segue la tabella di precedenza degli operatori del linguaggio Python:

| Precedenza | Operatori | Descrizione |
|---|---|---|
| 1 | `()` `[]` `{}` | Raggruppamento, accesso a indice, slicing, literal |
| 2 | `x.attribute` | Accesso ad attributo |
| 3 | `f(...)` | Chiamata di funzione |
| 4 | `await x` | Await expression |
| 5 | `**` | Potenza |
| 6 | `+x` `-x` `~x` | Operatori unari (positivo, negativo, bitwise NOT) |
| 7 | `*` `@` `/` `//` `%` | Moltiplicazione, matrix multiplication, divisione, floor division, modulo |
| 8 | `+` `-` | Addizione e sottrazione |
| 9 | `<<` `>>` | Shift bitwise |
| 10 | `&` | AND bitwise |
| 11 | `^` | XOR bitwise |
| 12 | `\|` | OR bitwise |
| 13 | `in` `not in` `is` `is not` `<` `<=` `>` `>=` `!=` `==` | Operatori di confronto |
| 14 | `not x` | NOT logico |
| 15 | `and` | AND logico |
| 16 | `or` | OR logico |
| 17 | `if ... else ...` | Espressione condizionale (ternaria) |
| 18 | `lambda` | Espressione lambda |
| 19 | `:=` | Walrus operator (assegnazione in espressione) |
