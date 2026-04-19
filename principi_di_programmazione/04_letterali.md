# 04. Letterali

Un letterale e' un valore scritto direttamente nel codice sorgente. Ogni letterale ha un proprio tipo. Per esempio, `10` e' un letterale intero, mentre `"Hi!"` e' un letterale stringa.

Un **letterale intero** e' un valore intero. Il tipo `int` permette sia numeri positivi sia numeri negativi nel linguaggio Python:

```python
x = 100
y = +100  # numero positivo, con + opzionale
z = -7  # numero negativo, con - obbligatorio
```

Un **letterale floating-point** e' un valore in virgola mobile. Il tipo `float` permette sia numeri positivi sia numeri negativi:

```python
x = 10.5
y = 10.0  # la parte decimale puo' essere omessa
z = 0.5  # la parte intera puo' essere omessa nello scritto .5
```

Python memorizza i valori floating-point secondo lo standard IEEE 754:

- Un numero in singola precisione ha 32 bit: 23 per la mantissa, 1 per il segno, 8 per l'esponente.
- Un numero in doppia precisione ha 64 bit: 52 per la mantissa, 1 per il segno, 11 per l'esponente.
- Un numero in quadrupla precisione ha 128 bit: 112 per la mantissa, 1 per il segno, 15 per l'esponente.

Puoi specificare letterali floating-point anche in notazione esponenziale, o scientifica:

```python
10.5E3  # con E maiuscola
10.5e3  # con e minuscola
.5e2  # senza parte intera
10.e7  # senza parte decimale esplicita
```

Nei numeri, soprattutto quelli lunghi, puoi usare l'underscore `_` per rendere il codice piu' leggibile:

```python
1_000
1_500_000
10_000.10_23_24
```

Python supporta anche i **numeri complessi**. Un numero complesso e' un numero con una parte reale e una parte immaginaria. La parte immaginaria termina sempre con `j`:

```python
10 + 5j
10.5 + 2.7j
.2 + .5j
```

Un **letterale stringa** e' una sequenza di caratteri scritta direttamente nel codice. Una stringa puo' essere racchiusa tra doppi apici oppure tra apici singoli:

```python
"This is a string"
'This is a string also'
```

Puoi usare tripli doppi apici oppure tripli apici singoli per racchiudere una stringa multilinea, preservando spazi e formattazione:

```python
"""
This is
        a string
        with spaces.
"""
'''
This is
        a string
        with spaces
    also.
'''
```

I **letterali booleani** sono solo due: `True` e `False`. `True` rappresenta un valore di verita', mentre `False` rappresenta un valore di falsita'.

```python
True
False
```

Ricorda che in Python la prima lettera di `True` e `False` deve essere sempre maiuscola.
