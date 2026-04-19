# 0A. Python CLI

### 0A.01. Versioni di Python e PIP

In questa sezione vedremo alcuni comandi Python che possono essere usati direttamente in una console o in una CLI (Command-Line Interface), come zsh, bash, csh o altre shell.

Puoi vedere la versione di Python in questo modo:

```bash
python -v
# or
python --version
```

Puoi vedere la versione di PIP con il seguente comando:

```bash
pip -v
# or
pip --version
```

### 0A.02. Eseguire un programma con Python

Se hai un file chiamato `main.py`, cioe' un file sorgente Python con estensione `.py`, puoi usare questo comando:

```bash
python main.py
```

### 0A.03. Installare e disinstallare pacchetti

Puoi installare un pacchetto esterno usando il comando `pip install`:

```bash
pip install <packageName>
```

Per esempio, se vuoi installare un pacchetto esterno chiamato `cowsay`, puoi usare il seguente comando:

```python
pip install cowsay
```

Pip installera' non solo il pacchetto `cowsay`, ma anche tutte le sue dipendenze.

Se vuoi disinstallare un pacchetto, puoi usare `pip uninstall`:

```bash
pip uninstall <packageName>
```

Per esempio, se vuoi rimuovere `cowsay` dal sistema, puoi usare il seguente comando:

```bash
pip uninstall cowsay
```

Pip rimuovera' il pacchetto `cowsay` e, se possibile, anche le sue dipendenze non piu' utilizzate da altri pacchetti.

Puoi aggiornare un pacchetto esterno usando il flag `--upgrade` prima del nome del pacchetto:

```bash
pip install --upgrade <packageName>
```

For example:

```bash
pip install --upgrade cowsay
```

Se vuoi la lista dei pacchetti Python installati, puoi usare:

```bash
pip list
```

Se vuoi informazioni dettagliate su un pacchetto Python specifico, puoi usare `pip show`:

```bash
pip show <packageName>
```

An example:

```bash
pip show cowsay
```

Ma come funziona pip? Un pacchetto Python e' una libreria esterna che puoi aggiungere alla tua installazione Python tramite pip. pip e' il package manager ufficiale e piu' comune per Python. Si basa su PyPI, il repository ufficiale dei pacchetti Python, che contiene un numero molto ampio di librerie. Quando scegli se installare un pacchetto, i fattori principali da considerare sono:

- Community support and popularity.
- Frequency of updates.
- Documentation and ease of use.

### 0A.04. Usare un pacchetto con `import`

In un programma Python puoi importare e usare un pacchetto con l'istruzione `import`:

```python
import math
```

Dopo la riga precedente puoi usare l'identificatore `math` per accedere a variabili, funzioni e altre entita' definite nel modulo `math`. Questa e' la sintassi base di `import`.

Puoi importare piu' moduli in una sola riga separandoli con una virgola:

```python
import math, random
```

Puoi rinominare un modulo usando la parola chiave `as`, che permette di definire un alias:

```python
import numpy as np
```

Puoi importare un elemento specifico definito in un modulo usando `from`:

```python
from math import sqrt
```

Puoi specificare piu' elementi separandoli con la virgola:

```python
from math import sqrt, pi
```

Un'altra sintassi usa l'operatore `*`, che significa tutti gli elementi. Se vuoi importare tutto dal modulo `math`, puoi scrivere:

```python
from math import *
```

Puoi usare `from` e `as` nella stessa istruzione:

```python
from math import sqrt as square_root
```

In un programma Python, il simbolo `.` si riferisce al modulo corrente, mentre `..` si riferisce al modulo padre. Puoi importare i moduli del pacchetto corrente con:

```python
from . import * 
```

Puoi importare i moduli del pacchetto padre con:

```python
from .. import *
```

Puoi importare anche un modulo specifico:

```python
from . import <moduleName>
from .. import <moduleName>
```

oppure una lista di moduli:

```python
from . import <moduleName>, <moduleName>, ..., <moduleName>
from .. import <moduleName>, <moduleName>, ..., <moduleName>
```

### 0A.05. Ambienti virtuali con Python

Particolarmente importanti sono i VENV, cioe' i virtual environment. Un ambiente virtuale in Python e' un ambiente isolato nel tuo computer, nel quale puoi eseguire e testare i tuoi progetti. Ti permette di gestire dipendenze specifiche del progetto senza interferire con altri progetti o con l'installazione principale di Python. Puoi pensarlo come a un contenitore separato per ciascun progetto Python.

Ogni ambiente:

- Has its own Python interpreter.
- Has its own set of installed packages.
- Is isolated from other virtual environments.
- Can have different versions of the same package.

Usare ambienti virtuali e' importante perche':

- It prevents package version conflicts between projects.
- Makes projects more portable and reproducible.
- Keeps your system Python installation clean.
- Allows testing with different Python versions.

Puoi creare un VENV con il seguente comando:

```bash
python -m venv .venv
```

Questo comando crea una cartella chiamata `.venv` in cui vengono memorizzati pacchetti e dipendenze. Per usare il VENV, devi prima attivarlo:

```bash
source .venv/bin/activate # for Linux, or Mac OS
.venv\Scripts\activate # for Windows
```

Per disattivare un VENV:

```bash
deactivate
```

Dopo aver attivato il VENV, puoi installare uno o piu' pacchetti:

```bash
pip install cowsay
```

Dove `cowsay` e' il nome del pacchetto. Se vuoi un elenco di tutti i pacchetti installati in un VENV specifico, puoi usare il seguente comando:

```bash
pip freeze > requirements.txt
```

Il comando crea, oppure aggiorna, un file chiamato `requirements.txt` in cui ogni riga specifica un pacchetto con la relativa versione.
