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
<!-- to do -->