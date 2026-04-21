# 03. Livello logico digitale

### 03.01. Algebra booleana

**Algebra booleana**: l'algebra booleana e' un ramo della matematica usato per rappresentare e manipolare variabili logiche e operazioni logiche, in cui le variabili possono assumere solo due valori. Questi valori sono detti letterali booleani e possono essere assegnati alle variabili booleane.

**Variabile booleana**: e' una variabile che puo' assumere solo due valori possibili: `0` oppure `1`. Le variabili booleane sono gli elementi fondamentali dell'algebra booleana e dei circuiti logici digitali. Normalmente una variabile booleana e' indicata con una lettera maiuscola, come `A` oppure `B`.

**Letterale booleano**: e' un valore logico fisso che puo' essere solo `0` oppure `1`. In algebra booleana gli unici due valori utilizzabili sono `0`, detto anche `false` o `low`, e `1`, detto anche `true` o `high`.

**Relazione tra tensione e algebra booleana**: nella logica positiva un valore alto di tensione, normalmente `Vcc` oppure `Vdd`, viene considerato il valore logico `1`, mentre un valore basso di tensione, normalmente `GND`, viene considerato il valore logico `0`. I circuiti digitali hanno proprie specifiche sui livelli di tensione: per esempio, un circuito integrato potrebbe considerare `1` logico una tensione tra `2.5 V` e `5 V`, e `0` logico una tensione tra `0 V` e `1.5 V`. Questo dipende dalla tecnologia costruttiva.

**Logica positiva e logica negativa**: la logica positiva associa il valore logico `1` a una tensione alta e il valore logico `0` a una tensione bassa. La logica negativa fa l'opposto: associa `1` a una tensione bassa e `0` a una tensione alta.

**Insieme funzionalmente completo**: come in altri rami della matematica, in algebra booleana e' detto funzionalmente completo un insieme di operatori booleani che consente di esprimere qualunque espressione booleana. Un insieme di operazioni logiche e' funzionalmente completo se ogni espressione booleana puo' essere costruita usando solo quelle operazioni. L'insieme piu' comune e' `AND`, `OR`, `NOT`. Anche il solo operatore `NAND` e il solo operatore `NOR` costituiscono insiemi funzionalmente completi e sono molto usati nell'implementazione di circuiti digitali VLSI (*Very Large Scale Integration*).

**Espressione booleana**: e' un'espressione matematica usata in algebra booleana che combina letterali booleani, cioe' `0` o `1`, tramite operazioni logiche come `AND`, `OR` e `NOT`, producendo un risultato che e' ancora un valore booleano compreso tra `0` e `1`. Per esempio, la seguente e' un'espressione booleana:

```text
Y = AB + C(!D) + !(E + !(A))
```

Dove `A`, `B`, `C`, `D` ed `E` sono tutte variabili booleane. `!` e' l'operatore `NOT`, o invertitore; `+` e' l'operatore `OR`, cioe' disgiunzione logica; `x`, spesso non indicato, e' l'operatore `AND`, cioe' congiunzione logica. L'espressione precedente e' anche chiamata funzione booleana di cinque variabili booleane e puo' essere scritta anche cosi':

```text
Y = f(A, B, C, D, E) = AB + C(!D) + !(E + !(A))
```

Vedremo in dettaglio nei paragrafi seguenti come funzionano i principali operatori dell'algebra booleana.

**Tabella di verita'**: una tabella di verita' e' il modo principale per descrivere la relazione tra un insieme di variabili booleane e un'espressione booleana. Data un'espressione booleana, la sua tabella di verita' e' composta da un'intestazione e da un corpo. L'intestazione definisce almeno `N + 1` colonne, dove `N` e' il numero di variabili booleane presenti nell'espressione e la colonna rimanente contiene il risultato dell'espressione. Per esempio, consideriamo l'espressione seguente:

```text
Y = !(AB) + AB(!C) + A
```

In questo esempio compaiono tre variabili booleane: `A`, `B` e `C`. Quindi la tabella di verita' ha `3 + 1` colonne. Il corpo della tabella di verita' ha `2^N` righe: in questo caso, poiche' abbiamo tre variabili booleane, la tabella ha `2^3 = 8` righe. In ogni riga compare una specifica combinazione delle variabili booleane `A`, `B` e `C`. Normalmente le combinazioni seguono il conteggio binario e nel nostro esempio si parte da `000` e si arriva a `111`. La seguente e' la tabella di verita' dell'espressione precedente, senza i valori della colonna `Y`:

| A | B | C | Y |
|---|---|---|---|
| 0 | 0 | 0 |   |
| 0 | 0 | 1 |   |
| 0 | 1 | 0 |   |
| 0 | 1 | 1 |   |
| 1 | 0 | 0 |   |
| 1 | 0 | 1 |   |
| 1 | 1 | 0 |   |
| 1 | 1 | 1 |   |

Si noti che, in decimale, ogni combinazione varia da `0` a `2^N - 1`, nel nostro caso da `0` (`000`) a `7` (`111`). Quando si costruisce una tabella di verita' per un'espressione booleana complessa, e' utile aggiungere alcune colonne per seguire i valori delle sottoespressioni, come `!(AB)`, `AB(!C)` o `A`. Per esempio, possiamo aggiungere quattro altre colonne nella tabella precedente, ciascuna con valori intermedi:

| A | B | C | !C | AB | !(AB) | AB(!C) | Y |
|---|---|---|----|----|-------|--------|---|
| 0 | 0 | 0 | 1  | 0  |   1   |   0    |   |
| 0 | 0 | 1 | 0  | 0  |   1   |   0    |   |
| 0 | 1 | 0 | 1  | 0  |   1   |   0    |   |
| 0 | 1 | 1 | 0  | 0  |   1   |   0    |   |
| 1 | 0 | 0 | 1  | 0  |   1   |   0    |   |
| 1 | 0 | 1 | 0  | 0  |   1   |   0    |   |
| 1 | 1 | 0 | 1  | 1  |   0   |   1    |   |
| 1 | 1 | 1 | 0  | 1  |   0   |   0    |   |

Infine possiamo calcolare facilmente i valori per la colonna `Y`, cioe' il risultato dell'espressione booleana:

| A | B | C | !C | AB | !(AB) | AB(!C) | Y |
|---|---|---|----|----|-------|--------|---|
| 0 | 0 | 0 | 1  | 0  |   1   |   0    | 1 |
| 0 | 0 | 1 | 0  | 0  |   1   |   0    | 1 |
| 0 | 1 | 0 | 1  | 0  |   1   |   0    | 1 |
| 0 | 1 | 1 | 0  | 0  |   1   |   0    | 1 |
| 1 | 0 | 0 | 1  | 0  |   1   |   0    | 1 |
| 1 | 0 | 1 | 0  | 0  |   1   |   0    | 1 |
| 1 | 1 | 0 | 1  | 1  |   0   |   1    | 1 |
| 1 | 1 | 1 | 0  | 1  |   0   |   0    | 0 |

Come vedremo nei paragrafi successivi, questa espressione corrisponde a una forma NAND di tre variabili booleane: `A`, `B` e `C`.

**Operatore NOT**: l'operatore invertitore e' un operatore booleano a un solo operando che calcola il complemento dell'ingresso ed e' indicato con `!`. La tabella di verita' dell'operatore `NOT` e':

| A | !A |
|---|---|
| 0 | 1 |
| 1 | 0 |

**Operatore AND**: l'operatore di congiunzione logica e' un operatore booleano a due operandi che restituisce `1` solo se entrambi gli ingressi sono `1` ed e' indicato con `x`, spesso implicito, come nell'algebra classica. L'operatore `AND` segue la stessa regola del prodotto nell'algebra classica: qualunque valore moltiplicato per `0` restituisce `0`. La tabella di verita' dell'operatore `AND` e':

| A | B | AB |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**Operatore OR**: l'operatore di disgiunzione logica e' un operatore booleano a due operandi che restituisce `1` se almeno uno degli ingressi, oppure entrambi, valgono `1`; e' indicato con `+`. L'operatore `OR` segue una regola simile alla somma dell'algebra classica, con una differenza importante: `1 + 1` vale `1`, non `10`. La tabella di verita' dell'operatore `OR` e':

| A | B | A + B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

**Operatore NAND**: l'operatore `NAND` e' un operatore logico derivato a due operandi che restituisce `0` solo se entrambi gli ingressi sono `1`; e' indicato dall'espressione `!(AB)`. La tabella di verita' dell'operatore `NAND` e' la stessa dell'`AND`, tranne la colonna del risultato, che e' complementata:

| A | B | !(AB) |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**Operatore NOR**: l'operatore `NOR` e' un operatore logico derivato a due operandi che restituisce `1` solo se entrambi gli ingressi sono `0`; e' indicato dall'espressione `!(A + B)`. La tabella di verita' dell'operatore `NOR` e' la stessa dell'`OR`, tranne la colonna del risultato, che e' complementata:

| A | B | !(A + B) |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

**Operatore XOR**: l'operatore `XOR` e' un operatore logico derivato a due operandi che restituisce `1` solo se gli ingressi sono diversi, cioe' uno vale `0` e l'altro `1`. E' spesso indicato con la somma esclusiva. La sua tabella di verita' e':

| A | B | A xor B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**Operatore XNOR**: l'operatore `XNOR` e' un operatore logico derivato a due operandi che restituisce `1` solo se gli ingressi sono uguali, cioe' entrambi `0` oppure entrambi `1`. E' il complemento dello `XOR` ed e' indicato da `!(A xor B)`. La tabella di verita' dell'operatore `XNOR` e':

| A | B | !(A xor B) |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**Principi a una variabile**: in algebra booleana esistono alcune identita' fondamentali che coinvolgono una sola variabile. Sono molto utili per semplificare le espressioni:

```text
A + 0 = A
A * 1 = A
A + 1 = 1
A * 0 = 0
A + A = A
A * A = A
A + !A = 1
A * !A = 0
!!A = A
```

**Principi a due variabili**: anche con due variabili esistono proprieta' fondamentali di semplificazione e manipolazione. Le piu' importanti sono le proprieta' commutativa, associativa, distributiva e di assorbimento:

```text
A + B = B + A
AB = BA
(A + B) + C = A + (B + C)
(AB)C = A(BC)
A(B + C) = AB + AC
A + BC = (A + B)(A + C)
A + AB = A
A(A + B) = A
```

**Leggi di De Morgan**: le leggi di De Morgan permettono di trasformare somme in prodotti e prodotti in somme, complementando ogni operando. Sono fondamentali sia per la semplificazione algebrica sia per la trasformazione di reti logiche:

$$
!(A + B) = !A !B
$$

$$
!(AB) = !A + !B
$$

In modo piu' generale, il complemento di una somma diventa il prodotto dei complementi, mentre il complemento di un prodotto diventa la somma dei complementi.

**Mintermini e maxtermini**: un **mintermine** e' un prodotto `AND` di tutte le variabili della funzione, ciascuna presente una sola volta, in forma diretta o complementata, e vale `1` per una sola combinazione degli ingressi. Un **maxtermine** e' una somma `OR` di tutte le variabili della funzione, ciascuna presente una sola volta, in forma diretta o complementata, e vale `0` per una sola combinazione degli ingressi.

**Implicante e implicato**: un **implicante** e' un termine prodotto che copre una o piu' combinazioni di ingresso per cui la funzione vale `1`. Un **implicante primo** e' un implicante che non puo' piu' essere combinato con un altro implicante per eliminare una variabile senza cambiare la funzione. In modo duale, un **implicato** e' un termine somma logicamente implicato dalla funzione, e un **implicato primo** e' un implicato che non puo' essere ulteriormente semplificato.

**Prima forma canonica e SOP**: la prima forma canonica, detta anche `SOP` (*Sum of Products*), e' una somma di prodotti. Si costruisce prendendo tutti i mintermini per cui la funzione vale `1`. Se una funzione vale `1` per le righe `1`, `3` e `5`, allora possiamo scrivere:

$$
F = \Sigma m(1, 3, 5)
$$

Ogni mintermine contiene tutte le variabili della funzione.

**Seconda forma canonica e POS**: la seconda forma canonica, detta anche `POS` (*Product of Sums*), e' un prodotto di somme. Si costruisce prendendo tutti i maxtermini per cui la funzione vale `0`. Se una funzione vale `0` per le righe `0`, `2` e `7`, allora possiamo scrivere:

$$
F = \Pi M(0, 2, 7)
$$

Anche in questo caso ogni maxtermine contiene tutte le variabili della funzione.

**K-map a due variabili**: una mappa di Karnaugh a due variabili e' una tabella `2 x 2` usata per semplificare funzioni booleane. Le celle adiacenti rappresentano combinazioni che differiscono per una sola variabile. Raggruppando celle con valore `1` in blocchi di dimensione `1`, `2` oppure `4`, si ottiene una forma semplificata della funzione.

|    | B=0 | B=1 |
|----|-----|-----|
| A=0 | m0 | m1 |
| A=1 | m2 | m3 |

**K-map a tre variabili**: una mappa di Karnaugh a tre variabili e' tipicamente una tabella `2 x 4`, in cui una variabile controlla le righe e due variabili controllano le colonne in codice Gray, cioe' `00`, `01`, `11`, `10`. Anche qui le adiacenze rappresentano variazioni di una sola variabile.

| A | BC=00 | BC=01 | BC=11 | BC=10 |
|---|-------|-------|-------|-------|
| 0 |  m0   |  m1   |  m3   |  m2   |
| 1 |  m4   |  m5   |  m7   |  m6   |

**K-map a quattro variabili**: una mappa di Karnaugh a quattro variabili e' una tabella `4 x 4`, con righe e colonne ordinate in codice Gray. Permette di creare raggruppamenti di `1`, `2`, `4`, `8` o `16` celle per ottenere espressioni minimizzate.

| AB\CD | 00 | 01 | 11 | 10 |
|------|----|----|----|----|
| 00   | m0 | m1 | m3 | m2 |
| 01   | m4 | m5 | m7 | m6 |
| 11   | m12 | m13 | m15 | m14 |
| 10   | m8 | m9 | m11 | m10 |

**Valore X**: il simbolo `X` indica una condizione di *don't care*, cioe' un valore che puo' essere trattato come `0` oppure `1` a seconda di quale scelta semplifica meglio il circuito. Non e' un terzo valore booleano: e' un'informazione di progetto.

**Valore Z**: il simbolo `Z` indica uno stato di alta impedenza. Non e' un valore booleano e non appartiene all'algebra booleana classica. Dal punto di vista circuitale significa che un'uscita e' elettricamente disconnessa dalla linea e quindi non la pilota.

### 03.02. Porte logiche e tabelle di verita'

**Porta NOT**: la porta `NOT` e' una porta logica di base che produce l'inverso, o complemento, del proprio ingresso. Accetta un ingresso e produce un'uscita. La relazione booleana tra l'ingresso `A` e l'uscita `Y` e' `Y = !A`. La porta logica `NOT` ha la seguente tabella di verita':

| A | Y |
|---|---|
| 0 | 1 |
| 1 | 0 |

La porta `NOT` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica NOT con ingresso A e uscita Y*

**Porta BUF**: la porta `BUF`, abbreviazione di *buffer*, e' una porta logica di base che produce in uscita lo stesso valore logico del proprio ingresso. Accetta un ingresso e produce un'uscita. La relazione booleana tra l'ingresso `A` e l'uscita `Y` e' `Y = A`. Da un punto di vista puramente logico questa porta non introduce una trasformazione utile, ma dal punto di vista circuitale e' molto importante. La porta logica `BUF` ha la seguente tabella di verita':

| A | Y |
|---|---|
| 0 | 0 |
| 1 | 1 |

La porta `BUF` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica BUF con ingresso A e uscita Y*

Per quale motivo una porta `BUF` dovrebbe essere usata? Normalmente, nei circuiti logici digitali, la lunghezza di un collegamento e il rumore degradano lentamente il segnale digitale. La porta `BUF` e' molto utile per rigenerare il segnale in termini di tensione e corrente. Questa e' un'applicazione comune quando un segnale digitale deve essere distribuito a uno o piu' dispositivi o circuiti.

**Porta AND**: la porta `AND` e' una porta logica di base che produce la funzione logica `AND` dei propri ingressi. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = A x B`, spesso abbreviata in `Y = AB`, come nell'algebra classica. La porta logica `AND` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

La porta `AND` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica AND con ingressi A e B e uscita Y*

Una porta `AND` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `AND3` ha tipicamente un ritardo inferiore a una `AND8`. Ecco un esempio di una porta `AND4`:

<!-- da aggiungere -->
*In figura: la porta logica AND4 con quattro ingressi e uscita Y*

**Porta OR**: la porta `OR` e' una porta logica di base che produce la funzione logica `OR` dei propri ingressi. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = A + B`, dove la funzione `OR` e' rappresentata dall'operatore di somma, come nell'algebra classica. La porta logica `OR` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

La porta `OR` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica OR con ingressi A e B e uscita Y*

Una porta `OR` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `OR3` ha tipicamente un ritardo inferiore a una `OR8`. Ecco un esempio di una porta `OR4`:

<!-- da aggiungere -->
*In figura: la porta logica OR4 con quattro ingressi e uscita Y*

**Porta NAND**: la porta `NAND` e' una porta logica di base che produce il complemento della funzione `AND` dei propri ingressi. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = !(A x B)`, spesso abbreviata in `Y = !(AB)`. La porta logica `NAND` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

La porta `NAND` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica NAND con ingressi A e B e uscita Y*

Una porta `NAND` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `NAND3` ha tipicamente un ritardo inferiore a una `NAND8`. Ecco un esempio di una porta `NAND4`:

<!-- da aggiungere -->
*In figura: la porta logica NAND4 con quattro ingressi e uscita Y*

**Porta NOR**: la porta `NOR` e' una porta logica di base che produce il complemento della funzione `OR` dei propri ingressi. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = !(A + B)`. La porta logica `NOR` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

La porta `NOR` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica NOR con ingressi A e B e uscita Y*

Una porta `NOR` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `NOR3` ha tipicamente un ritardo inferiore a una `NOR8`. Ecco un esempio di una porta `NOR4`:

<!-- da aggiungere -->
*In figura: la porta logica NOR4 con quattro ingressi e uscita Y*

**Porta XOR**: la porta `XOR` (*eXclusive OR*) e' una porta logica di base che produce `1` in uscita solo se il numero di ingressi posti a `1` e' dispari. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = A xor B`. La porta logica `XOR` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

La porta `XOR` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica XOR con ingressi A e B e uscita Y*

Una porta `XOR` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `XOR3` ha tipicamente un ritardo inferiore a una `XOR8`. Ecco un esempio di una porta `XOR4`:

<!-- da aggiungere -->
*In figura: la porta logica XOR4 con quattro ingressi e uscita Y*

La porta `XOR` e' anche chiamata porta di diversita', perche' con due ingressi restituisce `1` solo se i due ingressi sono diversi.

**Porta XNOR**: la porta `XNOR` (*eXclusive NOT OR*) e' una porta logica di base che produce `1` in uscita solo se il numero di ingressi posti a `1` e' pari. La porta base accetta due ingressi e produce un'uscita. La relazione booleana tra gli ingressi `A`, `B` e l'uscita `Y` e' `Y = !(A xor B)`. La porta logica `XNOR` ha la seguente tabella di verita':

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

La porta `XNOR` e' rappresentata nella figura seguente:

<!-- da aggiungere -->
*In figura: la porta logica XNOR con ingressi A e B e uscita Y*

Una porta `XNOR` puo' avere piu' di due ingressi, ma il ritardo introdotto dalla sua circuiteria dipende in modo crescente dal numero di ingressi accettati. Per esempio, una porta `XNOR3` ha tipicamente un ritardo inferiore a una `XNOR8`. Ecco un esempio di una porta `XNOR4`:

<!-- da aggiungere -->
*In figura: la porta logica XNOR4 con quattro ingressi e uscita Y*

La porta `XNOR` e' anche chiamata porta di uguaglianza, perche' con due ingressi restituisce `1` solo se i due ingressi sono uguali.

**Porta TRI**: la porta `TRI`, cioe' `TRIstate`, e' una porta particolare che ha un ingresso dati `A`, un segnale di controllo `E`, chiamato enable, e un'uscita `Y`. Il segnale `E` puo' essere attivo alto o attivo basso: in entrambi i casi, quando e' attivo, il segnale `A` attraversa la porta `TRI` e l'uscita `Y` assume lo stesso valore di `A`. Se `E` non e' abilitato, l'uscita `Y` assume il valore `Z`: nei circuiti digitali il valore `Z` indica alta impedenza, cioe' uno stato flottante dell'uscita. La porta `TRI` ha la seguente tabella di verita', nel caso attivo alto:

| E | A | Y |
|---|---|---|
| 0 | 0 | Z |
| 0 | 1 | Z |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

La figura seguente rappresenta due tipi di porta `TRI`, attiva alta e attiva bassa:

<!-- da aggiungere -->
*In figura: a sinistra una porta TRI con E attivo alto, a destra una porta TRI con !E attivo basso*

Come la porta `BUF`, anche `TRI` viene usata per rigenerare un segnale digitale o per fornire un segnale pulito a uno o piu' circuiti digitali. In piu', `TRI` e' usata per abilitare o disabilitare una specifica porzione di circuito, come una parte di memoria centrale o alcune linee di I/O nelle architetture moderne.

### 03.03. Circuiti combinatori

**Mintermini e maxtermini**: un mintermine e' un prodotto, cioe' una combinazione `AND`, di tutte le variabili di una funzione booleana, ciascuna presente esattamente una volta in forma diretta o complementata, che vale `1` per una sola combinazione degli ingressi. Un maxtermine e' una somma, cioe' una combinazione `OR`, di tutte le variabili di una funzione booleana, ciascuna presente esattamente una volta in forma diretta o complementata, che vale `0` per una sola combinazione degli ingressi.

**Implicante e implicante primo**: un implicante e' un termine prodotto di una funzione booleana che implica il valore `1` della funzione per tutte le combinazioni di ingresso coperte da quel termine. Un implicante primo e' un implicante che non puo' essere combinato con un altro implicante per eliminare una variabile e rimanere comunque un implicante della funzione.

**Implicato e implicato primo**: un implicato e' un termine somma, cioe' una combinazione `OR` di letterali, che e' vero ogni volta che la funzione booleana e' vera, cioe' la funzione implica logicamente quel termine. Un implicato primo e' un implicato che non puo' essere ulteriormente semplificato rimuovendo letterali senza modificare la funzione.

**Circuito combinatorio**: un circuito detto combinatorio e' un circuito digitale, o rete digitale, in cui le uscite dipendono solo e soltanto dagli ingressi correnti. Un circuito combinatorio puo' avere zero, uno o piu' ingressi e zero, uno o piu' uscite. Le porte logiche analizzate nel paragrafo precedente sono tutti esempi dei piu' semplici circuiti combinatori. La figura seguente mostra un esempio di circuito combinatorio:

<!-- da aggiungere -->
*In figura: esempio di circuito combinatorio*

Le seguenti regole definiscono come una rete combinatoria possa essere implementata:

- Ogni elemento della rete e' combinatorio.
- Ogni nodo della rete e' un ingresso della rete oppure e' collegato a una sola uscita di un elemento della rete.
- Una rete combinatoria non contiene collegamenti ciclici.

La figura seguente mostra alcuni esempi di reti non combinatorie: la rete `(a)` non e' combinatoria perche' contiene un ciclo; la rete `(b)` non e' combinatoria perche' le uscite di due elementi diversi sono collegate allo stesso ingresso di un elemento combinatorio; la rete `(c)` non e' combinatoria, ma e' una particolare rete sequenziale, che analizzeremo piu' avanti.

**Prima forma canonica**: l'algebra booleana permette al progettista di descrivere completamente una rete combinatoria. La `FCF` (*First Canonical Form*), detta anche `SOP` (*Sum of Products*), consiste in una somma di prodotti, cioe' un `OR` di termini `AND`. Dato un circuito combinatorio, come quello mostrato nella figura seguente:

<!-- da aggiungere -->
*In figura: esempio di circuito combinatorio descrivibile con la forma SOP*

possiamo creare la tabella di verita' seguendo le stesse regole viste all'inizio del capitolo. La seguente tabella di verita' mostra la relazione tra gli ingressi `A`, `B`, `C` e l'uscita `Y`:

| A | B | C | Y | Mintermini |
|---|---|---|---|------------|
| 0 | 0 | 0 | 0 | m0 |
| 0 | 0 | 1 | 1 | m1 |
| 0 | 1 | 0 | 0 | m2 |
| 0 | 1 | 1 | 0 | m3 |
| 1 | 0 | 0 | 0 | m4 |
| 1 | 0 | 1 | 0 | m5 |
| 1 | 1 | 0 | 1 | m6 |
| 1 | 1 | 1 | 1 | m7 |

Il primo passo per creare una forma `SOP` del circuito combinatorio consiste nel considerare le righe della tabella di verita' in cui `Y = 1`. Le righe `1`, `6` e `7` sono quelle in cui `Y = 1`. Questo significa che consideriamo i seguenti mintermini: `m1`, `m6` e `m7`. Possiamo scrivere che l'uscita `Y` vale `1` quando almeno uno dei mintermini precedenti vale `1`:

```text
Y = f(A, B, C) = m1 + m6 + m7
```

Oppure, in modo equivalente:

```text
Y = f(A, B, C) = Sigma(m1, m6, m7)
```

Oppure ancora:

```text
Y = f(A, B, C) = Sigma(1, 6, 7)
```

Dove:

- il mintermine `m1` e' il prodotto `!(A)!(B)C`,
- il mintermine `m6` e' il prodotto `AB!(C)`,
- il mintermine `m7` e' il prodotto `ABC`.

La formula booleana precedente e' equivalente alla seguente:

```text
Y = !(A)!(B)C + AB!(C) + ABC
```

La figura seguente mostra il circuito combinatorio a due livelli descritto dalla formula precedente:

<!-- da aggiungere -->
*In figura: circuito combinatorio a due livelli descritto dalla formula `Y = !(A)!(B)C + AB!(C) + ABC`*

Si noti che per scrivere la forma `SOP` si prende ogni variabile booleana in forma diretta se vale `1` nella riga considerata, e in forma negata se vale `0`. La forma `SOP` e' un esempio di logica a due livelli: il primo livello e' un insieme di porte `AND`, il secondo livello e' una grande porta `OR` che accetta come ingressi tutti i mintermini.

**Seconda forma canonica**: l'algebra booleana permette al progettista di descrivere completamente una rete combinatoria anche con la `SCF` (*Second Canonical Form*), detta anche `POS` (*Product of Sums*), che consiste in un prodotto di somme, cioe' un `AND` di termini `OR`. Dato un circuito combinatorio, come quello mostrato nella figura seguente:

<!-- da aggiungere -->
*In figura: esempio di circuito combinatorio descrivibile con la forma POS*

possiamo creare la tabella di verita' seguendo le stesse regole viste all'inizio del capitolo. La tabella seguente mostra la relazione tra gli ingressi `A`, `B`, `C` e l'uscita `Y`:

| A | B | C | Y | Maxtermini |
|---|---|---|---|------------|
| 0 | 0 | 0 | 0 | M0 |
| 0 | 0 | 1 | 1 | M1 |
| 0 | 1 | 0 | 0 | M2 |
| 0 | 1 | 1 | 0 | M3 |
| 1 | 0 | 0 | 0 | M4 |
| 1 | 0 | 1 | 0 | M5 |
| 1 | 1 | 0 | 1 | M6 |
| 1 | 1 | 1 | 1 | M7 |

Il primo passo per creare una forma `POS` consiste nel considerare le righe della tabella di verita' in cui `Y = 0`. Le righe `0`, `2`, `3`, `4` e `5` sono le righe in cui `Y = 0`. Questo significa che consideriamo i seguenti maxtermini: `M0`, `M2`, `M3`, `M4` e `M5`. Possiamo scrivere che l'uscita `Y` vale `1` quando tutti i maxtermini precedenti valgono `1`:

```text
Y = f(A, B, C) = M0 * M2 * M3 * M4 * M5
```

Oppure, in modo equivalente:

```text
Y = f(A, B, C) = Pi(M0, M2, M3, M4, M5)
```

Oppure ancora:

```text
Y = f(A, B, C) = Pi(0, 2, 3, 4, 5)
```

Dove:

- il maxtermine `M0` e' la somma `A + B + C`,
- il maxtermine `M2` e' la somma `A + !(B) + C`,
- il maxtermine `M3` e' la somma `A + !(B) + !(C)`,
- il maxtermine `M4` e' la somma `!(A) + B + C`,
- il maxtermine `M5` e' la somma `!(A) + B + !(C)`.

La formula booleana precedente e' equivalente alla seguente:

```text
Y = (A + B + C)(A + !(B) + C)(A + !(B) + !(C))(!(A) + B + C)(!(A) + B + !(C))
```

La figura seguente mostra il circuito combinatorio a due livelli descritto dalla formula precedente:

<!-- da aggiungere -->
*In figura: circuito combinatorio a due livelli descritto dalla formula `Y = (A + B + C)(A + !(B) + C)(A + !(B) + !(C))(!(A) + B + C)(!(A) + B + !(C))`*

Si noti che per scrivere la forma `POS` si prende ogni variabile booleana in forma diretta se vale `0` nella riga considerata, e in forma negata se vale `1`, cioe' in modo opposto rispetto alla `SOP`. Anche la forma `POS` e' un esempio di logica a due livelli: il primo livello e' un insieme di porte `OR`, il secondo livello e' una grande porta `AND` che accetta come ingressi tutti i maxtermini.

**Implementazioni solo NAND e solo NOR**: i circuiti integrati piu' comuni e molti chip commerciali usano implementazioni basate solo su `NAND` oppure solo su `NOR`.

Un'implementazione solo `NAND` usa esclusivamente la porta `NAND` per implementare qualunque altra porta logica. La figura seguente mostra come le principali porte possano essere implementate usando la sola porta `NAND`:

<!-- da aggiungere -->
*In figura: la porta NAND usata per implementare le porte NOT, AND e OR*

Un'implementazione solo `NOR` usa esclusivamente la porta `NOR` per implementare qualunque altra porta logica. La figura seguente mostra come le principali porte possano essere implementate usando la sola porta `NOR`:

<!-- da aggiungere -->
*In figura: la porta NOR usata per implementare le porte NOT, AND e OR*

Sia le implementazioni solo `NAND` sia quelle solo `NOR` sono usate nei moderni circuiti integrati `VLSI`. Le porte `NAND` e `NOR` richiedono un numero ridotto di transistor rispetto ad altre implementazioni dirette: questa e' una delle ragioni principali per cui CPU, cache e altri chip moderni si basano su reti `NAND` o `NOR`.

**Circuiti logici multilivello**: un circuito logico multilivello e' un circuito combinatorio in cui almeno un ingresso attraversa piu' di due porte logiche prima di raggiungere l'uscita. La figura seguente mostra un esempio di circuito logico multilivello:

<!-- da aggiungere -->
*In figura: esempio di circuito logico multilivello*

**Condizioni di don't care**: sono combinazioni di ingresso per cui l'uscita di una funzione booleana non e' specificata oppure non e' rilevante per il funzionamento del circuito. In una tabella di verita' vengono solitamente rappresentate con `X`, il che significa che l'uscita puo' essere sia `0` sia `1`, a seconda di quale scelta semplifica meglio il circuito. Normalmente le condizioni di *don't care* compaiono quando alcune combinazioni di ingresso non si presentano mai nella pratica, oppure alcune combinazioni sono inutilizzate, oppure alcune uscite sono irrilevanti in certi stati. La figura seguente mostra come un circuito combinatorio possa essere ottimizzato usando condizioni di *don't care*:

<!-- da aggiungere -->
*In figura: come un circuito combinatorio puo' essere rappresentato e semplificato con condizioni di don't care*

A questo punto, nei circuiti combinatori e sequenziali, possiamo usare tre simboli:

- `0` e' tipicamente una tensione bassa, nella logica positiva.
- `1` e' tipicamente una tensione alta, nella logica positiva.
- `X` significa "qualunque valore" e rappresenta una condizione di *don't care* per una particolare variabile booleana.

**Stato di alta impedenza**: indicato con `Z`, rappresenta uno stato di alta impedenza, detto anche tristate, nei circuiti digitali, cioe' una condizione in cui l'uscita e' elettricamente disconnessa dal circuito. La figura seguente mostra una porta tristate, cioe' una porta logica con due ingressi e un'uscita:

<!-- da aggiungere -->
*In figura: la porta tristate, con A come ingresso dati, E come ingresso di controllo e Y come uscita dati*

Quando `E = 1`, la tristate e' trasparente e ogni valore di `A` viene propagato, con un piccolo ritardo, e rigenerato sull'uscita `Y`. Quando `E = 0`, la tristate e' opaca e `Y = Z`. Questo significa che l'uscita `Y` si trova in uno stato di alta impedenza. Si noti che `Z` non e' un valore logico, ma una condizione circuitale che indica che l'uscita e' elettricamente inattiva e non influenza la linea di segnale. Un'uscita `Z` significa che il pin di uscita del circuito digitale si comporta come un interruttore aperto.

**Ritardo**: in un circuito combinatorio esistono diversi tipi di ritardo.

Il **tempo di salita** (*rise time*) e' il tempo richiesto a un segnale per passare da un livello logico basso a un livello logico alto, tipicamente misurato tra il 10% e il 90% del valore finale della tensione. Descrive quanto rapidamente un segnale digitale passa da `0` a `1` ed e' un parametro importante delle porte logiche di base.

Il **tempo di discesa** (*fall time*) e' il tempo richiesto a un segnale per passare da un livello logico alto a un livello logico basso, tipicamente misurato tra il 90% e il 10% del valore iniziale della tensione. Descrive quanto rapidamente un segnale passa da `1` a `0`.

Il **ritardo di propagazione** (*propagation delay*) e' il tempo che intercorre tra una variazione all'ingresso di una porta logica o di un circuito e la corrispondente variazione all'uscita. Rappresenta il tempo di risposta del circuito ed e' di solito misurato tra i punti al 50% della transizione di tensione. Si indica con `tpd`.

Il **ritardo di contaminazione** (*contamination delay*) e' il tempo minimo dopo una variazione di ingresso a partire dal quale l'uscita puo' iniziare a cambiare. Rappresenta il piu' rapido effetto possibile di una transizione in ingresso sull'uscita. Si indica con `tcd`.

**Ritardi del cammino critico**: il ritardo di propagazione dell'intero circuito logico e' il massimo ritardo di cammino tra tutti i possibili percorsi ingresso-uscita di un circuito combinatorio. Determina il periodo minimo di clock e quindi la massima velocita' operativa del circuito. Il ritardo di propagazione di un circuito logico multilivello e' la somma dei ritardi di propagazione delle porte lungo il cammino piu' lungo, chiamato cammino critico. Per esempio, consideriamo il seguente circuito logico:

<!-- da aggiungere -->
*In figura: esempio di circuito combinatorio con cammino critico, usato per calcolare il ritardo di propagazione `tpd` del circuito*

Nel cammino critico abbiamo tre porte logiche: una `NOT`, una `AND` e una `OR`. Il ritardo di propagazione `tpd` del circuito e' la somma dei ritardi di propagazione di ciascuna porta logica:

- `tpdNOT` per la porta `NOT`,
- `tpdAND` per la porta `AND`,
- `tpdOR` per la porta `OR`.

Quindi il ritardo totale di propagazione, indicato con `tpd`, e':

```text
tpd = tpdNOT + tpdAND + tpdOR
```

Il ritardo di contaminazione dell'intero circuito logico e' invece il minimo ritardo di cammino tra il cambiamento degli ingressi e il cambiamento dell'uscita. Il ritardo di contaminazione di un circuito logico multilivello e' la somma dei ritardi di contaminazione delle porte lungo il cammino piu' corto, chiamato cammino minimo. Per esempio, consideriamo il seguente circuito logico:

<!-- da aggiungere -->
*In figura: esempio di circuito combinatorio con cammino minimo, usato per calcolare il ritardo di contaminazione `tcd` del circuito*

Nel cammino minimo abbiamo due porte logiche: una `NOT` e una `NAND`. Il ritardo di contaminazione `tcd` del circuito e' la somma dei ritardi di contaminazione di ciascuna porta logica:

- `tcdNOT` per la porta `NOT`,
- `tcdNAND` per la porta `NAND`.

Quindi il ritardo totale di contaminazione, indicato con `tcd`, e':

```text
tcd = tcdNOT + tcdNAND
```

### 03.04. Blocchi combinatori

**Half adder**: il *mezzo sommatore* e' un blocco combinatorio che somma due bit `A` e `B` e produce due uscite: la somma `S` e il riporto `Cout`. Le equazioni fondamentali sono:

$$
S = A xor B
$$

$$
C_{out} = AB
$$

Questo blocco non ha ingresso di riporto.

**Full adder**: il *sommatore completo* somma tre bit: `A`, `B` e il riporto in ingresso `Cin`. Produce la somma `S` e il riporto in uscita `Cout`. Le equazioni minime piu' usate sono:

$$
S = A xor B xor C_{in}
$$

$$
C_{out} = AB + AC_{in} + BC_{in}
$$

I sommatori completi possono essere concatenati per costruire sommatori a piu' bit.

**Multiplexer**: un multiplexer, o `MUX`, e' un blocco combinatorio che seleziona uno tra piu' ingressi e lo inoltra a un'unica uscita. In un `MUX 2:1`, con ingressi `I0`, `I1`, selettore `S` e uscita `Y`, vale:

$$
Y = !S I_0 + S I_1
$$

I multiplexer sono molto usati per il routing dei dati e per implementare funzioni logiche.

**Demultiplexer**: un demultiplexer, o `DEMUX`, compie l'operazione opposta: prende un ingresso dati e lo instrada verso una delle possibili uscite in base ai segnali di selezione. In un `DEMUX 1:2` con ingresso `D`, selezione `S` e uscite `Y0`, `Y1`, vale:

$$
Y_0 = !S D
qquad
Y_1 = S D
$$

**Encoder**: un encoder e' un blocco combinatorio che trasforma un ingresso attivo tra molti in un codice binario in uscita. Un encoder `4:2`, per esempio, trasforma quattro linee di ingresso in due bit di uscita che rappresentano l'indice dell'ingresso attivo.

**Priority encoder**: un *priority encoder* e' un encoder che assegna priorita' agli ingressi. Se piu' ingressi sono attivi contemporaneamente, l'uscita rappresenta quello con priorita' maggiore. Questo evita ambiguita' nella codifica.

**Decoder**: un decoder e' un blocco combinatorio che trasforma un codice binario in una sola uscita attiva tra molte. Un decoder `n`-a-`2^n` attiva una sola linea di uscita per ciascuna combinazione degli ingressi. E' spesso usato per selezione di memoria e generazione di segnali di controllo.

**Comparator**: un comparatore e' un blocco combinatorio che confronta due parole binarie e produce uno o piu' segnali di risultato. Nella forma piu' semplice verifica se due bit o due vettori sono uguali.

**Magnitude comparator**: il comparatore di magnitudine confronta due numeri binari `A` e `B` e produce tipicamente tre uscite: `A > B`, `A = B` e `A < B`. E' usato quando non basta sapere se due valori sono uguali, ma occorre conoscerne anche l'ordinamento.

**PLA (Programmable Logic Array)**: una `PLA` e' una struttura logica programmabile composta da una rete `AND` programmabile e da una rete `OR` programmabile. Consente di implementare funzioni `SOP` in modo flessibile, perche' sia i prodotti sia le somme possono essere configurati.

**PAL (Programmable Array Logic)**: una `PAL` e' simile a una `PLA`, ma in genere ha la rete `AND` programmabile e la rete `OR` fissa. E' meno flessibile di una `PLA`, ma piu' semplice e spesso piu' efficiente da realizzare.

### 03.05. Circuiti sequenziali

**Definizione di circuiti sequenziali**: un circuito sequenziale e' un circuito digitale in cui le uscite dipendono non solo dagli ingressi correnti, ma anche dallo stato interno del circuito, cioe' dalla storia precedente degli ingressi e delle uscite.

**Differenza tra circuiti combinatori e sequenziali**: nei circuiti combinatori le uscite dipendono solo dagli ingressi attuali. Nei circuiti sequenziali, invece, le uscite dipendono dagli ingressi attuali e dallo stato memorizzato. Questo rende necessari elementi di memoria e spesso un segnale di clock.

**Elementi di memoria**: gli elementi di memoria sono componenti digitali capaci di conservare un valore logico nel tempo. Latch e flip-flop sono gli elementi di memoria fondamentali usati per costruire registri, contatori e macchine a stati finiti.

**Concetto di feedback**: il feedback e' il collegamento di una parte dell'uscita di un circuito verso i suoi ingressi. Nei circuiti sequenziali il feedback e' essenziale, perche' permette al circuito di mantenere e aggiornare il proprio stato interno.

**Segnale di clock**: il clock e' un segnale periodico che sincronizza il funzionamento dei circuiti sequenziali sincroni. E' caratterizzato da periodo `T` e frequenza `f`, legati da:

$$
 f = \frac{1}{T}
$$

Molti elementi sequenziali aggiornano il proprio stato solo sul fronte di salita o di discesa del clock.

**Circuiti sequenziali sincroni**: nei circuiti sincroni gli aggiornamenti di stato avvengono in istanti discreti determinati dal clock. Questa organizzazione semplifica l'analisi temporale e la progettazione, ed e' la piu' usata nei sistemi digitali moderni.

**Circuiti sequenziali asincroni**: nei circuiti asincroni lo stato puo' cambiare immediatamente al variare degli ingressi, senza attendere un fronte di clock. Possono essere piu' veloci in alcuni casi, ma sono piu' difficili da progettare e analizzare a causa dei problemi di glitch e hazard.

**Latch e flip-flop**: un latch e' un elemento di memoria sensibile al livello di un segnale di abilitazione, mentre un flip-flop e' tipicamente sensibile al fronte del clock. In pratica, il latch e' trasparente quando e' abilitato; il flip-flop campiona l'ingresso solo in un preciso istante.

**Latch SR**: il latch `SR` ha due ingressi principali: `S` (*set*) e `R` (*reset*). Permette di forzare lo stato memorizzato a `1` oppure `0`. Nella versione `NOR`, la combinazione `S = 1` e `R = 1` e' proibita, perche' porta a una condizione non valida.

**Latch D**: il latch `D` deriva dal latch `SR` ed evita la combinazione proibita. Ha un ingresso dati `D` e un segnale di enable. Quando l'enable e' attivo, l'uscita segue `D`; quando l'enable non e' attivo, l'uscita mantiene il valore memorizzato.

**Flip-flop SR**: il flip-flop `SR` e' la versione sincronizzata del latch `SR`. Gli ingressi `S` e `R` vengono campionati sul fronte del clock, cosi' che lo stato cambi solo in corrispondenza di quell'evento.

**Flip-flop D**: il flip-flop `D` e' l'elemento di memoria sincrono piu' usato. Sul fronte attivo del clock trasferisce il valore di `D` sull'uscita `Q`. La sua relazione fondamentale e':

$$
Q^{+} = D
$$

dove `Q+` indica lo stato successivo.

**Flip-flop JK**: il flip-flop `JK` generalizza il `SR` eliminando la combinazione proibita. Se `J = 1` e `K = 0`, il circuito va in set; se `J = 0` e `K = 1`, va in reset; se `J = K = 0`, mantiene lo stato; se `J = K = 1`, commuta. Una forma utile della legge di stato e':

$$
Q^{+} = J!Q + !KQ
$$

**Flip-flop T**: il flip-flop `T` (*toggle*) cambia stato quando `T = 1` al fronte di clock, e mantiene il valore quando `T = 0`. La relazione fondamentale e':

$$
Q^{+} = T xor Q
$$

**Setup time**: il tempo di setup e' il tempo minimo per cui l'ingresso dati deve rimanere stabile prima del fronte attivo del clock, affinche' il dato venga acquisito correttamente dal flip-flop.

**Hold time**: il tempo di hold e' il tempo minimo per cui l'ingresso dati deve rimanere stabile dopo il fronte attivo del clock, affinche' l'acquisizione sia corretta.

**Clock-to-Q delay**: il ritardo `clock-to-Q` e' il tempo che intercorre tra il fronte attivo del clock e la variazione effettiva dell'uscita `Q` del flip-flop.

**Metastabilita'**: la metastabilita' e' una condizione in cui un elemento sequenziale, tipicamente un flip-flop, non riesce a risolversi rapidamente in uno stato logico stabile `0` oppure `1`. Si verifica quando i vincoli temporali, come setup e hold, non sono rispettati. E' un fenomeno centrale nell'attraversamento di domini di clock diversi.

**FSM (Finite State Machines)**: una macchina a stati finiti e' un modello di circuito sequenziale in cui il comportamento e' descritto da un numero finito di stati, transizioni tra stati, ingressi e uscite. Le FSM sono usate per controlli, protocolli, sequenziamenti e datapath.

**Macchine di Mealy**: in una macchina di Mealy le uscite dipendono sia dallo stato corrente sia dagli ingressi correnti. Questo consente spesso di usare meno stati, ma rende le uscite potenzialmente piu' sensibili ai glitch sugli ingressi.

**Macchine di Moore**: in una macchina di Moore le uscite dipendono solo dallo stato corrente. Le uscite sono quindi tipicamente piu' stabili, ma talvolta servono piu' stati rispetto a una macchina di Mealy equivalente.

**Diagramma degli stati**: il diagramma degli stati rappresenta graficamente una macchina a stati finiti. I nodi rappresentano gli stati e gli archi rappresentano le transizioni, spesso etichettate con condizioni di ingresso ed eventuali uscite.

**Tabella degli stati**: la tabella degli stati e' una rappresentazione tabellare della FSM. Per ogni stato corrente e per ogni combinazione significativa di ingressi, indica lo stato successivo e le eventuali uscite.

**Minimizzazione degli stati**: la minimizzazione degli stati consiste nel ridurre il numero di stati di una FSM senza cambiarne il comportamento osservabile. Si ottiene identificando stati equivalenti e fondendoli.

**Codifica degli stati**: la codifica degli stati e' l'associazione di un codice binario a ciascuno stato simbolico della FSM. Scelte comuni sono la codifica binaria, one-hot e Gray. La scelta influenza area, velocita' e semplicita' della logica.

### 03.06. Blocchi sequenziali

**Registro**: un registro e' un insieme di flip-flop usati per memorizzare una parola binaria di piu' bit. Ogni flip-flop memorizza un bit della parola.

**Registro parallelo**: in un registro parallelo tutti i bit vengono caricati e letti simultaneamente. E' il tipo piu' comune di registro nei datapath e nei registri del processore.

**Shift register**: uno *shift register* e' un registro in cui il contenuto puo' essere spostato verso sinistra o verso destra a ogni impulso di clock. E' utile per conversione seriale/parallela, ritardi digitali e sequenze.

**Registro SISO**: un registro `SISO` (*Serial-In Serial-Out*) riceve i dati in serie e li restituisce in serie. Ogni bit attraversa il registro un clock alla volta.

**Registro SIPO**: un registro `SIPO` (*Serial-In Parallel-Out*) riceve dati in serie ma li rende disponibili in parallelo sulle uscite. E' molto usato per convertire flussi seriali in parole parallele.

**Registro PISO**: un registro `PISO` (*Parallel-In Serial-Out*) carica una parola in parallelo e poi la trasmette serialmente. E' utile per inviare dati paralleli su collegamenti seriali.

**Registro PIPO**: un registro `PIPO` (*Parallel-In Parallel-Out*) carica e fornisce dati in parallelo. E' essenzialmente un registro parallelo classico.

**Registro universale a scorrimento**: un registro universale a scorrimento combina piu' modalita' operative: mantenimento del contenuto, caricamento parallelo, shift a destra e shift a sinistra. E' un blocco molto flessibile.

**Registro con controllo di load**: un registro con segnale di load carica un nuovo valore solo quando il segnale di abilitazione al caricamento e' attivo. In caso contrario mantiene il valore precedente.

**Registro con clear o reset**: un registro con `clear` o `reset` puo' essere forzato a uno stato noto, spesso tutto zero. Il reset puo' essere sincrono oppure asincrono.

**Contatori sincroni**: nei contatori sincroni tutti i flip-flop vengono pilotati dallo stesso clock. Questo riduce gli sfasamenti temporali tra i bit e rende il comportamento piu' prevedibile.

**Contatori asincroni**: nei contatori asincroni, o *ripple counters*, il clock del primo flip-flop genera a cascata i cambiamenti dei successivi. Sono semplici ma piu' lenti, perche' il ritardo si accumula lungo la catena.

**Contatore up**: un contatore `up` incrementa il valore memorizzato a ogni impulso di clock.

**Contatore down**: un contatore `down` decrementa il valore memorizzato a ogni impulso di clock.

**Contatore up/down**: un contatore `up/down` puo' contare in aumento oppure in diminuzione in base a un segnale di controllo.

**Contatore modulo-n**: un contatore modulo `n` percorre ciclicamente `n` stati distinti e poi riparte dall'inizio. Per esempio, un contatore modulo `10` attraversa gli stati da `0` a `9`.

**Ring counter**: un ring counter e' un registro a scorrimento in cui un singolo bit `1` viene fatto ruotare ciclicamente tra le posizioni del registro. Produce una sequenza di stati one-hot.

**Johnson counter**: un contatore di Johnson, o *twisted ring counter*, reimmette il complemento dell'ultimo bit all'ingresso del registro a scorrimento. Con `n` flip-flop genera fino a `2n` stati distinti.

**Sequence detector**: un rilevatore di sequenza e' un circuito sequenziale progettato per riconoscere una specifica sequenza di bit in ingresso e attivare un'uscita quando quella sequenza viene osservata. E' una classica applicazione delle FSM.

### 03.07. System Verilog
<!-- to do - HDL (Hardware Description Languages) -->
<!-- to do - simulazione dell'hardware -->
<!-- to do - sintesi di una rete logica -->
<!-- to do - bug e debugging -->
<!-- to do - cenni storici e caratteristiche del system verilog -->
<!-- to do - moduli: la keyword module -->
<!-- to do - assegnamenti continui: la keyword assign e l'operatore = -->
<!-- to do - segnali logici singoli e multipli (bys): la keyword logic -->
<!-- to do - operatori logici -->
<!-- to do - operatori di riduzione -->
<!-- to do - operatore ternario (o condizionale) e assegnamento condizionale -->
<!-- to do -->

### 03.08. Curiosità: il codice Morse e il codice Braille

**Codice Morse**: il codice Morse è un sistema di codifica e di decodifica usato per trasmettere lettere, numeri e punteggiatura mediante segnali di tipo intermittente. In pratica il codice Morse si può usare per comunicare sia su brevi, sia su medie, sia su lunghe distanze, solitamente mediante suoni, o mediante l'accensione e lo spegnimento di una sorgente luminosa, come una torcia. Il codice Morse fu inventato da Samuel Finley Breese Morse (1791-1872) nel 1837 e venne usato soprattutto mediante il telegrafo, uno strumento usato appunto per comunicare su grandi distanze all'epoca. Alfred Vail (1807-1859) lo studiò e lo ampliò e perfezionò ulteriormente. Oggigiorno il codice Morse è soggetto a standard internazionale ed è standardizzato dall'ITU (International Communication Union) con la sua raccomandazione ITU-R M.1677-1.

La figura seguente mostra l'alfabeto del codice morse:

<!-- to add -->
*In Figura: l'alfabeto del codice Morse, che comprende lettere, numeri e caratteri di punteggiatura*

Le regole per comunicare in codice Morse sono:

- La durata del punto è arbitraria e unitaria: essa viene usata per determinare la velocità di comunicazione ed è il tempo di riferimento del codice Morse.
- La durata di una linea è circa tre volte la durata di un punto.
- La pausa tra punti e/o linee deve essere uguale alla durata di un punto.
- La pausa tra le lettere è circa uguale alla durata di una linea.
- La pausa tra le parole è circa uguale alla durata di due linee.

Per esempio, la seguente figura mostra la stringa di testo "Hello World" in codice Morse:

<!-- to add -->
*In Figura: la stringa di testo "Hello World" in codice Morse*

Numerosi sono i film e le serie TV in cui compare e viene usato il codice Morse: spesso, viene usato da spie ed agenti segreti durante le missioni segreti per comunicare in silenzio, senza dare nell'occhio. Il segnale SOS è costitiito da tre punti (per la prima S), tre linee (per la O) e da altri tre punti (per la seconda S): è la parola in codice Morse più nota.

Una piccola osservazione riguardo il codice Morse: esso è un classico esempio di codice binario, in quanto sfrutta due soli simboli per la rappresentazione di lettere, numeri e caratteri di punteggiatura. Punti e linee si possono anche chiamare, rispettivamente, come 0 e 1. Dati `n` simboli del codice Morse, si possono rappresentare al massimo `2^n` differenti caratteri.

Esiste un modo per decodificare facilmente e rapidamente il codice Morse mentre lo si sta ricevendo? Certamente e lo si fa mediante il diagramma ad albero rappresentato nella seguente figura:

<!-- to add -->
*In Figura: il diagramma ad albero usato per decodificare agevolmente il codice Morse*

Nota come la radice del diagramma ad albero (così come ogni nodo) rappresenta una scelta e si noti come ciascun livello, scendendo di profondità, abbia il doppio dei nodi rispetto al livello precedente. Per esempio, la prima scelta identifica il primo simbolo: se si riceve una sola linea (senza ricevere altri simboli) si ha la lettera T; se si riceve un solo punto (senza ricevere altri simboli) la letterea è la E. Se invece si ricevono altri simboli, si dovrà seguire il percorso dalla radice dell'albero fino a ché i simboli non terminano, di fatto attraversando (parzialmente, o interamente) l'albero dalla radice fino a un nodo ben preciso. Da notare che:

- La codifica in codice Morse consiste nel tradurre il messaggio in chiaro, o originale in una sequenza di simboli punti e linee e di pause.
- La decodifica del codice Morse consiste nel tradurre l'insieme di punti, linee e pause nel messaggio originale considerando il diagramma ad albero mostrato in precedenza.

Se il codice Morse permette di rappresentare `2^n` caratteri, significa che l'albero di decodifica ha `n` livelli, o `log2(2^n) = nlog2(2) = n`.

**Codice Braille**: <!-- to do -->