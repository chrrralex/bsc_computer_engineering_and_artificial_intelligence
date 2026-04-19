# 08. Operatori

### 08.01. Panoramica

Un operatore e' un simbolo che specifica un'operazione tra una, due o piu' variabili, letterali o altre entita'.

Un operatore puo' essere:

- unario, se opera su un solo operando,
- binario, se opera su due operandi,
- ternario, se opera su tre operandi.

Python mette a disposizione diversi tipi di operatori:

- aritmetici,
- di assegnazione,
- logici,
- di confronto,
- di identita',
- bitwise,
- di appartenenza.

In questo capitolo li esamineremo uno per uno.

### 08.02. Operatori aritmetici

`+` e' l'operatore di somma. E' binario ed e' associativo da sinistra a destra:

```python
a = 10
b = 5
c = a + b
print(c) # 15
print(a + b + c + 10) # 25
```

`-` e' l'operatore di differenza. E' binario ed e' associativo da sinistra a destra:

```python
a = 10
b = 5
c = a - b
print(c) # 5
print(a - b - c) # 0
```

`*` e' l'operatore di prodotto. E' binario ed e' associativo da sinistra a destra:

```python
a = 2
b = 3
c = a * b
print(c) # 6
print(a * c * 10) # 120
```

`/` e' l'operatore di divisione floating-point. E' binario ed e' associativo da sinistra a destra:

```python
a = 10.0
b = 5.0
c = a / b
print(c) # 2.0
print(a / b / c) # 1.0
```

Devi fare attenzione al secondo operando della divisione, perche' non puo' essere `0`. Se il secondo operando vale `0`, l'interprete Python genera il seguente errore:

```python
print(10 / 0)
# ERROR!
# Traceback (most recent call last):
#   File "<main.py>", line 6, in <module>
# ZeroDivisionError: division by zero
```

In Python esiste anche un altro modo di dividere due numeri: l'operatore di divisione intera `//`:

```python
a = 10.0
b = 6.7
c = a // b
print(c) # 1.0
```

Il risultato di un'espressione come `operand1 // operand2` e' sempre un intero oppure un floating-point senza cifre decimali significative.

`**` e' l'operatore di elevamento a potenza. E' binario:

```python
a = 2
b = 3
c = a ** b
print(c) # 2^3 = 2 * 2 * 2 = 8
```

`%` e' l'operatore modulo. E' binario e restituisce il resto della divisione `operand1 / operand2`:

```python
a = 10.5
b = 5.2
c = a % b
print(c) # 0.5
```

### 08.03. Operatori di assegnazione

`=` e' l'operatore di assegnazione e assegna il valore a destra alla variabile a sinistra. Questa operazione sovrascrive l'eventuale valore precedente, per questo viene detta distruttiva.

```python
a = 10
b = "A string"
print(a) # 10
a = b
print(a) # "A string"
```

Esistono poi diversi operatori di assegnazione composta, che combinano `=` con un altro operatore aritmetico o bitwise:

- `a += b`: shortcut of `a = a + b`.
- `a -= b`: shortcut of `a = a - b`.
- `a *= b`: shortcut of `a = a * b`.
- `a /= b`: shortcut of `a = a / b`.
- `a %= b`: shortcut of `a = a % b`.
- `a //= b`: shortcut of `a = a // b`.
- `a **= b`: shortcut of `a = a ** b`.
- `a &= b`: shortcut of `a = a & b`.
- `a |= b`: shortcut of `a = a | b`.
- `a ^= b`: shortcut of `a = a ^ b`.
- `a >>= b`: shortcut of `a = a >> b`.
- `a <<= b`: shortcut of `a = a << b`.

### 08.04. Operatori logici

`and` e' l'operatore AND logico. E' binario e restituisce `True` se e solo se entrambi gli operandi sono `True`; altrimenti restituisce `False`.

```python
print(True and True) # True
print(True and False) # False
print(False and True) # False
print(False and False) # False
```

`or` e' l'operatore OR logico. E' binario e restituisce `True` se almeno uno dei due operandi e' `True`; altrimenti restituisce `False`.

```python
print(True or True) # True
print(True or False) # True
print(False or True) # True
print(False or False) # False
```

`not` e' l'operatore NOT logico. E' unario e restituisce `True` se l'operando e' `False`; altrimenti restituisce `False`.

```python
print(not False) # True
print(not True) # False
```

Tutti questi operatori logici restituiscono un valore booleano. Spesso vengono usati per costruire espressioni booleane piu' complesse:

```python
a = 10
c = 1000
print(a < 100 and c * 2 >= 1000) # True
```

### 08.05. Operatori di confronto

`==` e' l'operatore di uguaglianza e restituisce `True` se l'operando sinistro e' uguale a quello destro.

```python
print(10 == 2) # False
print(10 == 10) # True
```

`!=` e' l'operatore di disuguaglianza e restituisce `True` se l'operando sinistro e' diverso da quello destro.

```python
print(10 != 2) # True
print(10 != 10) # False
```

`>` e' l'operatore maggiore di e restituisce `True` se l'operando sinistro e' maggiore di quello destro.

```python
print(10 > 2) # True
print(10 > 10) # False
```

`<` e' l'operatore minore di e restituisce `True` se l'operando sinistro e' minore di quello destro.

```python
print(10 < 100) # True
print(10 < 10) # False
```

`>=` e' l'operatore maggiore o uguale e restituisce `True` se l'operando sinistro e' maggiore o uguale a quello destro.

```python
print(10 >= 10) # True
print(10 >= 100) # False
```

`<=` e' l'operatore minore o uguale e restituisce `True` se l'operando sinistro e' minore o uguale a quello destro.

```python
print(10 <= 10) # True
print(10 <= 5) # False
```

### 08.06. Operatori di identita'

L'operatore `is` restituisce `True` se entrambi gli operandi fanno riferimento allo stesso oggetto:

```python
a = 10
b = 10
c = 10.0
print(a is b) # True
print(a is c) # False, cause c is a floating-point number and a is an integer number
```

L'operatore `is not` restituisce `True` se gli operandi fanno riferimento a oggetti diversi:

```python
a = 10
b = 10
c = 10.0
print(a is not b) # False
print(a is not c) # True, cause c is a floating-point number and a is an integer number
```

### 08.07. Operatori bitwise

Gli operatori bitwise lavorano a livello di bit. Sono:

- `a & b`: AND bitwise, imposta il bit a `1` solo se entrambi i bit corrispondenti sono `1`,
- `a | b`: OR bitwise, imposta il bit a `1` se almeno uno dei bit corrispondenti e' `1`,
- `~a`: NOT bitwise, calcola il complemento a uno,
- `a ^ b`: XOR bitwise, imposta il bit a `1` se i bit corrispondenti sono diversi.

Ecco un esempio:

```python
a = 10          # 1010
b = 5           # 0101

print(a & b)    # 1010 &
                # 0101 =
                # 0000

print(a | b)    # 1010 |
                # 0101 =
                # 1111

print(a ^ b)    # 1010 ^
                # 0101 =
                # 1111

print(~a)       # ~1010 =
                # 0101
```

L'operatore `<<` e' lo shift a sinistra con riempimento di zeri, mentre `>>` e' lo shift a destra. Entrambi sono operatori binari. `<<` sposta i bit verso sinistra inserendo zeri da destra; `>>` sposta i bit verso destra. Ecco un esempio:

```python
a = 10          # 1010
print(a << 3)   # 10 << 3 = 10 * 2^3 = 80

a = 80          # 1010000
print(a >> 3)   # 80 >> 3 = 80 / 2^3 = 10
```

Nota che `>>` e' equivalente, in molti casi, al quoziente tra `a` e `2^p`, dove `p` e' il secondo operando di `>>`.
Nota che `<<` e' equivalente, in molti casi, al prodotto tra `a` e `2^p`, dove `p` e' il secondo operando di `<<`.

### 08.08. Operatori di appartenenza

Abbiamo gia' incontrato gli operatori di appartenenza `in` e `not in`. Funzionano con tuple, liste, stringhe, dizionari e altri iterabili, e restituiscono un valore booleano.

`in` restituisce `True` se l'elemento specificato come operando sinistro e' presente nell'oggetto specificato come operando destro:

```python
l = [ 1, 2, 3 ]
1 in l # True
10 in l # False
```

`not in` restituisce `True` se l'elemento specificato come operando sinistro non e' presente nell'oggetto specificato come operando destro:

```python
l = [ 1, 2, 3 ]
1 not in l # False
10 not in l # True
```
