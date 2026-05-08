# 02. Physical Layer

### 02.01. Introduzione

Il livello fisico, o physical layer, è il primo livello dello stack TCP/IP che analizzeremo nel corso del testo. Questo livello si occupa di gestire i seguenti problemi:

- Come vengono rappresentati i bit in un mezzo trasmissivo wired, oppure wireless?
- L'analisi di Fourier per la trasmissione di dati digitali.
- La legge di Edholm.
- Il numero massimo di dati che si possono trasmettere, o MDR (Maximum Data Rate).

Tutto ciò ha a che fare con la natura del mezzo trasmissivo.

### 02.02. Segnali

Un segnale è rappresentato dalla variazione di una proprietà della corrente elettrica nel corso del tempo, tipicamente il voltaggio (indicato con V), oppure l'intensità di corrente elettrica (indicato con I). Il voltaggio rappresenta la tensione, ossia la pressione mediante il quale vengono spinti gli elettroni in modo che essi formino un vero e proprio flusso di corrente elettrica; l'intensità di corrente è la quantità di elettroni che passano dal punto A al punto B in una determinata unità di tempo. Il voltaggio si misura in V (Volt), mentre l'intensità di corrente in A (Ampere). Un segnale può essere di due tipi:

- Analogico: se la sua variazione risulta essere continua e, tra un determinato valore di tensione e un altro, il segnale assume una quantità teoricamente infinita di valori (tutte le tensioni "possibili" tra i due valori considerati). I segnali analogici sono generati tipicamente da fenomeni naturali ed è difficilissimo rigenerarli fedelmente tramite componenti elettronici. I segnali digitali hanno, spesso, una forma "ondulata": essi oscillano tra un valore minimo e un valore massimo, detti rispettivamente picco minimo e picco massimo.
- Digitale: se la sua variazione risulta essere discreta, ossia il segnale può assumere solo un ben preciso insieme di valori tra un minimo e un massimo. La natura discreta del segnale digitale lo rende sicuramente più gestibile e più facilmente generabile da parte dei componenti elettrici, per questo viene utilizzano nell'ambito dei sistemi di elaborazione (e anche nelle reti di calcolatori). Si dice anche che un segnale digitale ha un tipico aspetto "ad onde quadre", in quanto esse non oscillano, bensì la tensione cambia istantaneamente (solo dal punto di vista teorico) il valore tra un livello discreto e un altro.

La seguente figura mostra i due tipi di segnali:

<!-- to add -->
*In Figura: i due tipi di segnali elettrici. A sinistra si ha un segnale analogico, a destra un segnale digitale.*

Un segnale digitale ha le seguenti caratteristiche:

- Ampiezza: rappresenta la differenza tra il picco massimo della tensione raggunta dal segnale ed il picco minimo. Si misura in V (Volt).
- Periodicità: un segnale digitale periodico è un segnale che si ripete nella medesima forma nel corso del tempo. Un segnale non periodico, invece, non ha alcuna "forma" individuabile, per cui si può ripetere in qualsivoglia forma nel corso del tempo, anche senza seguire uno schema ben preciso.
- Periodo: un segnale nella sua interezza può durare per molto tempo, a seconda del tipo della comunicazione (si pensi allo streaming di un film, o di una serie TV). Il periodo è l'unità temporale base del segnale affinché esso possa trasmettere il quantitativo minimo di informazione, o di bit. Nelle infrastrutture di reti di calcolatori moderne, il periodo può essere misurato anche in ns (nanosecondi, laddove 1 nanosecondo = $10^{-9}$ secondi, ossia un miliardesimo di secondo), o altri sottomultipli del secondo. Come vedremo adesso, il periodo è l'inverso della frequenza, ossia $t = \frac{1}{f}$. Il periodo si misura ovviamente in $s$ (secondi).
- Frequenza: indica quante volte si ripete il segnale all'interno di un secondo. Si tratta di una metrica utile per comprendere "quanto veloce" va la comunicazione, anche se non è ovviamente il solo parametro che indichi la velocità di trasmissione di un mezzo trasmissivo. La frequenza si misura in Hz (Hertz) ed è l'inverso del periodo, ossia $f = \frac{1}{t}$.
- Lunghezza (o lunghezza d'onda): indicata con la lettera greca lambda ($λ$), essa è misurata in m (metri) e indica quanto è estesa l'onda elettromagnetica dal punto di vista spaziale. Maggiore è la frequenza $f$ del segnale, minore è la lunghezza d'onda $λ$; al contrario, minore è la frequeunza del segnale, maggiore è la lunghezza d'onda $λ$. La lunghezza del segnale è strettamente correlata alla frequenza ed alla velocità della luce, indicata con $c$ e pari a $299 792 458$ m/s (metri al secondo). La velocità della luce è la velocità massima a cui un segnale può arrivare, anche se difficilmente nell'effettiva pratica si raggiungono velocità pari a $\frac{1}{3}$ di quelle della luce, o al massimo a $\frac{1}{2}$. 

In che modo i bit vengono trasmessi mediante un mezzo trasmissivo? Variando la tensione V del mezzo stesso, in cui solitamente una tensione alta rappresenta un 1 logico, mentre una tensione bassa rappresenta uno 0 logico. Quanto abbiamo appena detto si chiama logica positiva ed esiste anche la logica negativa, in cui i due valori logici sono invertiti: 0 è rappresentato da una tensione alta, 1 da una tensione bassa. Ma i bit possono anche essere rappresentati in un altro modo. Ad esempio, nel caso dei mezzi trasmissivi wireless (senza alcun canale fisico), le frequenze delle onde elettromagnetiche stabiliscono se si tratta di un bit 1, o un bit 0: alte frequenze possono rappresentare l'1, basse frequenze lo 0. Analogamente, nelle fibre ottiche (che sono un mezzo trasmissivo basato su segnali luminosi, non elettrici) un impulso luminoso può essere considerato un 1 logico, mentre la sua assenza uno 0 logico.

### 02.03. Analisi di Fourier

Il matematico Jean Baptiste Fourier (1768-1830) studio a fondo le funzioni trigonometriche e le funzioni periodiche. In pratica lui scoprì che, data una funzione periodica, essa si può ricostruire mediante una somma infinita di funzioni seno e coseno, ognuna che accetta un opportuno argomento. Ciò che ne deriva dai suoi importanti studi riguardanti la matematica è la serie di Fourier, ossia una somma infinita di funzioni seno e coseno (ognuna detta armonica) definita da appositi coefficienti, in cui ciascuno rappresenta l'ampiezza dell'armonica.

Partiamo dai concetti singoli e semplici. Una sommatoria da 1 a N è una somma di N termini, ciascuno opportunamente numerato da un indice. Questo concetto si può esprimere, in matematica, nel seguente modo:

$$
\sum_{i=1}^{n} a_i
$$

Analogamente, possiamo creare una somma di termini b da 1 a N scrivendo la seguente formula:

$$
\sum_{i=1}^{n} b_i
$$

Ma per che cosa stanno $a_i$ e $b_i$? Ebbene, ciascun termine $a_i$ è il coefficiente che deve essere moltiplicato per una funzione seno, detta armonica, che presenta la seguente forma:

$$
sin(2πift)
$$

Mentre ciascun termine $b_i$ è il coefficiente che deve essere moltiplicato per una funzione coseno, anch'essa detta armonica, che presenta la seguente forma:

$$
cos(2πift)
$$

Laddove:

- La costante $2π$ rappresenta il periodo del segnale che, come ci dice la trigonometria, risulta essere $2π$.
- La variabile $i$ è proprio l'indice della sommatoria ed indica il numero dell'armonica (1a armonica, 2a armonica e così via).
- La variabile $f$ è definita frequenza fondamentale, ossia la frequenza alla quale si intende trasmettere il segnale. Come abbiamo detto prima, si misura in Hz (Hertz).
- La variabile $t$ rappresenta il tempo, sempre lo stesso a prescindere dall'armonica e dalla frequenza $f$.

Bene, in sostanza abbiamo completato le due sommatorie. Le armoniche seno hanno il seguente aspetto:

$$
\sum_{i=1}^{n} (a_i\ sin(2πift))
$$

Mentre le armoniche coseno hanno il seguente aspetto:

$$
\sum_{i=1}^{n} (b_i\ cos(2πift))
$$

Come abbiamo detto in precedenza, la serie di Fourier deriva direttamente dall'analisi di Fourier, che afferma che qualsiasi funzione periodica nel tempo può essere ricostruita sommando un numero infinito di armoniche seno e coseno. Quindi, possiamo sommare tra loro le due sommatorie, come nel seguente modo:

$$
\sum_{i=1}^{n} (a_i\ sin(2πift)) + \sum_{i=1}^{n} (b_i\ cos(2πift))
$$

La precedente espressione si può riscrivere nel modo seguente:

$$
\sum_{i=1}^{n} (a_i\ sin(2πift) + b_i\ cos(2πift))
$$

Ma non necessariamente abbiamo funzioni che oscillano intorno allo zero: la precedente formula, così come è scritta, "partirebbe" da zero. Tuttavia, nelle reti di calcolatori potrebbero benissimo esistere dei segnali che hanno una certa fase, ossia che partono prima, o dopo lo zero. Per indicare questa fase si somma un ulteriore altro termine, che normalmente si scrive $a_0$. Quindi, se indichiamo con $g(t)$ la funzione periodica che deve essere ricostruita utilizzando la serie di Fourier, possiamo indicare quest'ultima in questo modo:

$$
g(t) = a_0\ \sum_{i=1}^{n} (a_i\ sin(2πift) + b_i\ cos(2πift))
$$

Da notare che non necessariamente dobbiamo utilizzare infinite armoniche seno e coseno per rappresentare una funzione periodica nel tempo (ossia, un segnale). Basta utilizzare il numero giusto di armoniche, quello sufficientemente preciso da poterci garantire una completa ricostruzione del segnale, chiara dal punto di vista digitale. La seguente figura mostra come, aumentando gradualmente il numero di armoniche seno e coseno, si possa ricostruire fedelmente il segnale digitale rappresentato dalle onde quadre:

<!-- to add -->
*In Figura: ecco come viene utilizzata la serie di Fourier per ricostruire un segnale digitale (o segnale a onde quadre) aumentando man mano il numero delle armoniche*

### 02.04. Bandwidth

La bandwidth (o semplicemente banda) di un canale di comunicazione rappresenta l'ampiezza del canale stesso, ovvero la gamma di frequenze utilizzabili per poter trasmettere un segnale. La banda viene spesso confusa con la velocità della trasmisisone dati, ma non è assolutamente così. Se dovessimo fare un parallelismo con le autostrade, la banda indicherebbe il numero delle corsie dell'autostrada, mentre le macchine (ognuna con la propria velocità) rappresentano i singoli segnali che vengono trasmessi nel canale di comunicazione.

La banda è una gamma di frequenze associate al canale trasmissivo, per cui si misura in Hz (Hertz). Due, o più host della rete possono trasmettere simultaneamente, ma a ciascuno di essi viene associata una banda differente. CIò consente di avviare e consentire più comunicazioni contemporaneamente e, inoltre, permette ai dispositivi di comunicare solo con chi di dovere attraverso l'operazione di filtraggio dei segnali.

La bandwidth può anche essere misurata in bps (bit per seconds, o suoi multipli): attenzione che si parla di bit al secondo, non di Byte al secondo. La banda digitale indica quanti bit al secondo possono essere trasmessi utilizzando tutta la banda. Idealmente, se la banda ha una frequenza $f$ e trasmette $n$ bit in ciascun periodo, si potrebbe pensare che la banda digitale sia semplicemente la moltiplicazione dei due termini: $f\ n$. Ma, nella realtà dei fatti, la banda è affetta da rumore e, inoltre, maggiori sono i dispositivi posti in comunicazione fra loro, maggiore è l'overhead di gestione delle comunicazioni stesse. I flussi di bit, comunque, sono pur sempre flussi di bit ed il mezzo trasmissivo si occupa semplicemente di far avvenire tali flussi.

La banda digitale è fortemente correlata con il teorema di Shannon, teorema che afferma che all'interno di un canale trasmissivo dotato di una banda $B$ è possibile ottenere un numero massimo di traasmissione dati pari a:

$$
r = B\ log_2(1 + \frac{S}{N})
$$

$r$ è detto maximum data rate ed è misurato in bps (bit per seconds). $B$ è la banda ed è misurata in Hz (Hertz). $S$ e $N$ sono due nuovi parametri che compaiono in un rapporto: $S$ indica la potenza del segnale che trasmette i dati, mentre $N$ rappresenta la potenza del rumore (anche noto con il termine noise, in inglese). Più precisamente, $S$ è la potenza del segnale utile, mentre $N$ è la potenza del rumore di fondo all'interno di un canale di comunicazione ed è un rapporto critico, determinante per la massima velocità di trasmissione dati del canale di comunicazione. Spesso, $r$ si indica anche con $C$ e si dice che indica la capacità della banda. Il rapporto $\frac{S}{N}$ è detto SNR (Signal to Noise Ratio) e si misura in dB (decibell). Il significato del SNR è il seguente:

- Maggiore è il rapporto, maggiore è la dominanza del segnale rispetto al rumore.
- Minore è il rapporto, maggiore è la dominanza del rumore rispetto al segnale.

### 02.05. Guided Media
<!-- to do -->

##### 02.05.01. Twisted Pair
<!-- to do -->

#### 02.05.02. Coaxial Cable
<!-- to do -->

##### 02.05.03. Optic Fiber
<!-- to do -->

### 02.06. Unguided Media
<!-- to do -->

##### 02.06.01. Wi-Fi
<!-- to do -->

##### 02.06.02. Bluetooth
<!-- to do -->

##### 02.06.03. Mobile Networks
<!-- to do -->

##### 02.06.04. Onde Radio
<!-- to do -->

##### 02.06.05. Microonde
<!-- to do -->

##### 02.06.06. Infrarossi
<!-- to do -->

##### 02.06.07. Onde millimetriche
<!-- to do -->

##### 02.06.08. Comunicazioni satellitari
<!-- to do -->
