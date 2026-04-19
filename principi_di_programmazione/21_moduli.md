# 21. Moduli

### 21.01. Panoramica

Un modulo e' una libreria di codice in cui hai una o piu' entita' esportabili. In questo contesto, per entita' intendiamo elementi del linguaggio come funzioni, classi, costanti o variabili globali. Puoi vedere un modulo come un file che contiene codice riutilizzabile nella tua applicazione.

Python considera automaticamente un file con estensione `.py` come un modulo. Per esempio, se nella directory corrente hai un file chiamato `greetings.py`, Python lo vede come un modulo chiamato `greetings`. In questo file puoi definire una o piu' funzioni:

```python
def sayHello():
    print("Hello!")
```

Puoi anche creare variabili globali:

```python
GREETING_POSTFIX = "!\n"

def sayHello():
    print("Hello" + GREETING_POSTFIX)
```

Nell'esempio precedente abbiamo creato una variabile globale chiamata `GREETING_POSTFIX`. In un modulo puoi definire variabili di qualsiasi tipo: liste, tuple, dizionari, istanze e cosi' via.

In un altro file, per esempio `main.py`, puoi usare il modulo `greetings` tramite `import`:

```python
import greetings
```

Dopo questa riga puoi accedere a tutti i membri definiti nel modulo `greetings` usando una sintassi simile a quella dei metodi degli oggetti: nome del modulo, punto `.` e nome del membro.

```python
import greetings

print(greetings.GREETING_POSTFIX) # "!\n"
greetings.sayHello() # "Hello!\n"
```

L'istruzione `import` permette anche di usare un alias per un modulo tramite la parola chiave `as`:

```python
import greetings as grtns
```

Dopo la riga precedente, il modulo `greetings` sara' disponibile nel file con il nome `grtns`.

Python ha un sistema di moduli molto esteso, molti dei quali fanno parte della Python Standard Library. Per esempio `math`, `os` e `sys` possono essere importati senza installare nulla tramite pip, perche' sono gia' presenti nell'installazione standard di Python:

```python
import os
import sys
import math
```

Se non sai cosa contiene un modulo, puoi usare la funzione built-in `dir()`, che restituisce la lista degli identificatori disponibili nel modulo passato come argomento:

```python
import math

dir(math) # ['__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'acos', ... ]
```

Puoi usare `dir()` anche sui moduli creati da te.

Puoi importare un singolo membro di un modulo combinando `from` e `import`:

```python
from greetings import sayHello

sayHello() # "Hello!\n" 
```

In questo caso possiamo usare direttamente `sayHello()` senza `greetings.`, perche' abbiamo importato il membro specifico. Puoi indicare anche piu' membri:

```python
from greetings import GREETING_POSTFIX, sayHello
```

Con `from` puoi anche rinominare uno o piu' membri esportati usando `as`:

```python
from math import sqrt as s, pow as p

print(s(4))
print(p(4, 2))
```

### 21.02. Membri pubblici e privati

In un modulo puoi avere funzioni o variabili che vuoi usare solo internamente. Per segnalare una funzione o variabile come privata si usa convenzionalmente il prefisso `_`. Per esempio, se hai un modulo `examples.py` fatto cosi':

```python
a = 10 # questa e' una variabile pubblica

_b = 20 # questa e' una variabile privata

def f(): # questa e' una funzione pubblica
    pass

def _g(): # questa e' una funzione privata
    pass
```

puoi usare l'istruzione `from examples import *` e provare a usare ogni membro importato in un altro file, per esempio `main.py`:

```python
from examples import *

print(a) # va bene, perche' a e' pubblica
print(_b) # errore, perche' _b e' privata: ERROR! NameError: name '_b' is not defined

f() # va bene, perche' f() e' pubblica
_g() # errore, perche' _g() e' privata: ERROR! NameError: name '_g' is not defined
```

I membri privati hanno effetto soprattutto quando usi `from examples import *`. Se invece importi `_b` e `_g()` esplicitamente, saranno disponibili nel tuo codice:

```python
from examples import _b, _g

print(_b) # no problem, cause _b is imported explicitly
_g() # no problem, cause _g() is imported explicitly
```

### 21.03. Dove si trovano i moduli in Python

Ma come fa Python a trovare e caricare uno o piu' moduli nel programma corrente? `sys.path`, disponibile nel modulo `sys`, e' una lista di directory che Python cerca quando importa i moduli. Puoi stamparne il contenuto cosi':

```python
import sys
print(sys.path)
```

Se vuoi aggiungere una directory personalizzata, per esempio una cartella in cui tieni i tuoi moduli, puoi modificare direttamente `sys.path`:

```python
import sys
sys.path.append("./modules/")
```

Per default, `sys.path` contiene anche la stringa vuota `""`, che rappresenta la directory di lavoro corrente.

`PYTHONPATH` e' una variabile d'ambiente che aggiunge directory al percorso di ricerca dei moduli. Queste directory vengono aggiunte automaticamente a `sys.path` quando Python si avvia. Un altro modo per includere moduli personalizzati e' quindi modificare `PYTHONPATH`:

```bash
export PYTHONPATH=/modules # in Linux, or OS X
set PYTHONPATH=C:\modules # in Windows
```

Un terzo modo per aggiungere directory personalizzate e' usare file `.pth`, tipicamente presenti dentro `site-packages`:

```python
/modules
```

All'avvio, Python legge i file `.pth` e aggiunge quei percorsi a `sys.path`.

`sys.prefix` indica la directory radice dell'installazione Python o dell'ambiente virtuale corrente. Puoi stamparlo cosi':

```python
import sys
print(sys.prefix)
```

### 21.04. Scope e namespace

Lo scope di una variabile o di una funzione e' la regione del programma in cui quell'identificatore e' accessibile. Python ha quattro scope principali:

- Scope locale: va dalla riga in cui la variabile viene dichiarata fino alla fine del blocco. Per esempio, le variabili definite dentro una funzione, o i suoi argomenti, hanno scope locale.
- Scope globale: va dalla riga in cui la variabile viene dichiarata fino alla fine del file. In Python un file e' anche un modulo, percio' questo scope e' spesso chiamato anche scope di modulo.
- Scope built-in: comprende funzioni, costanti e utilita' messe a disposizione direttamente da Python, come `len()`, `min()`, `max()` e `dir()`.

Here's an example:

```python
x = 10 # questa e' una variabile globale

def f(z): # gli argomenti sono variabili locali della funzione
    y = 100 # questa e' una variabile locale della funzione
    return y + z

for i in range(3): # range() e' una funzione built-in
    print(i) # i e' una variabile locale del ciclo for
```

Puoi creare anche funzioni annidate. In questo caso si parla spesso di *enclosing scope*, cioe' lo scope della funzione esterna rispetto a quella interna:

```python
def f():
    x = 10 # variabile locale di f
    def nested_f():
        y = 20 # variabile locale di nested_f
        return y
    return nested_f() + x

print(f()) # 30
```

Nell'esempio precedente, `x` ha scope limitato a `f()`, mentre `y` ha scope limitato a `nested_f()`.

Puoi vedere questi scope anche come namespace. Un namespace e' un contenitore logico in cui identificatori di variabili, funzioni e altre entita' risultano visibili. In Python distinguiamo almeno tre livelli di namespace:

- Namespace globale: contiene gli identificatori globali visibili nel modulo corrente.
- Namespace locale: contiene gli identificatori visibili nella funzione o nel blocco corrente.
- Namespace built-in: e' sempre presente e contiene gli identificatori disponibili direttamente nell'ambiente Python.

Python permette di ispezionare gli identificatori legati al namespace corrente tramite questi strumenti:

- `locals()`, che restituisce un dizionario con gli identificatori del namespace locale.
- `globals()`, che restituisce un dizionario con gli identificatori del namespace globale.
- il modulo `builtins`, utile per ispezionare il namespace built-in.

Per esempio:

```python
print(locals()) # stampa tutti i membri del namespace locale
print(globals()) # stampa tutti i membri del namespace globale

import builtins
print(dir(builtins)) # stampa tutti i membri del namespace built-in
```

### 21.05. Conflitti tra nomi

Un conflitto di nomi si verifica quando due variabili, funzioni o moduli hanno lo stesso nome, causando l'uso dell'elemento sbagliato o nascondendone un altro.

Una variabile locale puo' nascondere una variabile globale con lo stesso nome:

```python
x = 10

def func():
    x = 5 # la variabile locale x nasconde la variabile globale x
    print(x)

func() # 5
print(x) # 10
```

Se usi lo stesso nome di una funzione built-in, la nascondi:

```python
len = 10
print(len) # 10
print(len([ 1, 2, 3 ])) # ERROR! TypeError: 'int' object is not callable
```

Se un file ha lo stesso nome di un modulo standard, Python potrebbe importare quello sbagliato. Per esempio, se hai un file `math.py` nella directory corrente, la seguente istruzione importera' il tuo modulo, non quello standard:

```python
import math # questo e' il tuo modulo, non quello standard di Python
```

Anche due oggetti importati possono condividere lo stesso nome:

```python
from math import sqrt
from cmath import sqrt # da qui in poi viene usata sqrt() del modulo cmath
```

### 21.06. Il modulo `os`

Un modulo particolarmente importante in Python e' `os`. Questo modulo permette di lavorare con file, directory, variabili d'ambiente e informazioni sul sistema. Grazie a `os`, puoi:

- lavorare con il file system locale, creando, modificando o rimuovendo file e directory,
- creare o manipolare path relativi e assoluti,
- lavorare con le variabili d'ambiente del sistema,
- gestire uno o piu' processi del sistema.

Il modulo `os` e' pensato per essere il piu' possibile indipendente dalla piattaforma, quindi lo stesso codice puo' funzionare su Windows, macOS o Linux.

Per usare il modulo `os` devi prima importarlo:

```python
import os
```

Per ottenere la directory di lavoro corrente, usa `getcwd()`:

```python
os.getcwd()
```

Puoi cambiare la directory di lavoro corrente dello script con `chdir()`:

```python
os.chdir("/scripts/python")
```
Per elencare i file nella directory corrente, usa `listdir()`:

```python
os.listdir()
```

Per creare una directory, usa `mkdir()`:

```python
os.mkdir("my_new_folder")
```

Per creare una directory annidata puoi usare `makedirs()`, sfruttando normali path relativi o assoluti. Per esempio, le seguenti righe creano una directory padre `parent` e una figlia `child`:

```python
os.makedirs("parent/child")
```

Puoi rimuovere una directory con `rmdir()`:

```python
os.rmdir("my_new_folder")
```

Per rinominare un file, usa `rename()`:

```python
os.rename("old.txt", "new.txt")
```

Per eliminare un file, usa `remove()`:

```python
os.remove("new.txt")
```

Puoi unire due o piu' path usando la funzione `join()`:

```python
os.path.join("path1", "path2")
```

Se vuoi verificare se un file o una directory esistono, puoi usare `exists()`:

```python
os.path.exists("my_file.txt")
```

I metodi `isdir()` e `isfile()` di `os.path` restituiscono un booleano: `True` se la directory o il file esistono, `False` altrimenti.

```python
os.path.isfile("my_file.txt")
os.path.isdir("parent")
```

`os.path.isabs()` restituisce `True` se il path specificato e' assoluto:

```python
os.path.isabs("/bin")
```

`os.path.samefile()` accetta due argomenti e restituisce `True` se rappresentano lo stesso file:

```python
os.path.samefile("/bin/an_executable", "/bin/an_executable")
```

Il sottomodulo `os.path` contiene due costanti particolarmente utili per gestire i path:

- `os.curdir`, che restituisce il simbolo usato dal sistema operativo per rappresentare la directory corrente,
- `os.pardir`, che restituisce il simbolo usato per rappresentare la directory padre.

Per esempio, in Linux e in altri sistemi Unix-like questi simboli sono `.` per la directory corrente e `..` per quella padre. Per scrivere codice portabile e' buona pratica usare queste costanti invece di hardcodare i simboli.

Puoi accedere alle variabili d'ambiente del sistema tramite `os.environ`.

```python
os.environ["HOME"]
```

Per creare una nuova variabile d'ambiente puoi specificarne nome e valore cosi':

```python
os.environ["NEW_ENV_VAR"] = "Questa e' una nuova variabile d'ambiente"
```

`os.name` restituisce il nome del sistema operativo, mentre tramite `os.system()` puoi eseguire un sottoprocesso come se fossi dentro una shell. Per esempio:

```python
os.system("ls")
```

esegue il comando `ls` per elencare file e directory nella directory corrente.