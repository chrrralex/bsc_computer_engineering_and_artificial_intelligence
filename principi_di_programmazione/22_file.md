# 22. File

### 22.01. Panoramica su file e directory in Windows, Linux e macOS

Il file system e' una delle parti piu' importanti di un sistema operativo. Oggi esistono diversi sistemi operativi, ma i piu' noti sono Windows, macOS e Linux. In questo capitolo cercheremo di chiarire che cosa sono file system, file e directory.

Un file system e' il modo in cui un sistema operativo organizza e gestisce i dati sui dispositivi di memoria, come hard disk, memorie flash o SSD. Definisce come i file vengono memorizzati, nominati e accessibili. NTFS, FAT32 ed ext4 sono esempi comuni di file system.

Un file e' una collezione nominata di dati memorizzata su disco, normalmente vista come un flusso di byte. Un file puo' contenere testo, immagini, codice o dati binari. Ogni file si trova in una directory specifica del file system e ha un nome e, spesso, un'estensione che fornisce informazioni sul contenuto. Per esempio, un sorgente Python e' un file con estensione `.py`.

Una directory, o cartella, e' un contenitore usato per organizzare file e altre directory. Aiuta a strutturare i dati in modo gerarchico. In Linux e macOS esiste una sola directory radice, mentre in Windows possono esistere piu' radici a seconda delle partizioni o dei volumi.

Un path e' una stringa che specifica la posizione di un file o di una directory nel file system. Due file con lo stesso nome non possono esistere nella stessa directory. Esistono due tipi principali di path:

- Un path assoluto specifica la posizione del file o della directory a partire dalla radice del file system.
- Un path relativo specifica la posizione del file o della directory a partire dalla directory di lavoro corrente.

In Windows, an example of an absolute path is:

```bash
C:\Users\Alice\Documents\file.txt
```

In Linux, or Mac OS X, an example of absolute path is:

```bash
/home/bob/file.txt
```

Windows e' generalmente case-insensitive, mentre Linux e macOS sono case-sensitive. Nei path relativi, `.` indica la directory corrente e `..` quella padre.

### 22.02. Modalita' di apertura dei file con `open()`

Python fornisce una funzione built-in per aprire file, chiamata `open()`. Quando vuoi usare un file in un programma Python, devi prima aprirlo. Aprire un file significa preparare il flusso di I/O per leggerlo o scriverlo.

La funzione `open()` accetta principalmente due parametri:

- il `filename`, oppure un path relativo o assoluto che lo contiene,
- il `mode`, cioe' la modalita' con cui Python accede al file.

Il parametro `mode` e' particolarmente importante, perche' determina come il file viene letto o scritto e se debba essere trattato come file di testo o file binario. I valori principali sono:

- `r`: apre il file in lettura ed e' il valore di default. Se il file non esiste, Python genera un errore.
- `w`: apre il file in scrittura. Se il file non esiste lo crea; se esiste, ne sovrascrive il contenuto.
- `a`: apre il file in append. Se il file non esiste lo crea; se esiste, aggiunge il nuovo contenuto in fondo senza sovrascrivere quello precedente.
- `x`: apre il file in modalita' creazione esclusiva. Se il file esiste gia', Python genera un errore.

Puoi aggiungere la lettera `t` per specificare un file di testo, che e' anche il valore predefinito, oppure la lettera `b` per indicare un file binario. Vedremo questi casi nei paragrafi successivi.

Puoi usare la funzione built-in `open()` in questo modo:

```python
f = open("file.txt")
```

La riga precedente apre un file chiamato `file.txt` nella directory corrente in modalita' lettura e testo, entrambe predefinite. `f` e' una variabile che contiene l'oggetto file. In Python puoi leggere e scrivere un file solo attraverso questo oggetto. La riga precedente equivale a:

```python
f = open("file.txt", "rt")
```

### 22.03. Lettura dei file con `read()`, `readline()` e `readlines()`

Consideriamo un file chiamato `text.txt` con il seguente contenuto:

```txt
Hello! Welcome to text.txt
This file is for testing purposes.
Good Luck!
```

L'oggetto file restituito da `open()` ha tre metodi principali per la lettura:

- `read()` legge l'intero contenuto del file e restituisce una stringa. Puoi passare anche una dimensione per leggere solo un certo numero di caratteri.
- `readline()` legge una sola riga del file. Se lo chiami piu' volte, ottieni righe diverse in sequenza. Il carattere di newline `\n` e' incluso nella stringa restituita.
- `readlines()` legge tutte le righe e restituisce una lista di stringhe, una per riga, di solito comprensive del `\n` finale.

Cominciamo dai metodi di lettura. Il seguente codice stampa tutto il contenuto di `text.txt`:

```python
f = open("text.txt")
print(f.read()) # Hello! Welcome to text.txt
                # This file is for testing purposes.
                # Good Luck!
```

Nel seguente esempio stampiamo il file riga per riga:

```python
f = open("text.txt")
print(f.readline()) # Hello! Welcome to text.txt
print(f.readline()) # This file is for testing purposes.
print(f.readline()) # Good Luck!
```

Abbiamo chiamato `readline()` tre volte, ottenendo una riga diversa a ogni chiamata.

Ecco un esempio di `readlines()` con un ciclo `for`:

```python
f = open("text.txt")
for line in f.readlines():
    print(line)     # Hello! Welcome to text.txt
                    # This file is for testing purposes.
                    # Good Luck!
```

### 22.04. Scrittura di file con `write()` e `writelines()`

Un oggetto file espone i metodi `write()` e `writelines()`. Per aprire un file in scrittura puoi usare le modalita' `w` e `a`: `w` riscrive il file da zero, mentre `a` aggiunge il nuovo contenuto in coda.

`write()` puo' scrivere una o piu' righe, a seconda di come usi il carattere `\n`:

```python
f = open("text.txt", "w")
f.write("This is the first line\n") # 23
f.write("This is the second line\n") # 24
```

Quando usi `write()`, il carattere `\n` non viene inserito automaticamente. Il valore restituito da `write()` e' il numero di caratteri scritti in modalita' testo, oppure il numero di byte scritti in modalita' binaria.

Il metodo `writelines()` accetta una lista di stringhe. Tipicamente, ogni elemento della lista rappresenta una riga se contiene il carattere `\n`. Ecco un esempio:

```python
f = open("text.txt", "w")
f.writelines([
    "This is the first line\n",
    "This is the second line\n",
    "This is the third line\n"
])
```

A differenza di `write()`, `writelines()` non restituisce alcun valore utile.

### 22.05. Chiusura del file con `close()`

Se vuoi chiudere il file che stai usando, in lettura o in scrittura, puoi usare `close()`:

```python
f = open("text.txt")

# ... some code to read/write the file ...

f.close()
```

E' importante chiudere sempre il file quando hai finito di usarlo, cosi' da rilasciare correttamente le risorse del sistema operativo.

### 22.06. Context manager con la parola chiave `with`

Puoi usare un context manager per leggere o scrivere un file tramite la parola chiave `with`:

```python
with open("text.txt") as f:
    for line in f:
        print(line)
```

Nota che abbiamo usato il ciclo `for` con `line in f`: Python vede infatti un file in lettura come un oggetto iterabile.

Usare un context manager ha diversi vantaggi:

- Prima di tutto, alla fine del blocco `with` il file viene chiuso automaticamente, quindi non devi scrivere `f.close()`.
- Inoltre, questo approccio e' raccomandato da PEP 343.
- Richiede meno codice per gestire apertura e chiusura del file.
- Rende piu' chiaro lo scopo del blocco di codice.
- Garantisce una corretta pulizia delle risorse anche in presenza di eccezioni.

In sintesi, l'uso di `with` garantisce la chiusura automatica e sicura del file, rendendo il codice piu' pulito e affidabile.

### 22.07. File di testo e file binari

Un file memorizzato nel file system puo' essere di due tipi:

- File di testo: viene visto come un flusso di caratteri, compatibili con il set di caratteri e la codifica usati dal sistema.
- File binario: viene visto come un flusso di byte. Ogni elemento del flusso e' un byte, cioe' un gruppo di 8 bit.

Entrambi i tipi sono usati in Python e la scelta dipende dall'applicazione. Le differenze principali tra file di testo e file binari sono:

- Contenuto. Un file di testo e' un flusso di caratteri, mentre un file binario e' un flusso di byte.
- Leggibilita'. Un file di testo e' leggibile da una persona, un file binario in genere no.
- Codifica. Un file di testo usa una codifica per rappresentare i caratteri, mentre un file binario viene trattato come sequenza grezza di byte.
- Modalita'. In Python un file di testo si legge o scrive tipicamente con `r` e `w`, mentre un file binario con `rb` e `wb`.
- Tipo dato. In Python il contenuto di un file di testo e' una stringa `str`, mentre il contenuto di un file binario e' una sequenza `bytes`.

Esempi di file di testo sono `.txt`, `.csv` e `.py`. Esempi di file binari sono `.mp3`, `.mp4` e `.png`.

### 22.08. Accesso sequenziale e casuale con `seek()` e `tell()`

Quando apri un file per leggerlo o scriverlo, esiste un puntatore alla posizione corrente che tiene traccia dell'ultima operazione effettuata. L'oggetto file ha due metodi utili per gestire questo puntatore: `seek()` e `tell()`.

Il metodo `tell()` restituisce la posizione corrente del puntatore, come intero che rappresenta il numero di byte dall'inizio del file. Per esempio, il seguente codice apre un file in scrittura, scrive due caratteri e poi chiama `tell()`:

```python
f = open("text.txt", "w")
f.write("A\n")
print(f.tell()) # 2
```

Se proviamo a scrivere altri due caratteri da un byte ciascuno, succede questo:

```python
f.write("B\n")
print(f.tell()) # 4
```

Lo stesso discorso vale in lettura:

```python
f = open("text.txt")

print(f.tell()) # 0
print(f.readline()) # "A"

print(f.tell()) # 2
print(f.readline()) # "B"

print(f.tell()) # 4
```

Se provi a chiamare `readline()` una terza volta, otterrai una stringa vuota e `f.tell()` continuera' a restituire `4`, cioe' la fine del file.

`seek()` e' il metodo complementare di `tell()`, perche' serve a spostare il puntatore. Accetta due parametri:

- `offset`, cioe' il numero di byte di spostamento,
- `whence`, che indica rispetto a quale riferimento va interpretato l'offset:
    - `0`: e' il valore di default e indica che l'offset e' riferito all'inizio del file.
    - `1`: l'offset e' riferito alla posizione corrente del file.
    - `2`: l'offset e' riferito alla fine del file.

Ecco un esempio:

```python
f = open("text.txt")

print(f.tell()) # 0
print(f.readline()) # A

f.seek(0) # equivalent to f.seek(0, 0), or f.seek(0, whence = 0)
print(f.readline()) # A
print(f.tell()) # 2

f.seek(0) # equivalent to f.seek(0, 0), or f.seek(0, whence = 0)
print(f.readline()) # A
print(f.tell()) # 2
```

Puoi posizionare il puntatore alla fine del file con questa istruzione:

```python
f.seek(0, whence = 2)
```

or:

```python
f.seek(0, 2)
```

### 22.09. File temporanei

Python mette a disposizione la libreria `tempfile` per lavorare con file temporanei. I file temporanei vengono creati per memorizzare dati solo per la durata dell'esecuzione del programma e sono spesso usati per caching, debugging o test.

Per usare un file temporaneo devi prima importare il modulo `tempfile`:

```python
import tempfile
```

Puoi usare `tempfile.TemporaryFile()` per creare un nuovo file temporaneo gestito automaticamente dal modulo. Il modo consigliato e' tramite context manager:

```python
with tempfile.TemporaryFile() as tf:
    tf.write(b"Hello")
    tf.seek(0)
    print(tf.read()) # "Hello"
```

Nell'esempio precedente il modulo `tempfile` crea il file e, grazie al context manager, possiamo usarlo tramite l'identificatore `tf`. Scriviamo dei byte, riportiamo il puntatore all'inizio e poi rileggiamo il contenuto.

Puoi usare anche `tempfile.NamedTemporaryFile()`, che crea un file temporaneo dotato di nome accessibile tramite la proprieta' `name`:

```python
with tempfile.NamedTemporaryFile() as tf:
    print(tf.name)
```

Puoi anche creare una directory temporanea con `tempfile.TemporaryDirectory()`:

```python
with tempfile.TemporaryDirectory() as td:
    print(td)
```

Ricorda che, grazie al context manager, tutte queste risorse vengono ripulite automaticamente alla fine del blocco.

### 22.10. File JSON

JSON (JavaScript Object Notation) e' un formato testuale leggero usato per rappresentare dati strutturati con oggetti e array. In Python puoi lavorare con JSON usando il modulo standard `json`: `json.dump()` scrive un oggetto Python su file, mentre `json.load()` legge JSON da un file e lo converte in tipi Python.

Ecco un esempio di scrittura di JSON su file:

```python
import json

data = { "name": "Alice", "age": 30, "skills": ["Python", "SQL"] }

with open("profile.json", "w") as f:
    json.dump(data, f)
```

Ecco un esempio di lettura di JSON da file:

```python
import json

with open("profile.json", "r") as f:
    data = json.load(f)
    print(data) # { "name": "Alice", "age": 30, "skills": ["Python", "SQL"] }
```

### 22.11. File CSV

CSV (Comma-Separated Values) e' un formato testuale semplice per dati tabellari, in cui ogni riga rappresenta un record e i valori sono separati da un delimitatore, tipicamente la virgola. In Python il modulo standard `csv` fornisce `csv.writer` e `csv.reader` per scrivere e leggere questi file.

Ecco un esempio di scrittura di un CSV:

```python
import csv

rows = [
    ["name", "age"],
    ["Alice", 30],
    ["Bob", 25]
]

with open("people.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(rows)
```

Ecco un esempio di lettura di un CSV:

```python
import csv

with open("people.csv", "r", newline="") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

### 22.12. Serializzazione e deserializzazione di strutture dati e oggetti

La serializzazione e' il processo di conversione di un oggetto Python in un formato che possa essere memorizzato o trasmesso, per esempio testo JSON o un flusso binario. La deserializzazione e' il processo inverso. In pratica, JSON e' spesso usato per strutture semplici, mentre `pickle` e' usato per oggetti Python piu' complessi.

Esempio di serializzazione in JSON:

```python
import json

data = {"name": "Alice", "scores": [28, 30, 27]}

with open("scores.json", "w") as f:
    json.dump(data, f)
```

Esempio di deserializzazione da JSON:

```python
import json

with open("scores.json", "r") as f:
    data = json.load(f)
    print(data)
```

### 22.13. File con `pickle`

`pickle` e' un modulo usato per serializzare e deserializzare oggetti Python. Converte gli oggetti in un flusso di byte che puo' essere salvato in un file, ed e' per questo molto utile con strutture dati complesse come liste, dizionari e oggetti.

L'azione di salvataggio viene chiamata *pickling*. Nel codice seguente importiamo `pickle`, creiamo un dizionario e lo salviamo in un file binario chiamato `data.pkl`.


```python
import pickle

data = {"name": "Alice", "age": 30}

with open("data.pkl", "wb") as f:
    pickle.dump(data, f) # pickling
```

La funzione `pickle.dump()` accetta come primo argomento la struttura dati da serializzare e come secondo il file aperto in modalita' binaria, in questo caso `wb`.

L'operazione inversa si chiama *unpickling*. Il codice e' simile, ma usa `pickle.load()` per leggere dal file binario e ricostruire l'oggetto Python:

```python
import pickle

with open("data.pkl", "rb") as f:
    data = pickle.load(f) # unpickling
    print(data)
```

Anche in lettura usiamo la modalita' binaria `rb`.

### 22.14. File con `shelve`

`shelve` e' un modulo che fornisce un oggetto persistente simile a un dizionario, salvato su memoria di massa. Puoi accedervi con chiavi e valori come a un normale `dict`, ma il contenuto viene mantenuto tra un'esecuzione e l'altra. Internamente `shelve` usa `pickle`, quindi le chiavi devono essere stringhe e i valori devono essere serializzabili.

Il modo consigliato per lavorare con uno `shelve` e' tramite context manager, cosi' viene chiuso correttamente e i dati sono scritti in modo sicuro.

Il seguente esempio mostra una serializzazione con `shelve`:

```python
import shelve

with shelve.open("students_db") as db:
    db["student:1"] = {"name": "Alice", "age": 21}
    db["student:2"] = {"name": "Bob", "age": 22}
```

Ecco invece un esempio di deserializzazione, cioe' caricamento dei dati con `shelve`:

```python
import shelve

with shelve.open("students_db") as db:
    alice = db["student:1"]
    print(alice)
```
