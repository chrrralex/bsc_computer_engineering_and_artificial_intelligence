# 07. Stringhe

### 07.01. Panoramica

Una stringa e' una collezione ordinata di caratteri. Un carattere e' un simbolo identificato univocamente da un codice, che dipende dal set di caratteri usato dal linguaggio o dal sistema. Python usa Unicode come insieme di caratteri: questo significa che puo' rappresentare piu' di un milione di caratteri appartenenti a lingue e culture diverse.

Lo standard Unicode propone tre codifiche principali:

- UTF-8 (Unicode Transformation Format - 8 bit): puo' rappresentare piu' di 250 caratteri ed e' retrocompatibile con ASCII a 7 e 8 bit,
- UTF-16 (Unicode Transformation Format - 16 bit): puo' rappresentare piu' di 65 mila caratteri,
- UTF-32 (Unicode Transformation Format - 32 bit): puo' rappresentare piu' di un milione di caratteri.

In Python una stringa e' racchiusa tra apici doppi o singoli:

```python
"This is a string literal"
'Also this is a string literal'
```

Puoi usare la funzione built-in `print()` per stampare una stringa sullo standard output:

```python
a = "Hello, World!\n"
print(a)  # "Hello, World!"
```

Una stringa racchiusa tra doppi apici puo' contenere apici singoli; allo stesso modo, una stringa racchiusa tra apici singoli puo' contenere doppi apici:

```python
"This is 'a string' enclosed by the double quotes"
'This is "a string" enclosed by the single quotes'
```

Puoi anche specificare una stringa multilinea:

```python
a = """This
is a multiple
line string"""
print(a)
```

Per le stringhe multilinea puoi usare sia tre apici singoli `'''` sia tre apici doppi `"""`.

La funzione `len()` restituisce la lunghezza di una stringa, cioe' il numero di caratteri che contiene:

```python
text = "Hello"
print(len(text))  # 5
```

### 07.02. Slicing

Puoi usare l'operatore di slicing per ottenere una sottostringa dalla stringa originale:

```python
a = "Hello"
print(a[2:4])  # ll
```

Le regole dell'operatore `[n:m]` sono sempre le stesse: sia `n` sia `m` sono opzionali. Se `n` non e' presente, il valore predefinito e' `0`. Se `m` non e' presente, il valore predefinito e' la lunghezza della stringa.

```python
a = "Hello"
print(a[2:4])  # ll
print(a[:4])  # Hell
print(a[2:])  # llo
```

Puoi creare una copia della stringa originale usando solo i due punti `:`:

```python
a = "Hello"
b = a[:]
print(b)  # Hello
```

Puoi usare anche indici negativi:

```python
a = "Hello"
print(a[-3:-1])  # ll
```

### 07.03. Caratteri di escape

Per inserire caratteri che non possono comparire direttamente dentro una stringa, si usa un carattere di escape. Un carattere di escape e' una barra inversa `\` seguita dal carattere che vuoi inserire. Un esempio classico e' il doppio apice all'interno di una stringa delimitata da doppi apici:

```python
"This is an " illegal string"  # ERROR!
```

In questo caso devi usare un escape:

```python
"This is an \" illegal string"
```

Alcuni dei caratteri di escape piu' comuni sono:

- `\n`: nuova riga,
- `\r`: ritorno carrello,
- `\a`: avviso sonoro,
- `\t`: tabulazione orizzontale,
- `\v`: tabulazione verticale,
- `\\`: barra inversa,
- `\"`: doppio apice,
- `\'`: apice singolo,
- `\b`: backspace.

Python consente anche di specificare caratteri Unicode tramite tre cifre ottali o due cifre esadecimali:

- `\ooo`, dove `ooo` sono tre cifre ottali da `000` a `777`,
- `\xhh`, dove `hh` sono due cifre esadecimali da `00` a `FF`.

### 07.04. Concatenazione

Puoi usare l'operatore di concatenazione `+` per unire due o piu' stringhe:

```python
a = "Hello"
b = "World"
print(a + " " + b + "!")  # Hello, World!
```

In Python il significato di `+` dipende dal contesto:

- se gli operandi sono numeri, `+` rappresenta la somma,
- se gli operandi sono stringhe, `+` rappresenta la concatenazione.

```python
print(10 + 5)  # 15
print("Hello, " + "World!")  # Hello, World!
```

### 07.05. Metodi

Tutti i metodi descritti di seguito non modificano la stringa originale, ma ne creano una copia e lavorano su quella. In Python, infatti, le stringhe sono immutabili.

`upper()` restituisce la stessa stringa in maiuscolo:

```python
a = "Hello"
print(a.upper())  # HELLO
```

`lower()` restituisce la stessa stringa in minuscolo:

```python
a = "HELLO"
print(a.lower())  # hello
```

`strip()` restituisce la stringa senza spazi all'inizio e alla fine:

```python
a = "   Hello!   "
print(a.strip())  # "Hello!"
```

`capitalize()` converte in maiuscolo il primo carattere:

```python
a = "hello"
print(a.capitalize())  # Hello
```

`count()` accetta una stringa o un carattere e restituisce il numero di occorrenze:

```python
text = "The apple is on the pineapple"
print(text.count("apple"))  # 2
```

`endswith()` restituisce `True` se la stringa termina con il valore specificato:

```python
a = "Hello"
print(a.endswith("llo"))  # True
print(a.endswith("lli"))  # False
```

`startswith()` restituisce `True` se la stringa inizia con il valore specificato:

```python
a = "Hello"
print(a.startswith("Hi"))  # False
print(a.startswith("He"))  # True
```

`find()` cerca una sottostringa e restituisce la posizione in cui viene trovata. Se il valore non e' presente, restituisce `-1`:

```python
a = "Hello"
print(a.find("llo"))  # 2
print(a.find("ll0"))  # -1
```

`isalnum()` restituisce `True` se tutti i caratteri della stringa sono alfanumerici:

```python
a = "Hell0123"
print(a.isalnum())  # True
```

`isalpha()` restituisce `True` se tutti i caratteri sono lettere:

```python
a = "Hello"
print(a.isalpha())  # True
```

`isascii()` restituisce `True` se tutti i caratteri appartengono all'insieme ASCII:

```python
a = "aeiou"
print(a.isascii())  # True
b = "⑳⑳⑳"
print(b.isascii())  # False
```

`isdecimal()` restituisce `True` se tutti i caratteri della stringa sono cifre decimali:

```python
a = "123"
print(a.isdecimal())  # True
b = "FFF"
print(b.isdecimal())  # False
```

`isdigit()` restituisce `True` se tutti i caratteri sono cifre:

```python
a = "123"
print(a.isdigit())  # True
```

`isidentifier()` restituisce `True` se la stringa e' un identificatore valido:

```python
a = "aNum"
print(a.isidentifier())  # True
```

`islower()` restituisce `True` se tutti i caratteri sono minuscoli:

```python
a = "hello"
print(a.islower())  # True
```

`isupper()` restituisce `True` se tutti i caratteri sono maiuscoli:

```python
a = "HELLO"
print(a.isupper())  # True
```

`replace()` restituisce una nuova stringa in cui un valore specificato viene sostituito con un altro:

```python
text = "I love pizza"
print(text.replace("pizza", "pasta"))  # I love pasta
```

`rfind()` cerca una sottostringa e restituisce l'ultima posizione in cui compare; se non e' presente, restituisce `-1`:

```python
text = "Pizza Pizza Pizza"
print(text.rfind("Pizza"))  # 12
```

`rstrip()` restituisce una versione della stringa senza spazi finali:

```python
text = "   Hello   "
print(text.rstrip())  # "   Hello"
```

`split()` divide la stringa sul separatore specificato e restituisce una lista:

```python
fruits = "apple,orange,cherry,kiwi"
print(fruits.split(","))  # ['apple', 'orange', 'cherry', 'kiwi']
```

`zfill()` riempie la stringa con un numero specificato di zeri iniziali:

```python
text = "50"
print(text.zfill(10))  # 0000000050
```

### 07.06. Formattazione con l'operatore `%`

In Python, l'operatore modulo per le stringhe `%` e' un modo piu' vecchio di formattare stringhe, spesso chiamato *printf-style formatting*. Funziona inserendo valori in segnaposto presenti nella stringa.

A sinistra di `%` c'e' una stringa con gli specificatori di formato; a destra c'e' invece un valore o una tupla di valori. Ogni specificatore viene sostituito, in ordine, dal valore corrispondente.

Gli specificatori piu' comuni sono:

- `%s` per le stringhe,
- `%r` per la rappresentazione ottenuta con `repr()`,
- `%d` e `%i` per gli interi,
- `%f` per i numeri floating-point,
- `%e` per la notazione scientifica,
- `%x` e `%X` per l'esadecimale,
- `%o` per l'ottale,
- `%%` per il carattere `%` letterale.

Per esempio:

```python
print("%s is a friend of %s" % ("Alice", "Bob"))  # "Alice is a friend of Bob"
```

Il primo elemento della tupla, `"Alice"`, prende il posto del primo `%s`; il secondo, `"Bob"`, prende il posto del secondo `%s`. Se nella stringa c'e' un solo specificatore, puoi evitare la tupla:

```python
print("%s is my friend" % "Alice")  # "Alice is my friend"
```

Per maggiori dettagli puoi fare riferimento alla documentazione ufficiale di Python.

### 07.07. Formattazione con `.format()`

Un altro modo per ottenere una stringa formattata e' usare il metodo `.format()`, invocato direttamente sulla stringa. In questo caso i segnaposto sono rappresentati dalle parentesi graffe `{}`.

Per esempio:

```python
print("{} is {} years old".format("Alice", 25))  # "Alice is 25 years old"
```

Il metodo `.format()` accetta un numero variabile di argomenti, uno per ogni segnaposto. Se passi piu' valori del necessario, quelli in eccesso vengono ignorati. Se ne passi meno, Python solleva un `IndexError`.

Puoi usare specificatori di formato all'interno delle parentesi graffe. I piu' comuni sono:

- `{}` per il formato predefinito,
- `{:d}` per gli interi,
- `{:f}` per i floating-point,
- `{:.2f}` per due cifre decimali,
- `{:x}` e `{:X}` per l'esadecimale,
- `{:o}` per l'ottale.

Con `.format()` puoi anche usare l'indicizzazione posizionale:

```python
print("{2} {0} {1}".format("a", "b", "c"))  # "c a b"
```

Inoltre puoi usare argomenti con nome:

```python
print("{name} is {age} years old".format(name="Alice", age=30))
```

Anche in questo caso, per approfondire conviene consultare la documentazione ufficiale.

### 07.08. Formattazione con `f""` (f-string)

Il modo piu' moderno e pratico per formattare stringhe in Python 3 e' usare le *f-string*. Una f-string e' una stringa preceduta dal prefisso `f` e contenente zero, uno o piu' segnaposto tra parentesi graffe.

Ecco un esempio:

```python
name = "Bob"
age = 30
print(f"{name} is {age} years old")  # "Bob is 30 years old"
```

Le f-string possono usare, tra gli altri, questi specificatori:

- `{var}` per inserire direttamente il valore di una variabile,
- `{var!r}` per usare `repr()`,
- `{var:d}` per gli interi,
- `{var:f}` per i floating-point,
- `{var:x}` e `{var:X}` per l'esadecimale,
- `{var:o}` per l'ottale,
- `{var:e}` per la notazione scientifica.

Puoi anche specificare larghezza e allineamento. Per esempio, `{var:>10}` indica un allineamento a destra su 10 posizioni, `{var:<10}` un allineamento a sinistra, `{var:^10}` un allineamento centrato e `{var:0>5}` un allineamento a destra su 5 posizioni riempiendo con zeri.

Le f-string costituiscono una sorta di mini-linguaggio molto potente integrato in Python. Per ulteriori dettagli, rimane comunque consigliata la documentazione ufficiale.
