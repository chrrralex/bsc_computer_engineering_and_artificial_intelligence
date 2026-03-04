# 09. Expressions

In this chapter we're going to see a serie of expression, progressively more difficult, to understand the operator precedence.

Example #1: a simple arithmetic operation (a sum). This is one of the simplest expressions you can write in Python: an operator with two operands.

```python
10 + 5
# Step 1: 10 + 5 =
# Result: 15
```

Example #2: using more arithmetic operators. `*` operator has an higher precedence than `+` and `-` operators. Both `+` and `*` operators are associative from left to right. Similarly, `/` operator has an higher precedence than `+` and `-`. Both `/` and `-` are associative from left to right.

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

Example #3: an expression with comparison and arithmetic operators. Airthmetic operators have higher precedence than the comparison operators (like `>`, or `>=`).

```python
10 * 5 - 2 >= 10 + 9 / 3
# Step 1: (10 * 5) - 2 >= 10 + (9 / 3) =
# Step 2: (50 - 2) >= (10 + 3.0) =
# Step 3: 48.0 >= 13.0 =
# Step 4: True
```

Example #4: an expression with comparison, arithmetic and boolean operators. Boolean operators have a lower precedence than the comparison operators and comparison operators have a lower precedence than the arithmetic operators.

```python
a = 15
10 + 5 > 3 and 15 == a
# Step 1: (10 + 5) > 3 and (15 == a)
# Step 2: (15 > 3) and True
# Step 3: True and True
# Result: True
```

Here's the precedence table of all the operators of the Python language programming:

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
