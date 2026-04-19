# 00. Introduzione

### 00.01. Gestire la complessita

**Astrazione**: e' il processo attraverso il quale un sistema reale viene convertito in un modello. L'astrazione consiste in due passaggi:

1. considerare solo i dettagli essenziali e utili;
2. eliminare i dettagli inutili.

Un'astrazione permette a un architetto di osservare un modello da punti di vista diversi. Per esempio, un ingegnere elettronico potrebbe vedere un computer come un insieme di circuiti, mentre un progettista di microprocessori potrebbe vederlo come un insieme di blocchi logici combinatori e sequenziali.

**Modello delle tre Y**: il modello delle tre Y, dalle tre parole hierarchY, modularitY e regularitY, e' un modello molto utile per studiare, progettare e comprendere un moderno sistema digitale. I tre principi sono:

- **Gerarchia**: ogni sistema complesso, come un moderno sistema digitale, puo' essere visto come un albero di componenti. Il componente radice e' la vista concettuale del sistema considerato e contiene solo i dettagli piu' generali. Il componente radice e' composto da uno, due o piu' altri componenti: ispezionando questi componenti emergono ulteriori dettagli sul sistema. La gerarchia e' il principio di progetto che organizza un sistema complesso in piu' livelli di astrazione, dove ogni livello e' costruito a partire da componenti piu' semplici dei livelli inferiori. La figura seguente mostra come si possa pensare al principio di gerarchia:

<!-- da aggiungere -->
*In figura: principio di progetto della gerarchia*

- **Modularita**: e' il principio di progetto che divide un sistema in blocchi funzionali indipendenti chiamati moduli, ciascuno dei quali svolge un compito specifico. Ogni entita' indipendente e' detta anche componente o sottosistema. Per esempio, la CPU di un computer ha come scopo principale eseguire programmi; la memoria principale ha come scopo principale memorizzare programmi; il bus di sistema ha come scopo principale permettere la comunicazione tra i sottosistemi del sistema (CPU, RAM, dispositivi di I/O, HD, SSD, GPU, TPU e cosi' via). Ogni componente del sistema deve essere completamente definito in termini di ingressi, uscite e segnali di controllo. Inoltre, un componente deve essere quanto piu' possibile generico.

<!-- da aggiungere -->
*In figura: principio di progetto della modularita'*

- **Regolarita**: e' il principio di progetto che prevede l'uso di strutture ripetute e schemi uniformi all'interno di un sistema. In generale, se un problema e' gia' stato risolto da un altro componente, la soluzione piu' semplice ed efficiente e' spesso riutilizzare quel componente. Per lo stesso problema, o compito, il sistema dovrebbe usare lo stesso componente o modulo. In questo modo il layout del sistema diventa prevedibile.

<!-- da aggiungere -->
*In figura: principio di progetto della regolarita'*

**Disciplina**: e' un insieme di regole e convenzioni che definiscono come i segnali si comportano e interagiscono in un sistema, garantendo il funzionamento corretto e prevedibile di componenti interconnessi. Nel contesto dei circuiti digitali, la disciplina si riferisce di solito alla regola secondo cui i segnali vengono interpretati solo come livelli logici discreti, tipicamente 0 e 1, anziche' come valori analogici continui. Ogni componente deve includere la specifica completa del proprio comportamento.

### 00.02. Astrazione digitale

**Bit**: un bit e' la piu' semplice unita' digitale che un sistema digitale puo' elaborare durante un'esecuzione. Un bit, contrazione dei termini "binary" e "digit", e' un valore bistabile che puo' variare da `0` a `1`: `0` e' chiamato anche `low`, oppure `0 V`, oppure `-5 V`; `1` e' chiamato anche `high`, oppure `5 V`, oppure `+5 V`. Un bit e' normalmente rappresentato da uno specifico livello di tensione. Se hai una stringa di `N` bit, puoi rappresentare `2^N` combinazioni differenti: da `0` a `2^N - 1` (la stringa con tutti i bit uguali a `0` fa parte delle combinazioni possibili e ammesse).

**Quantita' di informazione**: una variabile discreta e' una variabile che puo' assumere uno tra un numero finito di stati. Una variabile discreta con `N` stati puo' essere rappresentata con `log2(N)` bit, piu' precisamente con `ceil(log2(N))`. Per esempio, un semaforo puo' trovarsi in tre stati: giallo, verde e rosso. Due bit sono sufficienti per rappresentarne lo stato: `00` per il giallo, `01` per il verde e `10` per il rosso (`11` non e' usato, oppure non e' uno stato valido, oppure puo' indicare un errore).

**Gerarchia dell'informazione**: nei capitoli successivi analizzeremo in dettaglio come e' organizzata la memoria gerarchica e perche' e' organizzata in questo modo. In modo fondamentale, una memoria moderna organizza i bit in questo modo:

- **Bit**: puo' essere `0` oppure `1`.
- **Nibble**: e' composto da quattro bit, da `0000` a `1111`, cioe' `2^4 = 16` combinazioni. E' meta' di un byte.
- **Byte**: e' composto da otto bit, da `00000000` a `11111111`, cioe' `2^8 = 256` combinazioni.
- **Word**: un moderno sistema di memoria e' organizzato in piu' righe; ogni riga ha la stessa dimensione, spesso un multiplo del byte. Un moderno sistema digitale puo' avere una memoria principale con righe di `32` oppure `64` byte, cioe' `256` oppure `512` bit.
- **Half-word**: e' meta' di una word. Per esempio, se una memoria e' organizzata in word da `32` byte, una half-word e' composta da `16` byte, cioe' `128` bit.

**msb, lsb, MSB e LSB**: una stringa di bit e' composta da un certo numero di cifre binarie, ognuna delle quali puo' essere `0` oppure `1`. La posizione di ogni cifra cresce progressivamente da destra verso sinistra: parte da `0` e termina a `N - 1`, dove `N` e' la lunghezza della stringa binaria. Definiamo:

- **lsb** (*least significant bit*): il primo bit della stringa, cioe' il bit situato all'estrema destra;
- **msb** (*most significant bit*): l'ultimo bit della stringa, cioe' il bit situato all'estrema sinistra;
- **LSB** (*Least Significant Byte*): il gruppo di otto bit situato all'estrema destra della stringa, cioe' i primi otto bit;
- **MSB** (*Most Significant Byte*): il gruppo di otto bit situato all'estrema sinistra della stringa, cioe' gli ultimi otto bit.

Consideriamo il seguente esempio. Nella stringa binaria:

```text
10010011 10100000 11110000
```

- l'`lsb` e' `0`;
- l'`msb` e' `1`;
- l'`LSB` e' `11110000`;
- l'`MSB` e' `10010011`.

**Sistemi numerici posizionali**: un sistema numerico posizionale e' un sistema in cui ogni cifra del numero ha un peso specifico basato sulla sua posizione nel numero stesso. Esistono quattro sistemi numerici posizionali particolarmente importanti in informatica:

- **Sistema binario**: composto da sole due cifre, `1` e `0`.
- **Sistema ottale**: composto da otto cifre, da `0` a `7`.
- **Sistema decimale**: il piu' comune per gli esseri umani, composto da dieci cifre, da `0` a `9`.
- **Sistema esadecimale**: composto da sedici cifre, da `0` a `9` e da `A` (o `a`) a `F` (o `f`). Le cifre da `A` a `F` rappresentano i numeri da `10` a `15` nel sistema decimale.

Per comprendere un sistema numerico posizionale, consideriamo il seguente numero decimale:

```text
1236
```

E' composto da quattro cifre, da sinistra a destra: `1`, `2`, `3` e `6`. La base di un sistema numerico posizionale e' il numero di cifre che esso puo' usare: nel nostro caso la base e' `10`. La posizione parte da `0`, cioe' la prima cifra a destra, e aumenta di uno man mano che ci si sposta da destra verso sinistra. Nel nostro esempio le posizioni sono:

```text
6 in posizione 0
3 in posizione 1
2 in posizione 2
1 in posizione 3
```

In generale, un numero composto da `N` cifre ha posizioni che vanno da `0` a `N - 1`. Come si puo' calcolare il peso associato a ogni cifra di un numero? Si usa questa regola:

$$
D \cdot B^P
$$

Dove:

- `D` e' la cifra, nel sistema decimale un numero tra `0` e `9`;
- `B` e' la base, nel sistema decimale `10`;
- `P` e' la posizione della cifra `D`, che in un numero di `N` cifre puo' andare da `0` a `N - 1`.

Quindi, il peso di ogni cifra decimale nel nostro esempio e':

```text
6 * 10^0 = 6 * 1 = 6
3 * 10^1 = 3 * 10 = 30
2 * 10^2 = 2 * 100 = 200
1 * 10^3 = 1 * 1000 = 1000
```

Se sommi tutti i pesi, ottieni il numero originale:

```text
6 + 30 + 200 + 1000 = 1236
```

Lo stesso vale per il sistema binario. Se prendiamo il seguente numero binario:

```text
1010
```

La base `B` e' `2`, e le posizioni di ogni cifra, `1` oppure `0`, sono:

```text
0 in posizione 0
1 in posizione 1
0 in posizione 2
1 in posizione 3
```

Possiamo calcolare il peso di ogni posizione con la stessa regola, `D * B^P`:

```text
0 * 2^0 = 0 * 1 = 0
1 * 2^1 = 1 * 2 = 2
0 * 2^2 = 0 * 4 = 0
1 * 2^3 = 1 * 8 = 8
```

E possiamo verificare che tutti i pesi siano corretti sommando i vari contributi:

```text
0 + 2 + 0 + 8 = 10
```

`10` in decimale e' equivalente a `1010` in binario.

**Conversione da binario a decimale**: questa operazione converte un numero espresso nel sistema numerico posizionale binario in un numero espresso nel sistema numerico posizionale decimale.

```text
Binario: 1010
Decimale: ?

Conversione binario-decimale:
1010 = (1 * 2^3) + (0 * 2^2) + (1 * 2^1) + (0 * 2^0) = 8 + 0 + 2 + 0 = 10

Binario: 1010
Decimale: 10
```

**Conversione da decimale a binario**: questa operazione converte un numero espresso nel sistema numerico posizionale decimale in un numero espresso nel sistema numerico posizionale binario.

```text
Decimale: 10
Binario: ?

Conversione decimale-binario:
10 / 2 = 5, resto 0 <- questo e' l'lsb (least significant bit)
5 / 2 = 2, resto 1
2 / 2 = 1, resto 0
1 / 2 = 0, resto 1 <- questo e' l'msb (most significant bit)

Decimale: 10
Binario: 1010
```

**Conversione da binario a ottale**: questa operazione converte un numero espresso nel sistema numerico posizionale binario in un numero espresso nel sistema numerico posizionale ottale.

```text
Binario: 1000 (con gruppi: 001 000)
Ottale: ?

Conversione binario-ottale:
000 in binario e' 0 nel sistema numerico ottale
001 in binario e' 1 nel sistema numerico ottale

Binario: 001000
Ottale: 10
```

Questa conversione e' possibile perche' esiste una corrispondenza diretta tra ogni gruppo di tre cifre binarie e ogni cifra ottale. Le corrispondenze sono:

| Cifre binarie | Cifra ottale |
| --- | --- |
| 000 | 0 |
| 001 | 1 |
| 010 | 2 |
| 011 | 3 |
| 100 | 4 |
| 101 | 5 |
| 110 | 6 |
| 111 | 7 |

**Conversione da ottale a binario**: questa operazione converte un numero espresso nel sistema numerico posizionale ottale in un numero espresso nel sistema numerico posizionale binario.

```text
Ottale: 174
Binario: ?

Conversione ottale-binario:
4 in ottale e' 100 in binario
7 in ottale e' 111 in binario
1 in ottale e' 001 (oppure 1) in binario

Ottale: 174
Binario: 001111100, oppure 1111100
```

Questa conversione e' possibile perche' esiste una corrispondenza diretta tra ogni gruppo di tre cifre binarie e ogni cifra ottale. Le corrispondenze sono:

| Cifre binarie | Cifra ottale |
| --- | --- |
| 000 | 0 |
| 001 | 1 |
| 010 | 2 |
| 011 | 3 |
| 100 | 4 |
| 101 | 5 |
| 110 | 6 |
| 111 | 7 |

**Conversione da binario a esadecimale**: questa operazione converte un numero espresso nel sistema numerico posizionale binario in un numero espresso nel sistema numerico posizionale esadecimale.

```text
Binario: 1111 1010 0000 0010
Esadecimale: ?

Conversione binario-esadecimale:
0010 in binario e' 2 in esadecimale
0000 in binario e' 0 in esadecimale
1010 in binario e' 10 in decimale, cioe' A in esadecimale
1111 in binario e' 15 in decimale, cioe' F in esadecimale

Binario: 1111 1010 0000 0010
Esadecimale: FA02
```

Questa conversione e' possibile perche' esiste una corrispondenza diretta tra ogni gruppo di quattro cifre binarie e ogni cifra esadecimale. Le corrispondenze sono:

| Cifre binarie | Cifra esadecimale | Cifra decimale |
| --- | --- | --- |
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |
| 1010 | A (o a) | 10 |
| 1011 | B (o b) | 11 |
| 1100 | C (o c) | 12 |
| 1101 | D (o d) | 13 |
| 1110 | E (o e) | 14 |
| 1111 | F (o f) | 15 |

**Conversione da esadecimale a binario**: questa operazione converte un numero espresso nel sistema numerico posizionale esadecimale in un numero espresso nel sistema numerico posizionale binario.

```text
Esadecimale: FFC8
Binario: ?

Conversione esadecimale-binario:
8 in esadecimale e' 8 in decimale, cioe' 1000 in binario
C in esadecimale e' 12 in decimale, cioe' 1100 in binario
F in esadecimale e' 15 in decimale, cioe' 1111 in binario
F in esadecimale e' 15 in decimale, cioe' 1111 in binario

Esadecimale: FFC8
Binario: 1111 1111 1100 1000
```

Questa conversione e' possibile perche' esiste una corrispondenza diretta tra ogni gruppo di quattro cifre binarie e ogni cifra esadecimale. Le corrispondenze sono:

| Cifre binarie | Cifra esadecimale | Cifra decimale |
| --- | --- | --- |
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |
| 1010 | A (o a) | 10 |
| 1011 | B (o b) | 11 |
| 1100 | C (o c) | 12 |
| 1101 | D (o d) | 13 |
| 1110 | E (o e) | 14 |
| 1111 | F (o f) | 15 |

**Somma binaria**: la somma tra due numeri binari e' una delle operazioni piu' comuni eseguite da un sistema digitale o da una CPU. La somma di due numeri binari segue le stesse regole della somma tra due numeri decimali. Ecco un esempio:

```text
A: 1101
B: 0101

A   1 1 0 1 +
B   0 1 0 1 =
--------------

Passo 1:
1 + 1 = 0 con riporto

        1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
           0

Passo 2:
1 + 0 + 0 = 1 senza riporto

        1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
        1 0

Passo 3:
1 + 1 = 0 con riporto

    1   1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
      0 1 0

Passo 4:
1 + 1 + 0 = 0 con riporto

    1   1
A   1 1 0 1 +
B   0 1 0 1 =
--------------
  1 0  0 1 0

Risultato: 10010
```

**Complemento a 1 binario**: il complemento a 1 e' un'operazione binaria in cui ogni cifra binaria assume il valore inverso rispetto a quello originario. Se una cifra e' `1`, viene convertita in `0`; viceversa, se una cifra e' `0`, viene convertita in `1`. Ecco un esempio:

```text
Binario:           10 10 00 11
Complemento a 1:   01 01 11 00
```

L'operazione di complemento a 1 e' molto utile per rappresentare numeri negativi nella rappresentazione modulo e segno all'interno della memoria di un sistema digitale. Analizzeremo le varie tecniche di codifica dei numeri nel paragrafo successivo.

**Complemento a 2 binario**: il complemento a 2 e' un'operazione binaria in cui ogni cifra binaria viene invertita e, dopo che tutte le cifre sono state cambiate, si aggiunge 1 al risultato. Il complemento a 2 consiste in due passaggi:

1. calcolare il complemento a 1 del numero;
2. aggiungere 1 al complemento a 1 del numero: questo e' il complemento a 2.

Ecco un esempio:

```text
Binario:           10 10 00 11

Passo 1:
Complemento a 1:   01 01 11 00

Passo 2:
Aggiungi 1:        01 01 11 00 +
                   00 00 00 01 =
                   -------------
                   01 01 11 01
```

L'operazione di complemento a 2 e' molto utile per rappresentare numeri negativi nella rappresentazione in complemento a 2 all'interno della memoria di un sistema digitale. Analizzeremo le varie tecniche di codifica dei numeri nel paragrafo successivo.

**Prodotto binario**: il prodotto tra due numeri binari e' una delle operazioni piu' comuni eseguite da un sistema digitale o da una CPU. Il prodotto di due numeri binari segue le stesse regole del prodotto tra due numeri decimali. Ecco un esempio:

```text
A: 1101
B: 0101

A   1 1 0 1 +
B   0 1 0 1 =
--------------

Passo 1:
Moltiplica 1 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1

Passo 2:
Moltiplica 0 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0

Passo 3:
Moltiplica 1 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1

Passo 4:
Moltiplica 0 * 1101

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1
  0 0 0 0

Passo 5:
Somma di tutti i risultati parziali

A       1 1 0 1 +
B       0 1 0 1 =
-----------------
        1 1 0 1
      0 0 0 0
    1 1 0 1
  0 0 0 0
-----------------
  1 0 0 0 0 0 1

Risultato: 1000001
```

### 00.03. Rappresentazione dei dati

**Codifica dei numeri naturali (interi senza segno)**: la codifica binaria e' normalmente usata per rappresentare numeri naturali, cioe' interi positivi incluso lo zero, all'interno della memoria di un computer. Tutti i bit sono riservati a rappresentare il modulo del numero. Con `N` bit e' possibile rappresentare tutti i numeri compresi tra `0` e `2^N - 1`, per un totale di `2^N` valori possibili. Gli interi positivi sono anche chiamati numeri senza segno, perche' non esiste un bit dedicato a tracciare il segno, cioe' se il numero sia positivo o negativo. I moderni sistemi digitali, con architetture x32 e x64, possono rappresentare interi senza segno con 32 o 64 bit, o anche di piu', per esempio 128 o 256. Linguaggi di programmazione come Python, per esempio, permettono allo sviluppatore di memorizzare interi senza segno, o unsigned integers, con dimensione arbitraria, in base alla disponibilita' di memoria.

Questa e' la retta dei numeri naturali rappresentabile con `3` bit nella codifica binaria:

```text
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimale:       0     1     2     3     4     5     6     7
Binario:        000   001   010   011   100   101   110   111
```

**Codifica dei numeri relativi (interi con segno) con complemento a 1**: la codifica in complemento a 1 e' normalmente usata per rappresentare numeri relativi, cioe' interi con segno incluso lo zero, all'interno della memoria di un computer. Gli interi con segno sono anche chiamati signed integers. Con `N` bit, `N - 1` bit sono riservati a rappresentare il modulo del numero e l'`msb`, cioe' il bit piu' significativo, e' usato per rappresentare il segno: `0` se il numero e' positivo, `1` se il numero e' negativo. Con `N` bit e' possibile rappresentare:

- tutti gli interi positivi tra `+0` e `+2^(N - 1) - 1`;
- tutti gli interi negativi tra `-0` e `-2^(N - 1) + 1`.

Perche' `2^(N - 1)` e non `2^N`? Perche' un bit e' riservato al segno. Il complemento a 1 e' una codifica particolare, perche' esistono due rappresentazioni dello zero: `-0` e' lo zero negativo e `+0` e' lo zero positivo, ma entrambi rappresentano lo stesso numero, cioe' zero. Inoltre, somme e prodotti tra due o piu' numeri codificati in complemento a 1 sono difficili da elaborare o calcolare. Nota che, anche nella codifica in complemento a 1, essendoci un bit dedicato al segno, possiamo comunque rappresentare `2^N` valori differenti, anche se lo zero ha due rappresentazioni, quindi in realta' `2^N - 1` valori distinti.

Questa e' la retta dei numeri relativi rappresentabile con `3` bit nella codifica in complemento a 1:

```text
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimale:       -3    -2    -1    -0    +0    +1    +2    +3
Binario:        111   110   101   100   000   001   010   011
```

**Codifica dei numeri relativi (interi con segno) con complemento a 2**: la codifica in complemento a 2 e' normalmente usata per rappresentare numeri relativi, cioe' interi con segno incluso lo zero, all'interno della memoria di un computer. Gli interi con segno sono anche chiamati signed integers. Con `N` bit, `N - 1` bit sono riservati a rappresentare il modulo del numero e l'`msb`, cioe' il bit piu' significativo, e' usato per rappresentare il segno: `0` se il numero e' positivo, `1` se il numero e' negativo. Con `N` bit e' possibile rappresentare:

- tutti gli interi positivi tra `+0` e `+2^(N - 1) - 1`;
- tutti gli interi negativi tra `-0` e `-2^(N - 1)`.

Perche' `2^(N - 1)` e non `2^N`? Perche' un bit e' riservato al segno. Un'altra cosa da considerare e' che con la codifica in complemento a 2 dei numeri relativi si puo' rappresentare un numero negativo in piu' rispetto ai numeri positivi, poiche' questa codifica elimina la doppia rappresentazione dello zero: tutti i bit a `0` sono l'unica rappresentazione possibile di questo numero. Questo rende la codifica meno strana e piu' coerente. Per esempio, la codifica in complemento a 2 con `4` bit ha una e una sola rappresentazione dello zero: tutti i bit a `0`, cioe' `0000`. La rappresentazione dello zero e' unica nella codifica in complemento a 2. Somme e prodotti tra due o piu' numeri codificati in complemento a 2 sono molto semplici da elaborare, perche' sia la somma sia il prodotto possono essere eseguiti come per i numeri binari. Nota che, anche con la codifica in complemento a 2, c'e' sempre un bit di segno, ma possiamo comunque rappresentare `2^N` valori differenti.

Questa e' la retta dei numeri relativi rappresentabile con `3` bit nella codifica in complemento a 2:

```text
                |-----|-----|-----|-----|-----|-----|-----|----->
Decimale:       -4    -3    -2    -1    +0    +1    +2    +3
Binario:        100   101   110   111   000   001   010   011
```

Come puoi vedere osservando la retta, ecco alcune considerazioni:

- `-1` ha tutti i bit posti a `1`, compreso il bit di segno;
- il numero piu' piccolo, `-4` nel caso del complemento a 2 con `3` bit, ha tutti i bit posti a `0`, tranne il bit di segno che vale `1`;
- il numero piu' grande, `+3` nel caso del complemento a 2 con `3` bit, ha tutti i bit posti a `1`, tranne il bit di segno che vale `0`;
- `0` ha una e una sola rappresentazione, con tutti i bit posti a `0`.

**Codifica dei numeri decimali (numeri floating-point) con IEEE 754**: IEEE 754, dove IEEE e' l'acronimo di *Institute of Electrical and Electronics Engineers*, e' lo standard piu' comune usato per rappresentare numeri decimali in un sistema digitale. I numeri decimali sono anche noti come numeri floating-point. Originariamente stabilito nel 1985, IEEE 754 definisce come debba essere rappresentato un numero floating-point con una certa precisione e come debba funzionare l'aritmetica tra due o piu' numeri floating-point in un sistema digitale. IEEE 754 definisce i vari formati, i formati di interscambio, le regole di arrotondamento e varie operazioni aritmetiche, inclusi somma e prodotto. Lo standard definisce anche la gestione delle eccezioni, come la divisione per `0`. L'ultimo aggiornamento di IEEE 754 e' avvenuto nel 2020 da parte dell'ISO ed e' chiamato ISO/IEC 60559:2020.

Prima di analizzare lo standard IEEE 754, parliamo della notazione scientifica, o esponenziale. Questa notazione segue la regola:

$$
M \cdot B^N
$$

Dove:

- `M` e' chiamata mantissa;
- `B` e' la base del sistema numerico posizionale usato per rappresentare il numero, per il sistema binario `B = 2`, per il sistema decimale `B = 10`;
- `N` e' chiamato esponente.

La notazione precedente e' spesso abbreviata come `MeN` oppure `MEN`. Il numero decimale e' il risultato dell'operazione `M * B^N`.

Un numero floating-point conforme allo standard IEEE 754 puo' avere formati diversi; i tre formati piu' usati sono:

- **Single precision floating-point**: usa 32 bit, cioe' 4 byte, organizzati in questo modo:
  - `S`: `1` bit per il segno, detto *sign bit*. Vale `1` se la mantissa e' negativa, `0` se la mantissa e' positiva.
  - `M`: `23` bit per la mantissa. La mantissa e' la parte di un numero in notazione scientifica, o di un numero floating-point, costituita dalle sue cifre significative. Una mantissa e' detta normalizzata quando ha un solo `1` a sinistra della virgola.
  - `E`: `8` bit per l'esponente. L'esponente e' il numero per cui la mantissa deve essere moltiplicata. Questo numero compare come esponente della base del numero rappresentato, `2` nel caso del sistema binario e `10` nel caso del sistema decimale.
- **Double precision floating-point**: usa 64 bit, cioe' 8 byte, organizzati in questo modo:
  - `S`: `1` bit per il segno, detto *sign bit*. Vale `1` se la mantissa e' negativa, `0` se la mantissa e' positiva.
  - `M`: `52` bit per la mantissa. La mantissa e' la parte di un numero in notazione scientifica, o di un numero floating-point, costituita dalle sue cifre significative. Una mantissa e' detta normalizzata quando ha un solo `1` a sinistra della virgola.
  - `E`: `11` bit per l'esponente. L'esponente e' il numero per cui la mantissa deve essere moltiplicata. Questo numero compare come esponente della base del numero rappresentato, `2` nel caso del sistema binario e `10` nel caso del sistema decimale.
- **Quadruple precision floating-point**: usa 128 bit, cioe' 16 byte, organizzati in questo modo:
  - `S`: `1` bit per il segno, detto *sign bit*. Vale `1` se la mantissa e' negativa, `0` se la mantissa e' positiva.
  - `M`: `113` bit per la mantissa. La mantissa e' la parte di un numero in notazione scientifica, o di un numero floating-point, costituita dalle sue cifre significative. Una mantissa e' detta normalizzata quando ha un solo `1` a sinistra della virgola.
  - `E`: `15` bit per l'esponente. L'esponente e' il numero per cui la mantissa deve essere moltiplicata. Questo numero compare come esponente della base del numero rappresentato, `2` nel caso del sistema binario e `10` nel caso del sistema decimale.

Nello standard IEEE 754 alcuni valori sono particolari:

- il numero `0` e' rappresentato con tutti i bit di `M` posti a `0` e tutti i bit di `E` posti a `0`;
- la quantita' `Infinity` e' rappresentata con tutti i bit di `M` posti a `0` e tutti i bit di `E` posti a `1`. Questa quantita' rappresenta tipicamente un overflow, perche' i bit non sono sufficienti a rappresentare il risultato oppure il numero;
- il caso `NaN`, *Not a Number*, e' rappresentato con `M` diverso da `0` e tutti i bit di `E` posti a `1`. Questo valore rappresenta un errore durante un calcolo;
- una mantissa denormalizzata ha `M` diverso da `0` e l'esponente `E` con tutti i bit posti a `0`. In questo caso il numero non possiede il bit iniziale implicito uguale a uno prima del punto binario.

**ASCII ed EASCII**: ASCII, *American Standard Code for Information Interchange*, e' uno standard a `7` bit creato nel 1963 dall'ANSI, *American National Standards Institute*, per rappresentare un insieme di `95` caratteri stampabili, focalizzati sulla lingua inglese, e `33` caratteri di controllo, per un totale di `128` *code point*. Una stringa binaria ASCII valida consiste in `7` bit. Ogni combinazione di questi `7` bit e' un numero compreso tra `0` e `2^7 - 1`, cioe' tra `0` e `127`: ciascun numero e' chiamato *code point* e identifica in modo univoco uno specifico carattere. Una variante della codifica ASCII e' l'EASCII, *Extended ASCII*. Essa estende la lunghezza di un code point da `7` a `8` bit, quindi puo' rappresentare numeri tra `0` e `2^8 - 1`, cioe' tra `0` e `255`.

**Unicode e UTF-8**: Unicode, chiamato anche TUS, *The Unicode Standard*, e' uno standard di codifica dei caratteri mantenuto dal Unicode Consortium e progettato per supportare l'uso del testo in tutti i sistemi di scrittura del mondo. Unicode ha un numero molto elevato di *code point*. Unicode supporta caratteri cinesi, arabi, giapponesi, emoji, molti simboli matematici e culturali e molti altri tipi di caratteri. E' davvero una codifica universale che viene aggiornata continuamente dal Unicode Consortium.

Unicode definisce due metodi di mappatura: le codifiche UTF, *Unicode Transformation Format*, e le codifiche UCS, *Universal Coded Character Set*. Una codifica mappa, eventualmente su un sottoinsieme, l'insieme dei *code point* Unicode in sequenze di valori appartenenti a un intervallo di dimensione fissa, chiamati *code unit*. Tutte le codifiche UTF mappano i *code point* in una sequenza unica di byte. I numeri nei nomi delle codifiche indicano il numero di bit per *code unit*, nel caso delle codifiche UTF, oppure il numero di byte per *code unit*, nel caso delle codifiche UCS e di UTF-1. Le seguenti codifiche UTF sono usate da Unicode:

- **UTF-8** (*Unicode Transformation Format*, 8 bit): usa unita' da 8 bit per code point e ha massima compatibilita' con ASCII. Ogni code point puo' avere da una a quattro unita'. Questa e' la codifica piu' usata per i documenti web.
- **UTF-16** (*Unicode Transformation Format*, 16 bit): usa unita' da 16 bit per code point.
- **UTF-32** (*Unicode Transformation Format*, 32 bit): usa unita' da 32 bit per code point.

**Codifica lossless per immagini**: PNG, GIF e BMP sono formati di immagine che usano compressione lossless, oppure nessuna compressione nel caso di BMP, cioe' nessuna informazione viene persa durante la memorizzazione. PNG supporta immagini di alta qualita' e trasparenza con una compressione efficiente. GIF supporta fino a 256 colori e semplici animazioni. BMP memorizza tipicamente dati di pixel grezzi ed e' usato soprattutto per compatibilita' piu' che per efficienza di compressione.

**Codifica lossy per immagini**: JPEG e AVIF sono formati di immagine che usano compressione lossy per ridurre significativamente la dimensione dei file rimuovendo dettagli visivi meno percepibili. JPEG e' ampiamente usato per le fotografie grazie al buon compromesso tra compressione e prestazioni. AVIF offre una maggiore efficienza di compressione rispetto a JPEG con migliore qualita' d'immagine a dimensioni inferiori. Entrambi i formati sono comunemente usati per applicazioni web e multimediali.

**Codifica lossless per audio**: WAV e AIFF sono formati audio lossless che memorizzano segnali audio digitali non compressi o minimamente compressi. Conservano la qualita' originale della registrazione senza perdita di informazione. Questi formati sono comunemente usati negli ambienti professionali di editing e produzione audio. Tuttavia richiedono molto piu' spazio di archiviazione rispetto ai formati compressi.

**Codifica lossy per audio**: MP3 e AAC sono formati di compressione audio lossy progettati per ridurre la dimensione dei file eliminando informazioni sonore percepivamente meno importanti. MP3 e' uno dei formati audio piu' usati per la distribuzione musicale. AAC offre una qualita' sonora migliore di MP3 a bitrate simili ed e' ampiamente usato nei servizi di streaming e nei dispositivi mobili. Entrambi i formati sono ottimizzati per l'archiviazione e la trasmissione efficienti.

**Codifica lossless per video**: FLAC e Lagarith sono codec di compressione lossless che preservano i dati originali senza degradazione. FLAC e' usato principalmente per la compressione audio lossless, mentre Lagarith e' usato per la compressione video lossless nei flussi di lavoro di editing. Questi codec mantengono esattamente la qualita' originale ma producono file piu' grandi rispetto ai formati lossy. Sono comunemente usati per archiviazione a lungo termine e per l'elaborazione professionale dei media.

**Codifica lossy per video**: AVC, cioe' H.264, e MPEG-4 sono standard di compressione video lossy progettati per ridurre in modo efficiente la dimensione dei file video mantenendo una qualita' visiva accettabile. AVC e' ampiamente usato nelle piattaforme di streaming, nei dischi Blu-ray e nelle applicazioni di videoconferenza. MPEG-4 supporta la compressione multimediale per video, audio e contenuti interattivi. Questi codec consentono una trasmissione e una memorizzazione efficienti del video digitale.

### 00.04. Architettura di Von Neumann

**Calcolatore digitale**: un calcolatore digitale e' un sistema digitale, un dispositivo elettronico general purpose che elabora segnali digitali. Un segnale digitale e' un segnale che puo' assumere un insieme specifico di valori, cioe' valori discreti: un calcolatore digitale usa il sistema binario, con cifre binarie `0` e `1`, per rappresentare dati e istruzioni. Un calcolatore digitale opera con cifre `0` e `1` ed elabora uno o piu' programmi durante il proprio ciclo di vita. Esegue operazioni logiche e aritmetiche, come somma, confronto, AND logico, OR logico, NOT logico e altre. Un calcolatore digitale e' un dispositivo elettronico automatico: produce risultati accurati e ripetibili. Inoltre, un calcolatore digitale e' una macchina deterministica: gli stessi ingressi causano le stesse uscite. Un calcolatore digitale non puo' essere un sistema stocastico, cioe' basato sulla probabilita'.

**Programma e processo**: programma e processo hanno una relazione molto stretta, importante sia nel contesto dell'architettura dei calcolatori sia nel contesto dei sistemi operativi.

Un programma e' un insieme ordinato di istruzioni memorizzato nella memoria del sistema. Una memoria e' un dispositivo elettronico che permette al sistema digitale di eseguire uno o piu' programmi memorizzando ciascuno di essi tramite determinati principi fisici, che l'elettronica sfrutta per memorizzare bit. Ricorda che, in un computer e nei sistemi digitali in generale, tutto viene considerato come un bit oppure come un gruppo di bit. Un programma e' un'entita' statica normalmente memorizzata nella memoria secondaria, come HD, *Hard Disk*, oppure SSD, *Solid State Disk*. Un programma e' un insieme ordinato di istruzioni a livello macchina o ad alto livello memorizzate in memoria ed eseguite dalla CPU per realizzare un calcolo o un'operazione di controllo.

Un processo e' un'entita' dinamica memorizzata nella memoria principale, detta anche memoria centrale, del computer, che puo' assumere stati diversi durante la sua esecuzione. Un processo e' un programma in esecuzione: il programma e' il progetto, mentre il processo e' la sua istanza. Un programma puo' essere eseguito piu' volte. Inoltre, da un programma possono nascere piu' processi: sono piu' istanze dello stesso programma, ma descrivono esecuzioni differenti di esso. La CPU, il cervello del computer, esegue ogni istruzione del programma.

**Architettura di Von Neumann**: l'architettura di Von Neumann e' un progetto di calcolatore proposto nel 1945 dal matematico, fisico, informatico e ingegnere ungherese-statunitense John Von Neumann. Questa architettura e' caratterizzata da una memoria condivisa e da un bus di sistema condiviso sia per i dati sia per le istruzioni. La figura seguente mostra come e' organizzato un tipico sistema di Von Neumann:

<!-- da aggiungere -->
*In figura: un tipico sistema di Von Neumann*

Come si puo' vedere osservando la figura, la CPU e' composta da CU, *Control Unit*, ALU, *Arithmetic-Logic Unit*, e registri. Due dei registri piu' importanti sono PC, *Program Counter*, e IR, *Instruction Register*: il primo contiene un puntatore, cioe' un indirizzo di memoria, alla prossima istruzione da eseguire; il secondo contiene l'istruzione corrente nella fase di esecuzione. La CU e' un componente interno della CPU che controlla l'interfaccia della CPU con l'esterno e governa i segnali al suo interno. L'ALU e' il componente interno della CPU che esegue i calcoli, come AND logico, somma aritmetica e cosi' via.

L'architettura di Von Neumann e' il fondamento dei moderni sistemi digitali. Tutti i dispositivi moderni sono basati sull'architettura di Von Neumann. I concetti chiave di questa architettura sono:

- prima di tutto, sia i dati sia le istruzioni sono memorizzati nella stessa memoria, chiamata memoria principale o centrale. I programmi possono essere modificati esattamente come i dati. Esiste un unico spazio sia per i dati sia per le istruzioni. La memoria principale e' chiamata anche RAM, *Random Access Memory*, una memoria che fornisce accesso rapido e diretto a ogni cella o locazione di memoria;
- un bus di sistema permette la comunicazione diretta tra CPU e memoria, e viceversa, e tra la CPU e i vari dispositivi di I/O, e viceversa. Il bus di sistema e' la spina dorsale dell'intero sistema e ha tre tipi di bus:
  - **Address bus**: trasporta indirizzi di memoria, per operazioni di lettura e scrittura. Trasporta anche gli indirizzi di memorie esterne o di dispositivi che possono essere trattati come memorie;
  - **Data bus**: trasporta i dati che la CPU richiede oppure invia a una specifica periferica o alla memoria;
  - **Control bus**: trasporta segnali di controllo per governare le comunicazioni o per rilevare eventuali malfunzionamenti;
- la CPU preleva il programma dalla memoria, istruzione dopo istruzione, e lo esegue. La CPU esegue un'istruzione alla volta e usa il registro PC per tracciare la prossima istruzione da eseguire. Il PC e' un registro piccolo e veloce direttamente accessibile dall'ALU, il componente interno della CPU che esegue i calcoli. Le istruzioni vengono eseguite una dopo l'altra e l'esecuzione e' controllata dal registro PC.

Nei prossimi capitoli analizzeremo in dettaglio ogni componente dell'architettura di Von Neumann.

### 00.05. Calcolatore digitale moderno

**Linguaggio**: un linguaggio e' un insieme di parole chiave e di regole sintattiche e semantiche usate per rappresentare o comunicare informazioni tra due o piu' attori. Esistono due grandi categorie di linguaggi:

- **Linguaggi informali**: sono linguaggi usati per la comunicazione nella vita quotidiana che non seguono regole grammaticali rigide o una struttura perfettamente precisa, e il significato di ogni frase puo' dipendere dal contesto oppure dall'interpretazione. Un esempio di linguaggio naturale e' l'inglese, usato dagli esseri umani per comunicare.
- **Linguaggi formali**: sono linguaggi definiti da un insieme preciso di regole, simboli e grammatica, in cui ogni affermazione ha un significato esatto e non ambiguo, comunemente usati in matematica, informatica e linguaggi di programmazione. Un esempio di linguaggio formale e' il linguaggio di programmazione C.

I linguaggi formali possono essere suddivisi nelle seguenti classi:

- **Linguaggi di programmazione a livello macchina**: in realta' e' soltanto uno ed e' composto da due soli simboli, `0` e `1`. Il linguaggio macchina rappresenta la concretizzazione dei segnali digitali, che possono essere `high` oppure `low`.
- **Linguaggi di programmazione a basso livello**: tutti i linguaggi di programmazione ancora vicini alla macchina. Fondamentalmente questi linguaggi sono i vari linguaggi assembly, come l'assembly per architettura x86 oppure l'assembly ARMv7. Ogni architettura definisce il proprio insieme di istruzioni, detto anche ISA, *Instruction Set Architecture*, come vedremo nei prossimi capitoli.
- **Linguaggi di programmazione a medio livello**: tutti i linguaggi collocati tra quelli piu' vicini alla macchina e quelli piu' vicini all'essere umano. Un esempio e' il linguaggio C, che fornisce vari costrutti di basso livello, come i puntatori e diverse funzioni della libreria standard del C usate per manipolare direttamente la memoria principale. Anche C++ e Pascal possono essere considerati esempi di linguaggi di programmazione a medio livello.
- **Linguaggi di programmazione ad alto livello**: tutti i linguaggi di programmazione piu' vicini all'essere umano. Linguaggi come Java, PHP, Python e JavaScript sono tutti esempi di linguaggi di programmazione ad alto livello.

**Interpretazione**: e' il processo di traduzione ed esecuzione di un programma riga per riga a tempo di esecuzione, senza generare prima un file eseguibile separato. L'interprete e' il componente software o hardware che esegue l'interpretazione. Per esempio, un codice sorgente scritto nel linguaggio Java viene interpretato da un componente software chiamato JVM, *Java Virtual Machine*. In realta', Java e' un linguaggio pseudo-interpretato, perche' prima interviene un componente chiamato compilatore Java che compila il codice sorgente in un linguaggio intermedio noto come bytecode; in seguito la JVM interpreta direttamente il bytecode, riga per riga, convertendo ciascuna istruzione nel linguaggio assembly dell'architettura di destinazione. La figura seguente rappresenta un processo generale di interpretazione e il processo di interpretazione specifico del linguaggio Java:

<!-- da aggiungere -->
*In figura: il processo generico di interpretazione, a sinistra, e il processo di interpretazione del linguaggio Java, a destra*

**Compilazione**: e' il processo di traduzione dell'intero codice sorgente di un programma in codice macchina prima dell'esecuzione, producendo un file eseguibile che puo' essere eseguito in modo indipendente. Il compilatore e' il componente software o hardware che esegue la compilazione. Per esempio, un codice sorgente scritto nel linguaggio C viene compilato, da un compilatore C come GCC, *GNU C Compiler*, in un file eseguibile direttamente eseguibile dall'architettura di destinazione. La figura seguente rappresenta un processo generale di compilazione e il processo di compilazione specifico del linguaggio C:

<!-- da aggiungere -->
*In figura: il processo generico di compilazione, a sinistra, e il processo di compilazione del linguaggio C, a destra*

**Macchina virtuale e modello a livelli**: nell'architettura dei calcolatori, una VM, *Virtual Machine*, definisce un livello. Piu' precisamente, una VM e' un'emulazione software, hardware o ibrida di un sistema fisico di calcolo che fornisce un ambiente capace di eseguire programmi, scritti in uno specifico linguaggio direttamente eseguibile dalla VM, come se fosse una macchina reale. I moderni sistemi digitali consistono in un insieme di livelli differenti. Questa architettura e' chiamata *layered model*, oppure *multilevel machine model*, e possiede i seguenti elementi e caratteristiche:

- ogni livello vede tutti i livelli inferiori usando la propria astrazione;
- ogni livello puo' comunicare direttamente con i livelli adiacenti, cioe' il livello immediatamente superiore e quello immediatamente inferiore;
- ogni livello espone i propri servizi tramite API, *Application Programming Interfaces*. Un'API e' un'interfaccia, cioe' un confine condiviso o un punto di interazione tra due sistemi, componenti o entita', attraverso il quale essi comunicano e scambiano informazioni;
- ogni livello ha il proprio linguaggio, o i propri linguaggi. Il livello zero esegue direttamente programmi rappresentati in linguaggio macchina;
- i livelli piu' alti sono piu' vicini agli esseri umani;
- i livelli piu' bassi sono piu' vicini alla macchina.

Di seguito e' mostrata una rappresentazione del modello a livelli, seguito da tutti i moderni sistemi digitali:

<!-- da aggiungere -->
*In figura: il modello a livelli, cioe' il modello seguito dalle macchine multilivello*

**Macchine multilivello attuali**: le attuali macchine multilivello consistono di piu' livelli, uno sopra l'altro. Tutti i moderni sistemi digitali seguono il modello a livelli. I livelli che si possono trovare in una comune macchina multilivello sono:

- **Livello 0: livello della logica digitale**. Questo livello consiste di circuiti digitali di base come porte logiche, flip-flop e registri che implementano operazioni fondamentali usando segnali binari. Costituisce la base fisica su cui sono costruiti i livelli superiori del sistema di calcolo. Questa e' una rappresentazione astratta del livello della logica digitale:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello della logica digitale*

- **Livello 1: livello di microarchitettura**. Questo livello definisce come componenti hardware come ALU, registri, bus e unita' di controllo siano organizzati e interconnessi per eseguire istruzioni a livello macchina. Determina come il processore implementa internamente l'insieme di istruzioni. Questa e' una rappresentazione astratta del livello di microarchitettura:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello di microarchitettura*

- **Livello 2: livello di architettura, o livello ISA**. Questo livello specifica l'insieme delle istruzioni macchina, i registri, i tipi di dato e i modi di indirizzamento visibili ai programmatori e ai compilatori. Funziona come interfaccia tra hardware e software. Questa e' una rappresentazione astratta del livello di architettura:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello di architettura*

- **Livello 3: livello macchina del sistema operativo**. Questo livello fornisce una macchina estesa o virtuale gestendo le risorse hardware e offrendo servizi di sistema come controllo dei processi, gestione della memoria e gestione dell'input/output. Permette ai programmi di funzionare senza interagire direttamente con l'hardware. Questa e' una rappresentazione astratta del livello macchina del sistema operativo:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello macchina del sistema operativo*

- **Livello 4: livello assembler**. Questo livello usa il linguaggio assembly, che fornisce rappresentazioni simboliche delle istruzioni macchina e degli indirizzi per semplificare la programmazione a livello macchina. Un assembler traduce queste istruzioni simboliche in codice macchina eseguibile. Questa e' una rappresentazione astratta del livello assembler:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello assembler*

- **Livello 5: livello delle applicazioni e dei linguaggi orientati ai problemi**. Questo livello include linguaggi di programmazione ad alto livello come C, Java o Python che permettono ai programmatori di risolvere problemi usando una sintassi leggibile per l'essere umano. I programmi scritti in questi linguaggi vengono tradotti in istruzioni di livello inferiore prima dell'esecuzione. Questa e' una rappresentazione astratta del livello delle applicazioni e dei linguaggi orientati ai problemi:

<!-- da aggiungere -->
*In figura: una semplice rappresentazione del livello delle applicazioni e dei linguaggi orientati ai problemi*

### 00.06. Tipi di architetture

**CPU, processore, multiprocessore, single-core e multi-core**: usiamo il termine CPU, acronimo di *Central Processing Unit*, per riferirci a qualsiasi unita' di calcolo installata in un sistema digitale, dal punto di vista concettuale. Usiamo invece il termine processore per indicare un chip hardware, cioe' un dispositivo fisico con i propri pin, ingressi, uscite e alimentazione. Tipicamente, un processore contiene una sola CPU. Usiamo il termine multiprocessore sia per una scheda hardware contenente piu' processori, sia per una rete di calcolatori in cui i computer lavorano sullo stesso problema sfruttando il parallelismo reale. Infine, usiamo due termini per descrivere i processori moderni:

- **Single-core**: un processore, inteso come chip hardware, con una sola unita' di calcolo, cioe' una sola CPU. Si puo' pensare a un core come a una singola CPU.
- **Multi-core**: un processore, inteso come chip hardware, con piu' di una unita' di calcolo, cioe' piu' CPU.

La figura seguente mostra le differenze tra un processore single-core, un processore multi-core e un sistema multiprocessore:

<!-- da aggiungere -->
*In figura: differenza tra processore single-core, processore multi-core e sistema multiprocessore*

Nota che tutti i sistemi precedenti possono essere considerati una CPU. Un intero cluster di computer, per esempio, potrebbe rappresentare una singola CPU dal punto di vista logico e a un alto livello di astrazione.

**Modelli computazionali**: i moderni processori multi-core sono basati sull'esecuzione parallela. La tassonomia di Flynn e' una classificazione delle architetture dei calcolatori proposta da Michael J. Flynn nel 1966 e successivamente estesa nel 1972. La tassonomia di Flynn descrive come diversi tipi di architetture CPU possano eseguire uno o piu' programmi sfruttando il parallelismo reale. Questa classificazione e' divisa nelle seguenti categorie:

- **SISD** (*Single Instruction stream, Single Data stream*): fondamentalmente e' un sistema con una sola CPU. La CPU esegue una sola istruzione alla volta e ogni istruzione ha i propri dati.
- **SIMD** (*Single Instruction stream, Multiple Data stream*): una singola istruzione viene applicata simultaneamente a piu' flussi di dati differenti. Le istruzioni possono essere eseguite in sequenza, per esempio tramite pipeline, oppure in parallelo tramite piu' unita' funzionali. Esempi di questi sistemi sono gli array processor, o vector processor, i processori pipelined e i processori associativi.
- **MISD** (*Multiple Instruction stream, Single Data stream*): piu' istruzioni operano su un solo flusso di dati. Questa e' un'architettura poco comune che viene generalmente usata per tolleranza ai guasti.
- **MIMD** (*Multiple Instruction stream, Multiple Data stream*): piu' processori autonomi eseguono simultaneamente istruzioni differenti su dati differenti. Le architetture MIMD includono processori superscalari multi-core e sistemi distribuiti, che usano uno spazio di memoria condiviso oppure uno spazio di memoria distribuito.

Di seguito ci sono rappresentazioni logiche della tassonomia di Flynn:

<!-- da aggiungere -->
*In figura: rappresentazioni logiche di SISD, SIMD, MISD e MIMD*

**Tipi di computer**: in relazione al modo in cui vengono usati i dispositivi digitali, possiamo classificarli in:

- **Sistemi embedded**. I sistemi embedded sono calcolatori specializzati progettati per svolgere funzioni dedicate all'interno di dispositivi piu' grandi come elettrodomestici, veicoli o macchine industriali. Sono ottimizzati per affidabilita', basso consumo energetico e funzionamento in tempo reale piu' che per il calcolo general purpose.
- **PC, Personal Computer**. Un personal computer e' un sistema di calcolo general purpose destinato all'uso individuale, capace di eseguire una grande varieta' di applicazioni come videoscrittura, navigazione web e software multimediale. Include tipicamente un microprocessore, memoria, archiviazione e dispositivi di input/output.
- **Computer mobili e da gioco**. I computer mobili, come smartphone, tablet e console portatili, sono sistemi portabili progettati per connettivita' wireless e funzionamento efficiente dal punto di vista energetico. I computer da gioco, incluse le console, sono ottimizzati per grafica ad alte prestazioni e intrattenimento interattivo.
- **Workstation**. Le workstation sono computer ad alte prestazioni progettati per applicazioni tecniche o scientifiche come ingegneria, progettazione grafica e analisi dei dati. Offrono maggiore potenza di elaborazione, maggiore capacita' di memoria e maggiore affidabilita' rispetto ai personal computer standard.
- **Mainframe**. I mainframe sono grandi sistemi di calcolo potenti usati dalle organizzazioni per elaborare volumi enormi di dati e supportare molti utenti simultanei. Sono comunemente impiegati nel settore bancario, governativo e nelle grandi imprese per l'elaborazione di transazioni critiche.
- **Supercomputer**. I supercomputer sono i computer piu' potenti disponibili, progettati per eseguire calcoli estremamente complessi ad altissima velocita'. Sono usati per applicazioni come modellazione climatica, simulazioni scientifiche e ricerca avanzata.
- **Cluster**. I cluster sono gruppi di computer interconnessi che lavorano insieme come un unico sistema per migliorare prestazioni, affidabilita' o scalabilita'. Sono comunemente usati nel calcolo scientifico, nei servizi cloud e negli ambienti di elaborazione dati su larga scala.

**Architetture Von Neumann, Harvard e Harvard modificata**: l'architettura Von Neumann usa un unico spazio di memoria condiviso per memorizzare sia le istruzioni del programma sia i dati. Istruzioni e dati viaggiano sullo stesso bus, il che semplifica il progetto del sistema ma puo' creare una limitazione prestazionale nota come *Von Neumann bottleneck*, perche' puo' avvenire un solo trasferimento alla volta. La figura seguente mostra una rappresentazione molto semplice dell'architettura Von Neumann:

<!-- da aggiungere -->
*In figura: una rappresentazione molto semplificata dell'architettura Von Neumann*

L'architettura Harvard usa memorie separate e bus separati per istruzioni e dati, permettendo l'accesso simultaneo a entrambi. Questo migliora prestazioni ed efficienza ed e' comunemente usato nei sistemi embedded e nei digital signal processor. La figura seguente mostra una rappresentazione molto semplice dell'architettura Harvard:

<!-- da aggiungere -->
*In figura: una rappresentazione molto semplificata dell'architettura Harvard*

Infine, l'architettura Harvard modificata combina caratteristiche delle architetture Von Neumann e Harvard usando percorsi separati per istruzioni e dati all'interno del processore, mantenendo pero' una memoria principale condivisa. Questo progetto migliora le prestazioni mantenendo la flessibilita' ed e' ampiamente usato nei processori moderni. La figura seguente mostra una rappresentazione molto semplice dell'architettura Harvard modificata:

<!-- da aggiungere -->
*In figura: una rappresentazione molto semplificata dell'architettura Harvard modificata*

**Architetture di calcolo parallelo**: il calcolo parallelo e' un tipo di computazione in cui molti calcoli o processi vengono eseguiti simultaneamente. Problemi grandi possono spesso essere divisi in problemi piu' piccoli, che possono poi essere risolti nello stesso momento. Esistono diverse forme di calcolo parallelo: parallelismo a livello di bit, a livello di istruzione, di dati e di task. Il parallelismo e' stato a lungo impiegato nel calcolo ad alte prestazioni, ma ha suscitato un interesse ancora piu' ampio a causa dei vincoli fisici che impediscono di continuare ad aumentare indefinitamente la frequenza di clock. Esistono varie forme di calcolo parallelo:

- **Scalar processor**: un processore scalare esegue una sola istruzione su un solo dato alla volta, seguendo un modello di elaborazione sequenziale. E' il tipo tradizionale di processore usato in molti sistemi di base.
- **Array processor**: un array processor esegue la stessa operazione simultaneamente su piu' elementi di dato usando molte unita' di elaborazione che lavorano in parallelo. E' comunemente usato nel calcolo scientifico e nelle applicazioni che coinvolgono grandi insiemi di dati numerici.
- **Associative processor**: un processore associativo elabora i dati in base al contenuto anziche' in base all'indirizzo di memoria, consentendo il confronto parallelo di molti elementi di dato contemporaneamente. E' utile in applicazioni come ricerca in basi di dati, riconoscimento di pattern e intelligenza artificiale.
- **Sistemi multiprocessore**: un sistema multiprocessore contiene due o piu' processori che condividono la memoria e lavorano insieme per eseguire i compiti in modo piu' efficiente. Questi sistemi migliorano prestazioni, affidabilita' e velocita' di calcolo tramite elaborazione parallela.
- **Sistemi multi-core**: un sistema multi-core include piu' core di elaborazione integrati nello stesso chip, permettendo l'esecuzione simultanea di piu' compiti. Questa architettura migliora prestazioni ed efficienza energetica nei moderni computer e dispositivi mobili.

### 00.07. Storia delle macchine multilivello

**Nascita della microprogrammazione, anni 1940**: tra la fine degli anni 1940 e l'inizio degli anni 1950 fu introdotta la microprogrammazione, in particolare da Maurice Wilkes, come tecnica per semplificare il progetto dell'unita' di controllo della CPU. Invece di implementare una logica di controllo complessa interamente in hardware, le istruzioni venivano interpretate tramite sequenze di microistruzioni piu' semplici memorizzate in una memoria di controllo. Questo approccio rese la progettazione dei processori piu' flessibile e piu' facile da modificare o estendere. La microprogrammazione divenne ampiamente usata nei primi processori con insiemi di istruzioni complessi, cioe' CISC.

**Nascita del sistema operativo, anni 1960**: durante gli anni 1960 il sistema operativo emerse come livello software chiave tra hardware e utenti. Sistemi come *IBM OS/360* introdussero concetti come multiprogrammazione, job scheduling e gestione della memoria. I sistemi operativi resero possibile la condivisione efficiente di costose risorse di calcolo tra piu' utenti e piu' programmi. Questo segno' il passaggio dall'esecuzione di un solo programma ad ambienti software strutturati a livello di sistema.

**Espansione dell'ISA, anni 1970**: negli anni 1970 molti processori adottarono *Instruction Set Architecture* sempre piu' complesse, caratteristiche della filosofia di progetto CISC. I produttori ampliarono gli insiemi di istruzioni per supportare costrutti di programmazione di livello piu' alto e ridurre la dimensione dei programmi. Architetture come le prime famiglie *x86* esemplificano questa tendenza. Questa espansione mirava a spostare la complessita' dal software all'hardware tramite istruzioni macchina piu' ricche.

**Riduzione del ruolo della microprogrammazione, anni 1980**: a meta' degli anni 1980, la diffusione delle architetture RISC ridusse la dipendenza dalla microprogrammazione favorendo istruzioni piu' semplici eseguite direttamente da logica di controllo cablata. Progetti come *MIPS* e *SPARC* dimostrarono che insiemi di istruzioni semplificati potevano raggiungere prestazioni piu' elevate tramite pipeline efficienti. Sebbene la microprogrammazione non sia stata eliminata completamente, il suo ruolo diminui' in molti nuovi progetti di processore. Le CPU moderne usano ancora microcodice internamente per compatibilita' e gestione di istruzioni complesse.

**Legge di Moore**: formulata da Gordon Moore nel 1965, osservava che il numero di transistor su un circuito integrato raddoppia approssimativamente ogni 18-24 mesi. Questa tendenza ha guidato una crescita esponenziale delle prestazioni di calcolo riducendo allo stesso tempo il costo per transistor. Ha reso possibile lo sviluppo di processori, sistemi di memoria e dispositivi integrati sempre piu' complessi. Sebbene il suo ritmo si sia rallentato negli ultimi anni, la legge di Moore rimane un concetto centrale nell'evoluzione dei semiconduttori.

### 00.08. Storia delle architetture dei calcolatori

**Generazione zero, computer meccanici, 1642-1945**: la generazione zero include dispositivi di calcolo meccanici ed elettromeccanici costruiti prima dei computer elettronici. Esempi notevoli includono la *Pascaline* di Blaise Pascal, 1642, la *Analytical Engine* di Charles Babbage, concettuale ma fondamentale, e l'*Harvard Mark I*, 1944, un computer programmabile elettromeccanico. Queste macchine si basavano su ingranaggi, rele' e movimento meccanico anziche' su componenti elettronici. Esse stabilirono i principi di base del calcolo automatico e della computazione programmabile.

**Prima generazione, tubi a vuoto, 1945-1955**: la prima generazione di computer uso' tubi a vuoto per i circuiti e tamburi magnetici per la memoria. Macchine iconiche includono *ENIAC*, 1945, uno dei primi computer elettronici general purpose, *EDVAC*, che introdusse il concetto di programma memorizzato, e *UNIVAC I*, il primo computer commerciale negli Stati Uniti. Questi sistemi erano molto grandi, consumavano molta potenza e generavano molto calore. La programmazione veniva svolta usando linguaggio macchina e schede perforate.

**Seconda generazione, transistor, 1955-1965**: la seconda generazione sostitui' i tubi a vuoto con i transistor, rendendo i computer piu' piccoli, piu' veloci e piu' affidabili. Esempi importanti includono *IBM 1401*, ampiamente usato per applicazioni aziendali, e *IBM 7090*, progettato per il calcolo scientifico. La memoria a nuclei magnetici divenne standard e vennero introdotti linguaggi di programmazione di alto livello come FORTRAN e COBOL. Questa generazione segno' il passaggio verso sistemi di calcolo commerciali piu' pratici.

**Terza generazione, circuiti integrati, 1965-1985**: la terza generazione introdusse i circuiti integrati, consentendo di collocare piu' transistor su un singolo chip e migliorando notevolmente prestazioni e affidabilita'. Macchine rappresentative includono *IBM System/360*, che standardizzo' famiglie di computer compatibili, e *DEC PDP-8*, un influente minicomputer. I sistemi operativi divennero piu' avanzati, supportando multiprogrammazione e time-sharing. I computer divennero piu' accessibili per universita' e imprese.

**Quarta generazione, Very Large Scale Integration, 1985-oggi**: la quarta generazione e' caratterizzata da *Very Large Scale Integration*, VLSI, che ha reso possibile collocare da migliaia a milioni di transistor su un singolo chip e ha portato allo sviluppo dei microprocessori. Sistemi iconici includono *Intel 4004*, 1971, il primo microprocessore commerciale, e i primi personal computer come *Apple II* e *IBM PC*. Questa generazione ha reso il personal computing diffuso e ha ridotto drasticamente costi e dimensioni. Moderni desktop, laptop e server sono basati su questa tecnologia.

**Quinta generazione, computer a basso consumo e invisibili, 1990-oggi**: la quinta generazione si concentra su calcolo a basso consumo, altamente integrato e spesso invisibile, incorporato negli ambienti della vita quotidiana. Esempi includono smartphone basati su processori ARM, sistemi embedded in dispositivi IoT e computer indossabili come gli smartwatch. Progressi nel calcolo parallelo, nell'accelerazione per l'intelligenza artificiale e nel mobile computing caratterizzano questa era. Il calcolo e' diventato pervasivo, connesso in rete e integrato in modo quasi invisibile nella vita quotidiana.
