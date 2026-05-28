# 02. Physical Layer

### 02.01. Introduzione

Il livello fisico, o physical layer, è il primo livello dello stack TCP/IP che analizzeremo nel corso del testo. Questo livello si occupa di gestire i seguenti problemi:

- Come vengono rappresentati i bit in un mezzo trasmissivo wired, oppure wireless?
- L'analisi di Fourier per la trasmissione di dati digitali.
- La legge di Edholm.
- Il numero massimo di dati che si possono trasmettere, o MDR (Maximum Data Rate).

Tutto ciò ha a che fare con la natura del mezzo trasmissivo.

### 02.02. Segnali

##### 02.02.01. Caratteristiche dei segnali

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

##### 02.02.02. Modalità di comunicazione

Nell'ambito delle reti di calcolatori sono tre le modalità secondo cui due host possono comunicare:

- Comunicazione simplex: il canale trasmissivo è unidirezionale e il segnale può scorrere solo ed esclusivamente in un determinato verso, da una parte all'altra. Solo un host può svolgere il ruolo di mittente ed il rimanente deve necessariamente essere il destinatario. Il megafono è un esempio di questo tipo di comunicazione, sebbene non ci sia un solo destinatario, ma molti.
- Comunicazione half-duplex: il canale trasmissivo può essere usato in modo bidirezionale, ma in modo alternato. In pratica può viaggiare solo ed esclusivamente un segnale alla volta ed in una determinata direzione. In un preciso momento nel tempo solo un host può agire come mittente ed il rimanente come destinatario, ma dopo che il mittente ha concluso la trasmissione del messaggio, si possono invertire i ruoli (ed anche il verso secondo cui viaggia il segnale). I walkie-talkie sono il classico esempio di comunicazione half-duplex: solo una persona alla volta può parlare ed in una determinata direzione.
- Comunicazione full-duplex: è quella più efficiente. In pratica possono viaggiare più sengali all'interno del canale trasmissivi: uno diretto al destinatario, l'altro diretto al mittente. Entrambi gli host posti in comunicazione possono svolgere, in modo intercambiabile, sia il ruolo di mittente, sia quello di destinatario. Si dice anche che il canale trasmissivo sia bidirezionale (il segnale può scorrere verso un polo, o un altro).

##### 02.02.03. Sincronizzazione

La sincronizzazione è il meccanismo che consente al ricevitore di individuare correttamente l'inizio e la fine dei bit trasmessi, garantendo una corretta interpretazione dei dati. A seconda del modo in cui trasmettitore e ricevitore mantengono il riferimento temporale, le comunicazioni possono essere sincrone o asincrone.

Nelle comunicazioni sincrone trasmettitore e ricevitore condividono un riferimento temporale comune, detto clock. I dati vengono inviati come un flusso continuo di bit organizzati in PDU senza la necessità di inserire bit di start e stop per ogni carattere trasmesso. Questo metodo consente una maggiore efficienza nella trasmissione, poiché riduce l'overhead dovuto alle informazioni di controllo. Tuttavia, richiede meccanismi di sincronizzazione più complessi per mantenere allineati i clock dei dispositivi coinvolti.

Nelle comunicazioni asincrone non esiste un clock condiviso tra trasmettitore e ricevitore. Ogni segnale viene trasmesso in modo indipendente ed è delimitato da particolari bit di controllo. Questo approccio semplifica l'implementazione dei dispositivi e permette di trasmettere dati a intervalli irregolari, a seconda della necessità, ma introduce un maggiore overhead e una minore efficienza rispetto alle comunicazioni sincrone.

##### 02.02.04. Modalità di switching

Le reti di calcolatori sono governati da due tipi principali di switching: la modalità packet switching (o commutazione di pacchetto) e la modalità circuit switching (o commutazione di circuito).

Partiamo dalla circuit switching, maggiormente utilizzata nelle reti telefoniche pubbliche, agli inizi di Internet. Il principio secondo il quale funzione una rete circuit switching è la creazione di un circuito virtuale dall'host mittente all'host destinatario: in pratica ciascun host intermedio (router, switch, hub, o altro) si "accorda" con il precedente ed il successivo host in modo da formare un percorso completo che congiunga i due host posti in comunicazione tra loro. La modalità circuit switching si basa, quindi, su un vero e proprio canale virtuale costantemente allocato e riservato agli host posti in comunicazione. La comunicazione non parte in modo diretto, ma dopo una prima fase di creazione del percorso virtuale tra i due host in comunicazione (fase che solitamente richiede del tempo). Inoltre l'efficienze è molto limitata da quanto effettivamente i due host utilizzino il proprio percorso, che si chiama circuito virtuale: raramente viene utilizzato durante tutto il tempo in cui è allocato e in tutta la sua banda allocata. In pratica il circuito virtuale è sottoutilizzato (e la banda che occupa non può, ovviamente, essere usata da altri host della rete). Il vantaggio è che due host non verranno mai disturbati da altri durante la loro comunicazione (meno overhead di gestione durante l'effettiva comunicazione) ed i messaggi inviati dal mittente subiscono ritardi generalmente prevedeibili e controllabili. Si tratta di una modalità adatta per le comunicazioni in tempo reale, non a caso viene ancora oggi usata in certi casi per le chiamate vocali. Tuttavia causa spesso un elevato spreco delle risorse e non è poco flessibile (la modifica del circuito virtuale è molto onerosa). La seguente figura mostra un esempio di rete circuit switching, in cui due host A e B sono collegati da un circuito virtuale formato da nodi intermedi:

<!-- to add -->
*In Figura: una rete circuit switching*

Al contrario, possiamo dire che oggigiorno Internet è una rete globale basata sulla modalità packet switching. La tecnica utilizzata in una rete packet switching è molto semplice: al posto di allocare un circuito virtuale, sarà l'host intermedio a gestire autonomamente (e secondo dovuti algoritmi) il traffico della rete. Questo sarebbe più un argomento da livello network dello stack TCP/IP, ma si è comunque deciso di trattarlo nel livello physical così da comprendere fin da subito le potenzialità delle reti packet switching. Il messaggio originale viene diviso in più PDU, informalmente chiamate pacchetti, che viaggiano lungo la rete: ogni pacchetto include una parte del messaggio originale e delle informazioni di controllo e, a seconda del tipo di comunicazione, può essere numerato, oppure no (in modo tale che il destinatario riordini il messaggio nel modo corretto). Ogni porzione della rete, così come anche l'intera banda del canale di comunicazione, è utilizzata da più utenti in modo dinamico e, quando un host vuole trasmettere qualcosa, inizia semplicemente a farlo senza che venga allocato alcun percorso virtuale tra lo stesso e il destinatario. Grazie agli algoritmi di routing, ai nodi intermedi ed alla frammentazione del messaggio originale in più pacchetti si ha una maggior efficienza ed un elevato utilizzo del canale: questo vuol dire che molti più host possono comunicare all'interno della rete. Il ritardo non è facilmente prevedibile, ma dipende dal traffico della rete e soprattutto da quanto essa è congestionata, se ha colli di bottiglia, se qualche percorso è inusabile a causa di un guasto e molti altri fattori. Si ha una possibile perdita dei pacchetti, ma le reti moderne garantiscono comunque tassi di errore molto bassi, inoltre ciascun livello superiore al fisico dello stack TCP/IP prevede una qualche forma di controllo degli errori, che può arrivare anche a far ritrasmettere un determinato pacchetto al mittente. La seguente figura mostra la modalità packet switching:

<!-- to add -->
*In Figura: una rete packet switching*

Una terza modalità è il message switching, ovvero un packet switching che non utilizza dei pacchetti come unità dati, ma in cui ciascun nodo trasmette l'intero messaggio (causando anche maggiori ritardi). In pratica si mantengono tutti i vantaggi della tecnica packet switching, ma a differenza di suddividere il messaggio originale in più pacchetti e trasmetterli in vari momenti nel corso del tempo, si trasmette direttamente l'intero messaggio. Ciò causa un grande ritardo e, soprattutto, un elevato tasso di errori.

##### 02.02.05. Throughput

A differenza della bandwidth, il trhoughput è la quantità di dati che realmente viaggiano all'interno del mezzo trasmissivo ed è sempre minore, o al massimo uguale (anche se raramente) alla bandwidth. Per esempio, una fibra ottica che ha una frequenza di 1 GHz, difficilmente fornirà questa velocità se più utenti sono collegati alla stessa fibra, per via della gestione dell'overhead degli utenti stessi. Inoltre la fibra ottica (in particolare il nucleo, fatto in vetro) è soggetta ad impurità. Diciamo che arrivare a 700-800 MHz è un buon compromesso. Ecco, in questo esempio 1 GHz rappresenta la bandwidth, mentre 700-800 MHz rappresenta il throughput.

In questo paragrafo cercheremo di calcolare il throughput considerando scenari via via più complessi. Partiamo dal primo caso, ovvero il calcolo del throughput end-to-end tra due host: un host client che richiede dei dati a un host server. Il client è quello che richiede un determinato servizio, mentre il server è quello che lo fornisce. Assumiamo, per semplicità, che tra client e server è presente un nodo intermedio. In pratica vogliamo calcolare il throughput end-to-end tra client e server con un nodo intermedio tra di essi. La situazione è rappresentata nella seguente figura:

<!-- to add -->
*In Figura: throughput end-to-end tra client e server con un nodo intermedio tra di essi*

Il collegamento tra il server S ed il nodo intermdio R ha una velocità di trasmissione pari a $R_S$. Il collegamento tra il client C e il nodo intermedio R ha una velocità di trasmissione pari a $R_C$. Possiamo dire che la massima velocità di trasmissione dati tra S e C è $min(R_S, R_C)$: in pratica è il minimo tra la velocità del collegamento del server e la velocità del collegamento del client. Perché la minima? Perché ovviamente gli host non possono comunicare ad una velocità superiore, se questa non è consentita da un particolare mezzo trasmissivo. Da notare che in figura i due collegamenti sono stati rappresentati come guided media, ma lo stesso discorso vale se questi fossero degli unguided media.

E nel caso di due host, un client C ed un server S, collegati però da un certo numero N - 1 di nodi intermedi (ad esempio, dei router) ed N collegamenti? In pratica si vuole calcolare il throughput end-to-end tra client e server separati da N nodi intermedi tra di essi. Questa situazione è molto simile a quella mostrata nella figura precedente, ma al posto di avere i collegamenti $R_S$ e $R_C$, si hanno più collegamenti: $R_1$, $R_2$, $R_3$, fino a $R_N$. Questa situazione è rappresentata nella figura seguente:

<!-- to add -->
*In Figura: throughput end-to-end tra client e server con N - 1 nodi intermedi tra di essi e N collegamenti*

Ancora una volta, possiamo dire che la massima velocità di trasmissione dati tra S e C è $min(R_1, R_2, R_3, ..., R_N)$: in pratica il throughput è la velocità di trasmissione minima tra tutti i collegamenti a disposizione. In pratica, il collo di bottiglia (bottleneck) è il collegamento che possiede la velocità di trasmissione minima tra C ed S.

Consideriamo ora uno scenario più realistico in cui sono presenti $M$ coppie client-server ($M$ host di tipo client ed $M$ host di tipo server) che condividono uno stesso collegamento della rete. In questo caso il throughput disponibile sul collegamento condiviso deve essere ripartito tra tutte le comunicazioni attive.

Supponiamo che il collegamento condiviso (bottleneck) abbia capacità $R$ e che venga utilizzato contemporaneamente da tutte le $M$ connessioni. Se la banda viene distribuita equamente tra tutte le connessioni, ciascuna coppia client-server avrà a disposizione un throughput pari a:

$$
\frac{R}{M}
$$

Di conseguenza, il throughput end-to-end di una singola connessione sarà limitato sia dalla capacità dei collegamenti lungo il percorso sia dalla quota di banda disponibile sul collegamento condiviso. In generale, il throughput può essere espresso come:

$$
\min\left(R_1, R_2, \ldots, R_N, \frac{R}{M}\right)
$$

dove:

- $R_1, R_2, \ldots, R_N$ sono le capacità dei collegamenti attraversati dalla connessione;
- $R$ è la capacità del collegamento bottleneck condiviso;
- $M$ è il numero di connessioni che utilizzano contemporaneamente tale collegamento.

In altre parole, quando più utenti condividono una stessa risorsa di rete, il throughput disponibile per ciascuno diminuisce all'aumentare del numero di connessioni attive. Per questo motivo, nelle reti reali il throughput percepito dagli utenti può variare nel tempo in funzione del livello di congestione della rete.

### 02.03. Analisi di Fourier

Il matematico Jean Baptiste Fourier (1768-1830) studiò a fondo le funzioni trigonometriche e le funzioni periodiche. In pratica lui scoprì che, data una funzione periodica, essa si può ricostruire mediante una somma infinita di funzioni seno e coseno, ognuna che accetta un opportuno argomento. Ciò che ne deriva dai suoi importanti studi riguardanti la matematica è la serie di Fourier, ossia una somma infinita di funzioni seno e coseno (ognuna detta armonica) definita da appositi coefficienti, in cui ciascuno rappresenta l'ampiezza dell'armonica.

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

### 02.04. Bandwidth, teorema di Shannon e teorema di Nyquist

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

Il teorema di Nyquist stabilisce che la massima velocità di trasmissione dati ottenibile su un canale privo di rumore dipende dalla sua larghezza di banda. In particolare, la frequenza di campionamento deve essere almeno il doppio della massima frequenza presente nel segnale per consentirne la corretta ricostruzione.

Per un canale ideale, il bitrate massimo è dato da:

$$
C = 2B · log_{2}(M)
$$

dove:
- $C$ è la capacità del canale trasmissivo, espressa in bps (bit per second).
- $B$ è la larghezza di banda del canale, ovvero la bandwidth, miurata in Hz;
- $M$ è il numero di livelli del segnale. Un segnale digitale ha solamente due livelli: uno 0 logico ed un 1 logico. Tuttavia, possono esistere anche segnali digitali a più livelli.

Il teorema evidenzia che aumentando la larghezza di banda o il numero di livelli utilizzati nella codifica è possibile incrementare la velocità di trasmissione dei dati.

### 02.05. Guided Media

In canale trasmissivo che consiste in un mezzo guidato (guided media) sfrutta la propagazione del segnale all'interno di un solido per poter attuare la comunicazione. I cavi elettrici come il doppino telefonico ed il cavo coassiale sono esempi di guided media. Un guided media necessita di un'infrastruttura fisica che consiste nel collegamento fisico tra i due, o più host posti in comunicazione tra loro. Si dice anche che gli host sfruttano una connessione wired (cablata). 

##### 02.05.01. Twisted Pair

Il twisted pair (o doppino telefonico) è un guided media molto datato, usato fin dai primi anni della nascita di Internet. Un doppino singolo è costituito da una coppia di fili di rame intrecciati tra loro, in modo tale da ridurre il più possibile il rumore (i campi elettromagnetici generati tra i due fili). La coppia di fili consiste in due fili numerati: 1 e 2. Un moderno twisted pair consiste di ben 4 coppie di fili di rame, laddove ciascuna coppia è intrecciata. Le coppie sono numerate da 1 a 4 e sono opportunamente colorate: la prima coppia è blu, la seconda arancione, la terza verde e la quata è rossa. Ciascuna coppia di fili trasmettere i bit in modo seriale: il filo 1 della coppia va dal mittente al destinatario, mentre il filo 2 va dal destinatario al mittente. In totale ci sono 4 fili che vanno al destinatario e 4 fili che vanno al mittente, in modo tale da realizzare una trasmissione parallela di 4 bit. Le trasmissioni parallele, purtroppo, sono affette da una problematica denominata delay skew (o distorsione di propagazione), ovvero una variazione nel ritardo di propagazione del segnale sulle singole coppie, dovuta al diverso passo di binatura delle coppie. Ad esempio, la coppia 1 potrebbe trasmettere un bit all'istante $t$, mentre le coppie 2, 3 e 4 potrebbero subire un leggero ritardo (anche di pochi microsecondi, o nanosecondi) ed il segnale potrebbe propagarsi più lentamente, giungendo al tempo $t + r$, dove $r$ è il ritardo. La struttura di un doppino telefonico a 4 coppie è mostrata nella seguente figura:

<!-- to add -->
*In Figura: 4 coppie di fili di rame, numerate da 1 a 4. Ciascuna coppia è composta da due fili numerati da 1 a 2. Da notare come ciascun filo di rame ha il proprio isolante, così da non causare interferenze di natura elettrica agli altri fili.*

Esistono tre principali tipi di doppini telefonici:

- UTP (Unshielded Twisted Pair): le 4 coppie di fili di rame non sono schermate, ma sono tutte racchiuse all'interno di una guaina. Ovviamente, ciascun filo ha il proprio isolante.
- FTP (Foiled Twisted Pair): esattamente come l'UTP, ma utilizza un isolante aggiuntivo che racchiude le 4 coppie di fili di rame, riducendo il rischio di interferenze.
- STP (Shilded Twisted Pair): utilizza una schermatura in alluminio per ciascuna coppia di fili di rame, in modo da ridurre gli effetti di interferenze e crosstalk.

La seguente figura mostra le varie tipologie di cavi twisted pair:

<!-- to add -->
*In Figura: le differenze fra UTP, FTP e STP*

Il cavo UTP Categorie 5 (Cat5 UTP) viene spesso utilizzato per la Ethernet classica, che sfrutta solo 2 delle 4 coppie di fili di rame, garantendo una velocità di 100 Mbps (Megabit per second). La Gigabit Ethernet estende l'uso a tutte e 4 le coppie di fili, arrivando a velocità di 1 Gbps (Gigabit per second).

Le schermature dei cavi twisted pair sono state introdotte per ridurre il più possibile il fenomeno del crosstalk, ovvero delle interferenze elettromagnetiche dovute alla generazione di campi elettromagnetici attorno al filo di rame durante il passaggio della corrente elettrica. Si tratta di un fenomeno fisico che non può essere evitato, ma può solo essere controllato, o decrementato il più possibile utilizzando isolanti, guaine e schermature in alluminio (che "assorbono", per modo di dire, i campi elettromagnetici dei fili in rame).

I twisted paier utilizzano comunemente un connettore RJ45 per collegare l'host ad Internet.

#### 02.05.02. Coaxial Cable

Il cavo coassiale (coaxaial cable, o anche coax) viene utilizzato nelle telecomunicazioni e nelle linee di comunicazione elettriche. Spesso il suo scopo è quello di trasportare segnali audio e video, per questo viene utilizzato per trasmettere dati alla TV. La seguente figura mostra come è strutturato un comune cavo coassiale:

<!-- to add -->
*In Figura: struttura di un comune cavo coassiale*

Esso si componete di uno strato più esterno di guaina, che isola l'intero filo di rame. Come secondo strato si presenta una maglia di rame intrecciata, detto anche massa, che serve per isolare il conduttore elettrico di rame posto all'interno del cavo. Successivamete è presente un altro strato di isolante (detto dielettrico interno). Infine, abbiamo il filo di rame vero e proprio nel quale scorrono i segnali dati, detto anche nucleo, o polo caldo. Il segnale si propaga sottoforma di campo elettromagnetico generato dalla corrente elettrica che scorre nel nucleo del cavo. La velocità è una frazione $v$ della velocità della luce.

Sono due i principali tipi di cavi coassiali utilizzati nelle reti di telecomunicazioni:

- I coax con un'impedenza caratteristica di 50 Ω (Ohm) vengono utilizzati per le trasmissioni digitali.
- I coax con un'impedenza caratteristica di 75 Ω (Ohm) vengono utilizzati per trasmettere segnali audiovideo, o segnali video analogici, ma anche per le connessioni Internet via cavo.

Il cavo coassiale trasmette i bit in modo seriale e, vista la sua struttura dotata di numerosi isolanti, esso è adatto a realizzare infrastrutture non solo per LAN, ma anche per MAN.

##### 02.05.03. Optic Fiber

La fibra ottica, detta anche OF (Optic Fiber) è un tipo di mezzo trasmissivo guidato in cui i segnali digitali sono concretizzati da veri e propri segnali luminosi (detti anche impulsi luminosi). Ecco i vantaggi offerti dalle fibre ottiche:

- Esse consetono una maggiore velocità di propagazione del segnale: trattandosi di impulsi luminosi, il segnale luminoso che scorre nucleo del cavo può tranquillamente raggiungere una frazione $v$ della velocità della luca pari a $\frac{1}{3}c$, oppure pari a $\frac{1}{3}c$.
- Sono molto più robuste rispetto ai coax ed ai twister pairs: questo perché i segnali non sono più di natura elettrica, bensì luminosa. Dal punto di vista fisico, è difficile "bloccare" un impulso luminoso che si propaga in un mezzo solido, come il nucleo di una fibra ottica, fatto in filamenti vetrosi (detti anche macromolecolari, o polimeri).
- La fibra ottica è immune ai fenomeni del crosstalk, in quanto non viene generato alcun tipo di campo elettromagnetico intorno al cavo. Questo consente a numerosi provider di Internet di inserire un intero fascio di fibre ottiche all'interno dello stesso cavo senza che l'uno interferisca con l'altro.
- Tutti i punti precedenti si traducono in una maggiore capacità (maggiore bandwidth) ed in una velocità di trasmissione dati, misurata in bps, nettamente maggiore rispetto ai cavi in rame analizzati in precedenza.
- Le fibre ottiche hanno un tasso di errore molto basso, molto più basso rispetto ai cavi in rame. Questo è in parte dovuto all'immunità, da parte della fibra ottica, ai fenomeni come il crosstalk ed alle interferenze elettromagnetiche.
- Una fibra ottica può realizzare facilmente collegamenti su lunghe distanze: numerosi esperimenti provano che la trasmissione di un segnale luminoso può avvenire anche per 50-100 km senza essere rigenerato. Questo rende le fibre ottiche particolarmente adatte alla realizzazioni di reti MAN e WAN.

La struttura della fibra ottica è presentata nella seguente figura:

<!-- to add -->
*In Figura: la struttura di una fibra ottica*

Lo strato più interno è detto nucleo e misura 8 µm (micrometro, dove 1 µm = $10^{-6}$ m): si tratta del filamento vetroso in cui si propaga il segnale luminoso. Poi abbiamo il mantello da 125 µm, che ricopre completamente il nucleo della fibra ottica. Abbiamo poi un buffer, tipicamente più spesso, di 250 µm. Infine, ad avvolgere l'intero cavo con tutti i suoi strati è un ultimo strato che prende il nome di jacket, il cui spessore è ancora maggiore, 400 µm. Da notare come, man mano che si procede dall'interno verso l'esterno del cavo, ciascuno strato aumenta il proprio spessore di circa il doppio rispetto allo strato più interno. Questo garantisce robustezza.

Esistono tantissime tipologie di fibre ottiche, ma noi qui distingueremo solo le fibre ottiche in base alla quantità di segnali che può trasportare nel nucleo del cavo. Ecco che avremo:

- Fibre ottiche monomodali: trasportano un solo segnale alla volta ed il cavo deve essere mantenuto il più possibile diritto (senza curve). Il nucelo è spesso pochi µm, tipicamente non oltre i 15 µm. Solo una comunicazione alla volta è concessa.
- Fibre ottiche multimodali: trasportano più segnali alla volta ed il cavo è più flessibile, in quanto il nucleo arriva ad uno spessore di anche 50 µm, o 60 µm. Una fibra multimodale può consentire più comunicazioni differenti, ossia più impulsi luminosi dotati di una lunghezza d'onda differente possono viaggiare all'interno dello stesso nucleo.

Le fibre multimodali sono utilizzate per lo più nella realizzazione di LAN, o al massimo MAN ad alte velocità; differentemente, le fibre monomodali sono utilizzate più per la realizzazione di reti WAN e per reti MAN particolarmente grandi (coma grandi centri urbani). I cavi transoceanici, ad esempio, che collegano due continenti, o due nazioni differenti separate dal mare, sono per la maggior parte cavi in fibra ottica monomodale: questo perché la luce ha un solo verso di percorrenza ed il segnale presenta molta meno attenuazione e dispersione, è più gestibile e, inoltre, presenta una velocità di trasmissione dati maggiore su lunghe distanze.

Ma divaghiamo un attimo dalle reti di calcolatori e parliamo di fisica: le leggi di Snell sono i principi fisici secondo il quale gli impulsi luminosi si propagano all'interno di un filamento vetroso, ovvero all'interno di una fibra ottica. La prima legge di Snell (detta anche legge della riflessione) stabilisce che il raggio riflesso permane nello stesso piano del raggio incidente che, dal punto di vista puramente matematico, si rappresenta nel seguente modo:

$$
\theta_{i} = \theta_{r}
$$

Laddove $\theta_{i}$ è l'angolo incidente (ovvero l'angolo formato tra il segnale luminoso e la parete del cavo, o superficie riflettente), mentre $\theta_{r}$ è l'angolo del raggio riflesso (ovvero l'angolo tra l'impulso luminoso riflesso e la medesima parete del cavo, o superficie riflettente). La seguente figura mostra la legge di riflessione:

<!-- to add -->
*In Figura: la legge di riflessione*

La seconda legge di Snell (o legge di rifrazione) ha a che fare con gli indici di rifrazione. L'indice di rifrazione di un particolare materiale è indicato solitamente con $n$ ed indica di quanto il raggio incidente sia sfasato rispetto al raggio rifratto. Infatti, quando si hanno due materiali distinti, ognuno con i propri indici di rifrazione $n_{1}$ e $n_{2}$, il segnale luminoso si comporta in modo leggermente diverso rispetto a quanto si potrebbe immaginare:

- Consideriamo il piano perpendicolare alla supercicie incidente. Il raggio incidente formerà un angolo $\theta_{1}$ tra il raggio stesso ed il piano perpendicolare. Il raggio incidente si propaga nel primo materiale, con indice di rifrazione $n_{1}$.
- Sempre considerando il piano perpendicolare, dall'altra parte della superficie riflettente vi è il raggio rifratto, che avrà un angolo tra la superficie perpendicolare ed il raggio stesso di $\theta_{2}$. Il raggio rifratto si propaga nel secondo materiale, con indice di rifrazione $n_{2}$.

La legge di rifrazione, dal punto di vista matematico, si esprime nel seguente modo:

$$
n_{1}\ sin(\theta_{1}) = n_{2}\ sin(\theta_{2})
$$

La seguente figura mostra che cosa significa la precedente formula:

<!-- to add -->
*In Figura: la legge di rifrazione*

Le fibre ottiche sono costruite in modo tale da minimizzare il più possibile il raggio rifratto: ogni volta che un segnale luminoso "rimbalza" contro la superficie riflettente del nucleo, detto anche core, esso perde pochissima potenza; analogamente, il core della fibra ottica è fatto in un materiale opportuno in modo da garantire la massima riflessione possibile. Anche le più piccole impurità possono causare perdita di potenza (attenuazione) non trascurabile del segnale luminoso, per questo le fibre ottiche devono avere meno curve possibili ed hanno un processo di costruzione più complesso rispetto a quello dei cavi in rame.

### 02.06. Unguided Media

Eccoci giunti ai mezzi non guidati (unguided media). Un canale trasmissivo non guidato sfrutta la propagazione delle onde elettromagnetiche per poter trasmettere dei dati dall'host mittente all'host destinatario. Si dice anche che gli host posti in comunicazione sfruttano una connessione di tipo wireless (senza fili). Le comunicazioni wireless sono tipiche dei sistemi satellitari, delle reti mobile e della trasmissione radio.

##### 02.06.01. Wi-Fi

Le reti Wi-Fi sono particolari reti LAN base sulla comunicazione wireless che consentono a dispositivi elettronici di scambiare dati senza utilizzare alcun tipo di guided media. Il funzionamento di una rete Wi-Fi si basa sulla trasmissione di informazioni tramite onde radio, o onde RF (Radio Frequency), generalmente nelle seguenti tre bande di frequenza:

- Una banda a 2.4 GHz.
- Una banda a 5 GHz.
- Una banda a 6 GHz, introdotta nelle più recenti versioni delle reti Wi-Fi.

Una rete Wi-Fi è composta principalmente da un AP (Access Point, punto d'accesso), spesso integrato nel router, o nello switch, e da uno o più dispositivi client (personal computer, laptop, smartphone, smartwatch, tablet e dispositivi IoT). L'AP crea la rete wireless e coordina le comunicazioni, mentre i client si collegano a essa tramite una scheda di rete Wi-Fi: più client possono comunicare tra loro sfruttando frequenze differenti all'interno di una stessa banda o, se lo supportano, all'interno della banda che utilizza frequenze più alte e segnali più potenti, posta a 6 GHz.

Quando un dispositivo cerca una rete, rileva i segnali radio trasmessi dagli AP vicini. Ogni rete è identificata da un nome chiamato SSID (Service Set IDentifier). Dopo aver scelto una rete, il dispositivo avvia una procedura di associazione e autenticazione. Se la rete è protetta, viene richiesta una password che serve per generare chiavi crittografiche utilizzate per cifrare il traffico dati. Una volta stabilita la connessione, il router assegna al dispositivo un indirizzo IP tramite il protocollo DHCP (Dynamic Host Configuration Protocol). Tale indirizzo identifica il dispositivo all’interno della rete locale e permette lo scambio corretto dei dati.

La comunicazione avviene attraverso pacchetti di dati. Le informazioni vengono suddivise in piccoli blocchi, convertite in segnali radio e trasmesse nell’aria. Il dispositivo destinatario riceve il segnale, lo decodifica e ricostruisce i dati originali. Le prestazioni di una rete Wi-Fi dipendono da diversi fattori: distanza dal router, presenza di ostacoli, interferenze elettromagnetiche, numero di dispositivi collegati e standard Wi-Fi utilizzato. Le pareti, soprattutto se spesse e fatte in materiali metallici (o rivestite in materiali metallici), attenuano sensibilmente il segnale. Anche altre reti Wi-Fi vicine possono causare interferenze se utilizzano gli stessi canali radio e le stesse frequenze.

Nel tempo gli standard Wi-Fi si sono evoluti per aumentare velocità, stabilità ed efficienza. Gli standard più recenti, come Wi-Fi 6 e Wi-Fi 7, introducono tecnologie avanzate come MIMO, OFDMA e beamforming, che migliorano la gestione simultanea di molti dispositivi e ottimizzano la direzione del segnale radio. Studieremo alcune di queste tecniche nel corso dei prossimi capitoli.

Dal punto di vista della sicurezza, le reti moderne utilizzano protocolli come WPA2 e WPA3, che proteggono le comunicazioni tramite cifratura. Una password robusta e l’aggiornamento regolare del firmware del router sono elementi fondamentali per ridurre i rischi di accessi non autorizzati.

È importante distinguere tra Wi-Fi e Internet. Il Wi-Fi è semplicemente la tecnologia wireless utilizzata per collegare dispositivi a una rete locale, mentre Internet è la rete globale che permette la comunicazione tra sistemi distribuiti nel mondo. Una rete Wi-Fi può esistere anche senza accesso a Internet.

##### 02.06.02. Bluetooth

Bluetooth è una tecnologia di comunicazione wireless a corto raggio utilizzata per lo scambio di dati tra dispositivi come smartphone, computer, cuffie, smartwatch e periferiche. Opera nella banda ISM (Industrial, Scientific, Medical) a 2.4 GHz e consente la creazione di reti personali (WPAN -Wireless Personal Area Network-). Le comunicazioni avvengono a basso consumo energetico e su distanze generalmente comprese tra pochi metri e alcune decine di metri, a seconda della classe del dispositivo e della versione utilizzata.

##### 02.06.03. Lo spettro elettromagnetico e le leggi di Maxwell

In fisica viene utilizzato il termine spettro per indicare il modo in cui una grandezza fisica si distribuisce nel corso del tempo, oppure in funzione di un'altra grandezza fisica. Nel nostro caso, che parliamo di reti di calcolatori, si tratta di spettri elettromagnetici: una vastissima gamma di frequenze che sono già utilizzate, o potrebbero essere utilizzate per la comunicazione su Internet. In breve, lo spettro elettromagnetico è la gamma di tutte le possibili frequenze della radiazione elettromagnetica. La radiazione elettromagnetica è la propagazione dell'energia nello spazio circostante sotto forma di campi elettrici ed onde elettromagnetiche. Le onde elettromagnetiche, in condizioni atmosferiche normali, presentano la stessa velocità posseduta dalle onde luminose, in fisica nota come $c$, pari a circa $299 792 458$ m/s (metri al secondo). La velocità della luce, $c$, è una costante universale e nessun oggetto può superare tale velocità. In realtà è veramente molto difficile, nelle reti di calcolatori (per quanto un mezzo trasmissivo possa essere quanto più puro possibile) permettere a un segnale di viaggiare alla velocità della luce.

La seguente immagine mostra lo spettro elettromagnetico utilizzato per allocare determinati range di frequenze a particolari tipi di comunicazione:

<!-- to add -->
*In Figura: ecco lo spettro elettrmagnetico, utilizzato nelle comunicazioni di tipo unguided nelle reti di calcolatori*

Maggiore è la frequenza del segnale, minore è la sua lunghezza d'onda; analogamente, maggiore è la sua lunghezza d'onda, minore è la sua frequenza. Lo spettro elettromagnetico è rappresentato come una barra orizzontale in cui all'estrema destra vi sono le onde radio, che presentano una frequenza che va dai $10^8$ ai $10^4$ Hz (lunghezza d'onda dell'ordine dei metri, fino ai migliaia di metri), mentre all'estrema sinistra vi sono le onde gamma, che presentano una frequenza molto più elevata (e di conseguenza una lunghezza d'onda molto minore), variabile tra i $10^24$ e $10^19$ Hz. In pratica il diagramma nella precedente figura mostra il variare di due grandezze:

- La lunghezza d'onda aumenta man mano che si scorre da sinistra verso destra.
- La frequenza d'onda aumenta man mano che si scorre da destra verso sinistra.

In fisica si utilizza la lettera $f$ per indicare la frequenza, mentre la lettera greca $\lambda$ si utilizza per la lunghezza d'onda, ma ciò è irrilevante per i nostri fini.

Esistono varie tipologie di onde utilizzate nel mondo delle reti di calcolatori:

- Onde radio: onde elettromagnetiche a bassa frequenza utilizzate nelle comunicazioni radio, televisive, mobili e satellitari. Possono propagarsi su lunghe distanze e attraversare diversi ostacoli.
- Microonde: onde elettromagnetiche a frequenza più elevata rispetto alle onde radio, utilizzate nelle comunicazioni satellitari, nei ponti radio, nelle reti Wi-Fi e nei radar.
- Infrarossi: radiazioni elettromagnetiche con frequenza superiore alle microonde e inferiore alla luce visibile. Utilizzate per telecomandi, sensori e comunicazioni a corto raggio. Sono molto direzionali e più sensibili a certi ostacoli (come strutture, abitazioni, o pareti).
- Onde UV (Ultra Violetti): radiazioni elettromagnetiche con frequenza superiore alla luce visibile. Sono impiegate in applicazioni mediche, sterilizzazione e analisi dei materiali. Sono estremamente direzionali.
- Raggi X: radiazioni elettromagnetiche ad alta frequenza e grande capacità di penetrazione, utilizzate principalmente in ambito medico e industriale per ottenere immagini dell'interno degli oggetti. Forniscono analisi molto dettagliate in contesti clinici e, talvolta, militari.
- Raggi gamma (onde luminose): radiazioni elettromagnetiche con la frequenza più elevata e la maggiore energia nello spettro elettromagnetico. Sono prodotte da fenomeni nucleari e utilizzate in medicina, ricerca scientifica e trattamenti radioterapici (applicazioni molto specifiche).

I principali fenomeni che possono disturbare la propagazione delle onde elettromagnetiche sono:

- Attenuazione: perdita di potenza del segnale durante la propagazione nel mezzo trasmissivo.
- Rumore: disturbi casuali che alterano il segnale trasmesso, causati da fenomeni naturali, o da altre comunicazioni condotte da altri dispositivi elettronici.
- Interferenza: sovrapposizione di segnali provenienti da altre sorgenti che degradano la comunicazione. Per esempio, due onde elettromagnetiche potrebbero andare in conflitto tra loro.
- Riflessione: il segnale rimbalza su superfici, o ostacoli modificando il percorso di propagazione.
- Rifrazione: variazione della direzione dell'onda dovuta al passaggio tra mezzi con caratteristiche differenti.
- Diffrazione: deviazione dell'onda attorno agli ostacoli, o attraverso aperture che causano una distorsione del segnale stesso.
- Scattering: dispersione del segnale causata da particelle, o irregolarità presenti nel mezzo (nel caso delle onde elettromagnetiche, il mezzo è l'atmosfera terrestre).
- Multipath: ricezione dello stesso segnale attraverso percorsi differenti, con possibili ritardi e distorsioni.

##### 02.06.04. Comunicazioni satellitari

I satelliti e le comunicazioni satellitari hanno subito profonde innovazioni nel corso degli ultimi tre decenni, in particolare durante gli ultimi anni. I satelliti sono dispositivi elettromeccanici di grosse dimensioni che vengono periodicamente mandati in orbita per scopi di comunicazione, di perlustrazione, o di analisi dell'atmosfera terrestre, o del sistema solare.

Le comunicazioni satellitari derivano in modo diretto dalle comunicazioni S2S (Ship-to-Shore) e possono essere considerate la sua naturale evoluzione. La comunicazione S2S (Ship-to-Shore) è una comunicazione wireless tra una nave (ship) e una stazione terrestre, o costiera (shore). Viene utilizzata per trasmettere dati, voce e informazioni operative tra le imbarcazioni e i centri di controllo a terra. In pratica questa comunicazione è fondamentale per trasmettere dati nell'oceano e per la sicurezza marittima, inoltre essa garantisce servizi di rete a bordo di una nave (sebbene sia isolata dai centri urbani).

Un'altra forma di comunicazione molto utilizzata in passato è la TLT (Terra-Luna-Terra), meglio nota con l'acronimo inglese come EME (Earth-Moon-Earth), o moon bounce. Si tratta di una tecnica di radiocomunicazione che utilizza la superficie della Luna come riflettore passivo. Un segnale radio viene trasmesso dalla Terra verso la Luna, riflesso dalla sua superficie e successivamente ricevuto da una stazione terrestre. Questa tecnica consente comunicazioni su distanze molto elevate senza l'utilizzo di satelliti artificiali, ma richiede antenne direttive ad alto guadagno e trasmettitori di elevata potenza a causa della forte attenuazione del segnale.

Parliamo di satelliti. Il satellite ha uno scheletro chiamato bus, la struttura portante dell'intera macchina che, realizzata in materiali come titanio, o leghe di alluminio, sopporta le grandissime tensioni che possono avvenire durante il lancio. Le strutture secondarie e terziarie comprendono le staffe, gli alloggiamenti per le apparecchiature elettroniche ed i pannelli protettivi. Un satellite è anche costituito dai cosiddetti MLI (Multi-Layer Insulation): strati sovrapposti di materiale riflettente che proteggono l'hardware dal caldo estremo del Sole e dal gelo dello spazio profondo. Un satellite ha tantissimi sensori, tra cui: controllo dell'altitudine, controllo dell'orbita, telemetria, antenne (per trasmettere nelle bande C, Ku e Ka), computer di bordo, controllo terminco e tanto altro. I satelliti hanno ovviamente dei propulsori che sono continuamente, o parzialmente operativi durante tutto il ciclo di vita del satellite stesso. Ovviamente i propulsori consumano carburante, per il quale è previsto un apposito alloggiamento.

Un satellite nasce per mantenere un'orbita ben precisa, che viene denominata orbita geostazionaria (geotrationary orbit, in inglse): in pratica un satellite descrive un'orbita simile a una circonferenza intorno al pianeta Terra, mantenendosi sempre alla stessa distanza dalla sua superficie (in realtà viene considerato il livello dell'acqua come superficie). Il satellite deve utilizzare in modo continuo, o ad intermittenza, o a comando i propri propulsori in modo da controbilanciare la forza d'attrazione gravitazionale esercitata dal pianeta Terra stesso. Questa situazione è rappresentata nella seguente figura:

<!-- to add -->
*In Figura: l'orbita geostazionaria descritta da un satellite intorno al pianeta Terra posto ad una certa altitudine*

Esistono tre principali fasce in cui i satelliti possono mantenere la propria orbita geostazionaria. Tali fasce sono:

- LEO (Low Earth Orbit): i satelliti LEO orbitano a un'altitudine compresa tra circa 160 e 2.000 km dalla superficie terrestre. Grazie alla loro vicinanza alla Terra, offrono una bassa latenza e sono utilizzati per telecomunicazioni su brevi/medie distanze, osservazione terrestre e sistemi di navigazione. Per garantire una copertura globale è necessario impiegare costellazioni composte da numerosi satelliti, per questo le costellazioni di satelliti (ne parleremo a breve) tipicamente risiedono nella fascia LEO, anche se non è detto.
- MEO (Medium Earth Orbit): i satelliti MEO orbitano a un'altitudine compresa che varia tra circa 2.000 e circa 35.786 km. Presentano una latenza e una copertura intermedie rispetto ai satelliti LEO e GEO. Sono impiegati principalmente nei sistemi di navigazione satellitare, come il GPS, Galileo e GLONASs.
- GEO (Geostationary Earth Orbit): i satelliti GEO orbitano a circa 35.786 km di altitudine sopra l'equatore terrestre e ruotano con la stessa velocità angolare della Terra. Di conseguenza appaiono fermi rispetto a un osservatore terrestre. In pratica sono geosincronizzati con la rotazione della Terra (un pò come la Luna). Grazie all'ampia area di copertura, sono utilizzati per telecomunicazioni, trasmissioni televisive e collegamenti satellitari a lunga distanza . Lo svantaggio principale è l'elevata latenza dovuta alla grande distanza dalla superficie terrestre.

Le tre fasce dell'atmosfera terrestre sono rappresentate di seguito:

<!-- to add -->
*In Figura: le fasce LEO, MEO e GEO ospitanti satelliti*

<!-- to do - costellazioni di satelliti: Starlink, Project Kuiper e WorldVu -->

##### 02.06.09. Reti wireless mobile

La tecnologia 1G (Generation 1) è basata sulla trasmissione dati mediante l'invio e la ricezione di segnali analogici, molto più difficili da generare e da interpretare dai dispositivi elettronici. Aveva un livello di sicurezza molto basso, se non nullo in determinate comunicazioni. Si tratta della rete mobile più utilizzata negli anni '80 del secolo scorso. La tecnologia 1G, con la sua trasmissione analogica, utilizzava la AMPS (Advanced Mobile Phone System), che permetteva solo la comunicazione vocale (solo segnali vocali). AMPS utilizzava la FDMA (Frequency Division Multiple Access), in cui a ciascuna comunicazione veniva allocata una determinata banda di frequenze.

La tecnologia 2G (Generation 2) introdusse numerose novità. Lanciata commercialmente nel 1991 con il GSM (Global System for Mobile communication), rispetto alle reti 1G essa utilizza segnali solo ed esclusivamente digitali. Si utilizzano frequenze di comunicazione più alte rispetto alle reti 2G, anche se comunque non troppo robuste a determinati fenomeni di interferenza elettromagnetica. Fu la tecnologia più utilizzata negli anni '90 del secolo scorso. L'utilizzo delle SIM (Subscriber Identity Module) era all'ordine del giorno, laddove era registrato il numero di telefono. Da quegli anni in poi si sono susseguiti vari formati di SIM, ma oggi il futuro è destinato alle eSIM (eletronic SIM), ovvero SIM non fisiche, ma elettroniche. Nello standard GSM, il MSC (Mobile Switching Center) è un grande centro che smista e gestisce le comunicazioni tra due, o più utenti mobili. Il compito principale di un MSC è gestire, instradare e smistare le chiamate vocali e gli SMS tra gli utenti della rete mobile e tra questi e la rete fissa. A proposito: SMS (Short Message Service) è un vero e proprio servizio di messaggistica utilizzato dagli utenti mobili per comunicare attraverso messaggi testuali. Un singolo SMS può contenere non più di 160 caratteri. Oggigiorno gli SMS vengono ancora utilizzati per la generazione di password temporanee, l'autenticazione a due fattori e molto altro. GSM utilizza il TDMA (Time Division Multiplex Access), ossia associa una porzione di tempo ben precisa a ciascuna coppia di host in comunicazione, di fatto non garantendo elevate velocità di trasmissione.

Il Giappone fu il primo paese ad introdurre la terza generazione delle reti mobili: le reti 3G (Generation 3). Le reti 3G sono molto più evolute rispetto a quelle 2G e lo standard che le governa è denominato UMTS (Universal Mobile Telecommunications System), che è la naturale evoluzione del GMS introdotto dalle reti 2G. Utilizza il protocollo W-CDMA (Wideband Code Division Multiple Access), un particolare metodo di accesso al canale radio che prevede l'utilizzo di una banda molto più larga rispetto a quella usata dalle reti 2G, in cui ogni host mobile che cerca di comunicare utilizza il canale mediante un codice. Analizzeremo meglio W-CDMA nel corso dei successivi capitoli. Lo standard W-CDMA supporta non solo più comunicazioni tra host mobili, ma anche una maggiore velocità visto lo spettro distribuito delle frequenze. In pratica ogni host ha a propria disposizione l'intera banda di frequenza e non più una sola parte, come avveniva con FDMA per AMPS. Le reti UMTS hanno il seguente aspetto:

<!-- to add -->
*In Figura: struttura di una rete UMTS delle reti 3G*

UMTS organizza il tutto in una CN (Core Network), in cui sono presenti i seguenti elementi principali:

- SGSN (Serving GPRS Support Node): gestisce il traffico dati a pacchetto (ossia destinato ad Internet).
- MSC Server (Mobile Switching Centre): smista e gestisce le chiamate vocali.
- MGW (Media GateWay): trasporta e converte i flussi voce.
- CBC (Cell Broadcast Centre): per l'invio di messaggi broadcast.

Il CN è ovviamente collegato attraverso un'apposita infrastruttura al resto della rete mobile. UTRAN (UMTS Terrestrial Radio Access Network) è la rete di accesso vera e propria che utilizza lo spettro radio distribuito (cone W-CDMA) per collegarsi alla rete UMTS globale. Una rete d'accesso a UMTS, anche detta RNS (Radio Network Subsystem) contiene due elementi fondamentali:

- RNC (Radio Network Controller): controlla le stazioni radio.
- Node B: equivalenti delle moderne stazioni base (antenne/celle). Capiremo meglio in seguito che cosa intendiamo con "celle" e con "antenne". 

Arriviamo quindi alla quarta generazione delle reti mobile: le reti 4G (Generation 4). In sostanza, le reti 4G hanno avuto una conferma ufficiale nel 2010, quando l'ITU (International Telecommunication Union) ha approvato gli standard LTE (Long-Term Evolution) e WiMAX per la telefonia. Partiamo da LTE: il suo obiettivo è arrivare a velocità di trasmissione di 1 Gbps, anche mentre l'utente mobile si sposta (ad esempio, mentre l'utente sta viaggiando in auto, oppure in treno). Anche LTE vanta un ampio spettro di frequenze, ma utilizza la tecnica OFDM (Orthogonal Frequency Division Multiplexing), una particolare tecnica di accesso al canale trasmissivo che utilizza non un solo segnale portante, bensì svariate sottoportanti ortogonali tra loro (questa proprietà è poi utile per estrapolare facilmente il segnale di una particolare comunicazione). LTE ha un'efficienza spettrale tre volte superiore rispetto a UMTS e vanta un RTT (Round Trip Time, ne riparleremo quando tratteremo il livello fisico) veramente molto basso per le reti mobile, al di sotto di 10 ms, contro i 70 di UMTS. LTE garantisce una velocità massima di download pari a 326 Mbps, una velocità massima di upload pari a 86 Mbps e latenze molto basse rispetto alle reti 3G. Passiamo a WiMAX. WiMAX (Worldwide Interoperability for Microwave Access) è una tecnologia di telecomunicazione progettata per fornire accesso a Internet a banda larga senza fili su distanze molto maggiori rispetto alla classica tecnologia utilizzata nelle reti LAN, ovvero il Wi-Fi. Basata sullo standard 802.16, una stazione base WiMAX copre da qualche centinaia, fino anche a decine di chilometri. Nelle versioni più avanzate e potenti di WiMAX, si raggiungono velocità anche superiori ai 100 Mbps. WiMAX è particolarmente utile per garantire l'accesso ad Internet nelle aree rurali e nei collegamenti tra sedi aziendali. WiMAX è una vera e propria alternativa alle connessioni cablate (come ADSL e fibra ottica).

Le reti 5G (quinta generazione) rappresentano l'evoluzione delle reti mobili 4G e sono progettate per offrire velocità di trasmissione molto elevate, tempi di risposta estremamente ridotti (latenza di pochissimi millisecondi) e la possibilità di connettere un numero enorme di dispositivi contemporaneamente. L'architettura di una rete 5G è composta principalmente dai dispositivi degli utenti (smartphone, tablet, oggetti appartenenti al mondo IoT -Internet of Things-), dalle stazioni radio chiamate gNodeB, che forniscono la copertura wireless, e dal 5G Core Network, che gestisce autenticazione, mobilità, instradamento dei dati e servizi. Il 5G utilizza diverse bande di frequenza: bande basse per garantire ampia copertura, bande medie per un buon compromesso tra copertura e prestazioni e onde millimetriche (mmWave) per raggiungere velocità molto elevate su distanze più brevi. Tra le tecnologie fondamentali del 5G vi sono:

- Massive MIMO: impiega numerose antenne per aumentare la capacità della rete.
- Beamforming, che concentra il segnale verso specifici utenti migliorando efficienza e qualità della connessione.
- Network slicing: permette di creare reti virtuali dedicate a differenti applicazioni sulla stessa infrastruttura fisica.

Il 5G supporta tre principali categorie di servizi:

- eMBB (Enhanced Mobile Broadband) per Internet ad alta velocità e streaming avanzato.
- URLLC (Ultra-Reliable Low-Latency Communications) per applicazioni che richiedono comunicazioni affidabili e in tempo reale, come la robotica industriale e i veicoli autonomi.
- mMTC (Massive Machine-Type Communications) per la connessione massiva di dispositivi IoT.

Grazie a queste caratteristiche, il 5G non si limita a migliorare la navigazione mobile, ma costituisce una piattaforma tecnologica essenziale per lo sviluppo di città intelligenti, automazione industriale, telemedicina, realtà virtuale e aumentata e molte altre applicazioni innovative.

### 02.07. PSTN (Public Switched Telephone Network)

La PSTN (Public Switched Telephone Network) è la tradizionale rete telefonica pubblica commutata utilizzata per fornire servizi di comunicazione vocale tra utenti situati in qualsiasi parte del mondo. Si basa sulla tecnica del circuit switching (rete a commutazione di circuito), nella quale viene instaurato un circuito dedicato tra chiamante e destinatario per tutta la durata della comunicazione.

La PSTN è composta da una vasta infrastruttura di collegamenti fisici e centrali telefoniche che permettono di instradare le chiamate tra gli utenti. Sebbene originariamente fosse progettata per la trasmissione della voce in forma analogica, nel tempo la rete è stata progressivamente digitalizzata mantenendo però il principio della commutazione di circuito.

La struttura della PSTN può essere suddivisa in tre componenti principali:

- Terminali utente: telefoni fissi, o dispositivi collegati alla rete telefonica. Si tratta dei terminali utilizzati dall'utente finale.
- Rete di accesso: collega gli utenti alla centrale telefonica locale mediante il cosiddetto local loop (ultimo miglio). Analizzeremo vari tipi di local loop nel corso dei successivi paragrafi.
- Centrali di commutazione: nodi della rete che instaurano e gestiscono i circuiti necessari alla comunicazione tra gli utenti. Si parla di commutatori specifici per la telefonia nel caso di PSTN (nel caso di Internet si parla di switch, hub, router, gateway, ecc.).

Il seguente schema semplificato mostra la struttura della rete:

```text
Telefono A
     │
     ▼
Centrale locale
     │
     ▼
Rete di trasporto
     │
     ▼
Centrale locale
     │
     ▼
Telefono B
```

Quando un utente effettua una chiamata, la rete stabilisce un percorso dedicato tra i due telefoni. Tale percorso rimane riservato fino al termine della conversazione, garantendo una larghezza di banda costante e una qualità della comunicazione prevedibile.

### 02.08. Local loop

Un collo di bottiglie (bottleneck) particolarmente critico nelle infrastrutture moderne delle reti di calcolatori è il local loop (collegamento locale), informalmente conosciuto anche con il nome di "ultimo miglio". Il local loop è il collegamento che un determinato provider di connessione Internet, detto anche ISP (Internet Service Provider, fornitore del servizio Internet), effettua tra la propria centralina e l'utente finale. Si tratta di un possibile collo di bottiglia poiché, spesso, un singolo collegamento in realtà non è una connessione point-to-point tra centralina e utente finale, bensì è un collegamento multiplo (spesso di decine, o alcune centinaia di abitazioni) che segue una topologia a bus, a ring, o altro. Di seguito analizzeremo tutti i componenti essenziali del local loop nelle reti telefoniche e non solo.

##### 02.07.01. Modem

Il modem è un dispositivo di livello datalink dello stack TCP/IP che consente l'accesso a Internet all'utente finale, ovvero collega l'host finale all'ultimo miglio. Il modem è un nome particolare, che deriva dalle due espressioni inglesi "modulator" (modulatore di segnale) e "demodulator" (demodulatore di segnale). Il modem in realtà non è presente in ogni tipo di rete, bensì esso sfrutta la rete telefonica di un determinato ISP per trasmettere e ricevere dati in Internet. Il funzionamento di un modem è molto semplice:

- Esso è collegato tra la rete telefonica e l'host finale dell'utente. Spesso, dal punto di vista dell'ISP, il modem rappresenta l'abitazione dell'utente.
- Il modem riceve segnali di tipo analogico dall'esterno dell'abitazione, in quanto esso è collegato alla rete telefonica, che è adatta per la ricetrasmissione di segnali analogici. Affinché possano essere comprensibili dall'host dell'utente, il modem effettua una conversione di tipo ADC (Analog to Digital Conversion), ossia converte il segnale analogico ricevuto in ingresso in segnale digitale. Si tratta dell'operazione di demodulazione.
- Il modem trasmette segnali di tipo analogico all'esterno dell'abitazione. In pratica l'host finale dell'utente, tramite il collegamento (wired -spesso un doppino telefonico-, o wireless -spesso Wi-Fi-), riceve segnali di tipo digitale dall'host dell'utente e li converte in segnali di tipo analogico, adatti per essere trasmessi nella rete telefonica. Ciò che fa il modem in questo caso è detta DAC (Digital to Analog Conversion), ovvero una conversione del segnale da digitale ad analogico. Si tratta dell'operazione di modulazione.

La seguente figura mostra il funzionamento del modem:

<!-- to add -->
*In Figura: il funzionamento del modem*

Quanto velocemente un modem può inviare e ricevere informazioni? Dipende dal tipo di modem:

- Modem analogici (quelli più datati) hanno un tasso di ricezione e ritrasmissione pari a 56 kbs (kilobit per second).
- Modem ISDN hanno un tasso di ricezione e ritrasmissione pari a 128 kbps (kilobit per second).
- Modem ADSL hanno un tasso di ricezione e ritrasmissione pari a 640 kbps (kilobit per second).
- Modem VDSL hanno un tasso di ricezione e ritrasmissione pari a 26 Mbps (Megabit per second).
- Altri tipi di modem più costosi e moderni hanno una velocità di trasmissione dati che variano da 56 kbps a 3.3 Gbps (Gigabit per second).

##### 02.07.02. DSL (Digital Subscriber Line)

La DSL (Digital Subscriber Line) è una tecnologia che utilizza il cavo twisted pair (o doppino telefonico) per trasmettere dati digitali ad alte velocità. Il principio di funzionamento della DSL è molto semplice: si ha a disposizione un'altra vasta rete (la rete telefonica pubblica) costruita nel corso dei decenni di questo secolo e dello scorso secolo, ma essa era inizialmente poco sfruttata perché gestiva solo ed esclusivamente segnali vocali (la voce umana), per cui è possibile utilizzare tutta la capacità della linea telefonica per trasmettere anche un altro tipo di dati sotto forma di segnali analogici, ovvero le comunicazioni digitali in Internet.

La banda di una moderna linea telefonica è molto più ampia rispetto alla banda richiesta dalla voce umana, che varia dai 300 Hz ai 3400 Hz (una porzione relativamente ristretta); tuttavia, per via della natura stessa del doppino telefonico (il rame può supportare una banda di frequenze molto più ampia), la DSL divide la banda totale in:

- Banda per la voce umana.
- Banda per l'upload di dati (invio di dati dall'host finale verso Internet).
- Banda per il download di dati (ricezione di dati da Internet all'host finale).

L'infrastruttura che realizza il collegamento DSL è mostrata nella seguente figura:

<!-- to add -->
*In Figura: infrastruttura fisica che realizza una linea DSL tra l'utente finale e la cabina telefonica*

Partiamo dall'abitazione dell'utente. La linea telefonica collega sia il modem (a sua volta collegato all'host finale, sia esso un laptop, un personal computer, o uno smartphone), sia il telefono di casa. Questo collegamento è tipicamente realizzato in doppino telefonico e collega in modo diretto l'abitazione dell'utente con un centralino dell'ISP (come Vodafone, Wind, o TIM). Nel centralino risiede un dispositivo particolare che prende il nome di DLSAM (DSL Access Multiplexer): si tratta di un multiplexer che è capace di analizzare i segnali ricevuti in input e dividerli (signal splitting) a seconda del loro tipo. Il DSLAM preleva i segnali della voce umana e li consegna alla rete telefonica pubblica. Il DSLAM preleva anche i segnali dati relativi alle comunicazioni tra host su Internet e li invia all'infrastruttura pubblica di Internet (come una backbone in fibra ottica, o verso un altro centralino vicino collegato in qualche altra maniera).

Le linee DSL pure sono anche chiamate SDSL (Symmetric DSL), in quanto le due bande di upload e download hanno la stessa capacità: data $B$ la banda totale, $\frac{B}{2}$ Hz sono associati alla banda per l'upload, mentre $\frac{B}{2}$ Hz sono associati alla banda per il download. Ci sono anche altre tipologie di suddivisione della banda: l'ADSL (Asymmetric DSL) prevede di associare molta più banda al download dei dati (quindi alla ricezione dei dati da Internet), piuttosto che all'upload (quindi all'invio dei dati su Internet), in quanto si basa sul presupposto che un utente medio solitamente scarica molti più dati da Internet rispetto all'invio.

L'ADSL ha riscosso particolare successo. La seguente figura mostra come viene ripartita la banda totale a disposizione fornita dalla linea telefonica in collegamenti di tipo ADSL:

<!-- to add -->
*In Figura: come viene utilizzata la banda totale nell'ADSL*

L'ADSL viene utilizzata per trasmettere e ricevere dati di natura digitale su Internet e ripartisce la banda totale in 256 canali, ciascuno di un'ampiezza pari a 4.3125 kHz. Le aree principali della banda totale sono le seguenti:

- La banda 0-4 kHz è riservata ai segnali vocali dell'essere umano, quindi per la telefonia. Normalmente servirebbero dai 300 Hz ai 3400 Hz per la voce umana, tuttavia si è mantenuto un certo "scarto" sia per comodità di implementazione dei canali di comunicazione nell'ADSL, sia per supportare un certo rumore (noise). I segnali telefonici coprono 1 solo canale.
- La banda che va dai 4 Hz ai 25.875 kHz non viene utilizzata, in quanto serve come guard band (banda di guardia) per ridurre il più possibile interferenze e rumore. Questa banda copre circa 5 canali.
- La banda che va dai 25.875 kHz ai 138 kHz è riservata all'upload di dati, ossia all'upstream. L'upstream copre circa 25 canali.
- La banda che va dai 138 kHz fino ai 1104 kHz (o 1.104 MHz) è riservata al download dei dati, ossia al downstream. Il downstream copre circa 224 canali.

I canali, nell'ambito delle linee ADSL, viene anche detto tono.

##### 02.07.03. HFC (Hybrid Fiber-Coax)

HFP (Hybrid Fiber-Coaxial) è una rete che utilizza due mezzi trasmissivi fisici (fibra ottica e cavo coassiale) per connettere uno, o più clienti tipicamente di un intero quartiere alla una stazione base dell'ISP, in modo da collegarli ad Internet. Immaginiamoci un quartiere, costituito da più vie, ognuna costituita da più abitazioni. Lungo ciascuna via passa un grosso cavo coassiale a cui sono connessi tutte le abitazioni: ogni utente, in pratica, condivide lo stesso cavo coassiale degli utenti che abitano nella stessa via. Maggiore è il numero di utenti collegati, minore è la banda a disposizione dell'utente (giocare alle quattro del mattino, o guardare la TV alle due di notte permetteerebbe all'utente, invece, di utilizzare l'intera banda disponibile). Tutti i cavi coassiali colleganti ciascuno un'apposita via convergono in una singola stazione che prende il nome di ON (Optical Node): si tratta di una giunzione da cui entra il cavo coassiale e furoriesce una fibra ottica. Questi ON possono essere posizionati alla fine di ciascuna via, oppure direttamente all'interno del centralino. Soprattutto per le vie lunghe, si utilizzano numerosi amplificatori posizionati lungo la via stessa, in modo da garantire sempre un segnale sufficientemente pulito e potente. Ogni ON converge nel cosiddetot DH (Distribution Hub), ossia una centrale che si occupa di accogliere tutte le linee di più quertieri. Tutto questo scenario è presentato nella seguente figura:

<!-- to add -->
*In Figura: ultimo miglio che utilizza HFC (Hybrid Fiber-Coaxiall)*

##### 02.07.04. FTTH (Fiber to the Home) e FTTC (Fiber to the Cabin)

Nel contesto delle telecomunicazioni, FTTH (Fiber To The Home) è una architettura di accesso in cui la fibra ottica arriva direttamente fino all’abitazione o sede dell’utente finale. È una delle evoluzioni del local loop (o “ultimo miglio”), cioè il tratto di rete che collega la centrale dell’operatore all’utente.

Il local loop con tecnologia DSL, o ADSL è realizzato completamente in doppino telefonico (rete telefonica tradizionale). Con FTTH viene sostituito quasi interamente da fibra ottica e ciò rappresenta una reale innovazione dal punto di vista delle reti di calcolatori, per via di tutti i vantaggi offerti dalla fibra ottica stessa (già citati in precedenza). Il local loop che sfrutta la fibra ottica può essere di due tipi principali:

- AON (Active Optical Network): in cui ogni utente ha un collegamento dedicato, oppure passa tramite apparati Ethernet attivi. Ciascun utente ha un'intera banda dedicata ed il numero di utenti collegati non inficia sulla capacità di banda utilizzabile dall'utente.
- PON (Passive Optical Network): si tratta della tecnologia oggi più diffusa nelle reti FTTH residenziali, in cui tutti gli utenti collegati ad una centralina dell'ISP sfruttano tutti la stessa fibra ottica, ovvero lo stesso collegamento. La banda è condivisa: maggiore è il numero di utenti collegati a Internet, minore è la banda che ciascun utente può utilizzare.

La figura seguente mostra come è organizzata una soluzione FTTH che sfrutta le reti in fibra ottica di tipo PON:

<!-- to add -->
*In Figura: il modo in cui è organizzata una soluzione FTTH*

Esistono anche soluzioni FTTC (Fiber To The Cabin), ma non le tratteremo qui in questo paragrafo. L’architettura di una PON è composta dalle seguenti unità principali:

- Il primo componente della lista è l'OLT (Optical Line Terminator): si tratta della terinazione del local loop, che collega tipicamente da una singola abitazione a svariate decine di abitazioni, talvolta anche centinaia. Rappresenta il punto finale della rete locale, o LAN (che collega una via, o un quartiere) e l'inizio della backbone (dorsale), che può essere in fibra ottica, o in qualche altra tecnologia.
- Dopo l'OLT, come si può osservare nella precedente figura, abbia l'ODF (Optical Distribution Frame), ossia un quadro di distribuzione ottica che viene utilizzato per terminare le linee ottiche di ciascun utente e riorganizzare tutti i segnali provenienti dalle abitazioni in un'unica fibra (che tipicamente collega l'ODF all'OLT). OLT e ODF risiedono entrambi nella centralina dell'ISP, coem Telecom, o TIM.
- Passiamo al collegamento tra la centralina dell'ISP e lo splitter ottico: questo collegamento consiste in un fascio di fibre ottiche che, tipicamente, stanno in rapporto 1:16 con le linee degli utenti. In pratica una fibra trasporta 16 segnali differenti provenienti da 16 abitazioni differenti. Lo splitter ottico 1:16 è capace di interpretare ciascun segnale e consegnarlo all'abitazione corretta. Lo splitter viene anche detto POS (Passive Optical Splitter).
- Infine, dallo splitter ottico partono 16 linee, ognuna diretta verso un apposito ONU (Optica Network Unit): quest'ultimo rappresenta l'abitazione di un singolo utente.

### 02.08. Dispositivi di rete

Per dispositivi (o apparati) di rete intendiamo tutti quei dispositivi deputati in qualche modo a gestire una, o più comunicazioni all'interno di una rete di calcolatori. I dispositivi di rete si suddividono in due grandi famiglie:

- Gli apparati del livello datalink dello stack TCP/IP, che hanno il compito di instradare e gestire comunicazioni tra host appartenenti a alla rete locale.
- Gli apparati del livello network dello stack TCP/IP, che hanno il compito di instradare e gestire comunicazioni tra host appartenenti a reti diverse.

Nel corso dei successivi paragrafi prenderemo in esame alcuni apparati di rete di entrambe le categorie.

##### 02.08.01. Repeater

Il repeater (ripetitore) è un dispositivo del livello physical dello stack TCP/IP che accetta un segnale in ingresso e lo rigenera, ovvero produce in output lo stesso segnale in ingresso cercando di rigenerare la sua forma originale, attenuandone il rumore, per quanto possibile. Sebbene il compito sia molto semplice per i segnali digitali, esso risulta essere molto più difficile per i segnali analogici, per via della natura stessa di questo tipo di segnali, sinusoidali e curvilinei. Il repeater:

- Riceve il segnale attenuato in ingresso.
- Attraverso apposite tecniche di rigenerazione del segnale, riconsoce la sua forma originale.
- Trasmette il segnale rigenerato in output.

Il repeater, fondamentalmente, ha l'importante compito di allungare la distanza massima percorribile dalla comunicazione. Di seguito uno schema di una rete che sfrutta un repeater per rigenerare il segnale:

<!-- to add -->
*In Figura: ecco come viene utilizzato un repeater per rigenerare un segnale*

In realtà il repeater può essere utilizzato per supportare comunicazioni in vari layer dello stack TCP/IP: un repeater posto fra due reti viene utilizzato dal livello network, mentre un repeater posto tra due switch all'interno della stessa LAN opera a livello datalink.

##### 02.08.02. Hub

L'hub è un dispositivo del livello physical dello stack TCP/IP che supporta e gestisce le comunicazioni tra host posti all'interno della stessa rete. Un hub è un dispositivo multiporta, ossia ha due, o più porte a cui sono collegati gli host. A seconda della topologia della LAN, a una porta può essere collegato un solo host (topologia a stella), oppure ad ogni porta possono essere collegati più host (topologia ibrida). La seguente figura mostra la classica topologia a stessa in cui il dispositivo centrale è un hub:

<!-- to add -->
*In Figura: la topologia a stella di una rete LAN basata su un hub*

Il comportamento di un hub è forse il più semplice tra gli apparati di rete che andremo ad analizzare: quando riceve un segnale in ingresso da una porta, esso lo ritrasmette su tutte le altre porte (quindi realizza quella che, normalmente, viene chiamata comunicazione broadcast). Per esempio, se si hanno gli host A, B e C collegati ognuno a una porta (rispettivamente 1, 2 e 3) dell'hub H, allora:

- Se A invia un segnale a B, lo riceve anche C in quanto l'hub ritrasmette il segnale sia sulla porta 2, sia sulla porta 3.
- Se C invia un segnale a sé stesso (ad esempio un semplice ping per testare il collegamento con l'hub H), viene ricevuto anche da A e B, in quanto l'hub ritrasmette il segnale sulle porte 1 e 2.

Questo comportamento genera un traffico elevato e, talvolta, non necessario. Inoltre, dal punto di vista logico, avere un huhb centrale non è poi molto diverso dall'avere un unico bus a cui tutti i dispositivi della rete sono collegati. L'hub inoltre non legge il contenuto del segnale: non sa a chi è diretto un segnal e non ha alcuna forma d'intelligenza per quanto riguarda l'instradamento dei pacchetti. Tutti i dispositivi collegati all'hub condividono la stessa banda: questo vuol dire che più si hanno dispositivi collegati alla rete, minore è la porzione di banda che ciascun dispositivo può utilizzare. Se la banda a disposizione è indicata con $B$, ciascuno degli $N$ dispositivi avrà solo una frazione $\frac{B}{N}$ della banda. Se due, o più dispositivi cercano di trasmettere il proprio segnale nello stesso istante, potrebbero verificarsi delle collisioni. In pratica l'intera rete, dotata di un hub, appartiene allo stesso dominio di collisione.

Un'altra caratteristica interessante è il modo in cui lavora un hub: in half-duplex. La comunicazione half-duplex si ha quando, posti due dispositivi A e B in comunicazione tra loro, in un determinato istante solo uno dei due può trasmettere (o ricevere) un segnale. Non esiste una comunicazione bidirezionale contemporanea tra A e B. Un hub può svolgere anche il ruolo di repeater all'interno delle LAN, in quanto esso è capace di rigenerare il segnale.

##### 02.08.03. Bridge

Il bridge è un dispositivo che opera a livello datalink dello stack TCP/IP che collega due, o più reti LAN. Normalmente, un bridge (ponte, in italiano) ha due sole porte: alla porta 1 è collegata la LAN1, mentre alla porta 2 è collegata la LAN2. A differenza dell'hub, il bridge presenta un comportamento intelligente, in quanto esso associa il numero di porta a una lista di indirizzi MAC: alla porta 1 sono associati tutti gli indirizzi MAC dei dispositivi della LAN1, mentre alla porta 2 sono associati tutti gli indirizzi MAC dei dispositivi presenti in LAN2.

Il bridge opera nel seguente modo:

- Riceve un segnale in ingresso in una porta, per esempio la porta 1.
- Esso accede solo ai dati del pacchetto relativi al livello datalink: legge l'indirizzo MAC del destinatario.
- Consulta la sua tabella degli indirizzi MAC:
    - Se il destinatario appartiene alla LAN1, ritrasmette il segnale alla LAN1.
    - Se il destinatario appartiene alla LAN2, ritrasmette il segnale alla LAN2.

La seguente figura mostra una situazione in cui due LAN (LAN1 a sinistra e LAN2 a destra), ognuna composta da tre dispostivi (LAN1 da A, B e C; LAN2 da D, E e F), sono collegate da un bridge:

<!-- to add -->
*In Figura: le due reti locali LAN1 e LAN2 collegate attraverso un bridge*

Da notare la tabella costruita automaticamente dal bridge mostrata in figura. Il bridge aggiorna continuamente la sua tabella interna: ognivolta che legge i MAC sorgente e destinatario, se essi non sono presenti in tabella, aggiunge il MAC sorgente ed il numero di porta dal quale ha ricevuto il segnale alla propria tabella. Se il bridge non conosce il destinatario, ritrasmette in broadcast il segnale (cosicché quest'ultimo possa rispondere al mittente e il bridge stesso possa aggiornare la sua tabella).

Il bridge ha due distinti domini di collisione: uno per ogni rete locale collegata. I domini di collisione possono avvenire solo ed esclusivamente all'interno delle LAN, non all'interno del bridge. Inoltre, ciascuna LAN ha la propria topologia, che è completamente trasparente al bridge (ad esempio può essere una topologia ring, star, mesh, o bus).

##### 02.08.04. Switch

Uno switch è un dispositivo del livello datalink dello stack TCP/IP che collega più host posti nella stessa LAN ed inoltra il traffico solo ed esclusivamente verso il dispositivo (o verso i dispositivi) a cui sono destinati i dati. Come il bridge, anche lo switch al suo interno mantiene una tabella costituita da due informazioni principali:

- L'indirizzo MAC del dispositivo.
- La porta alla quale è collegato il dispositivo.

La tabella presenta tanti record quanti sono i dispositivi collegati allo switch. Quando lo switch riceve un pacchetto in ingresso in una determinata porta, esso legge anzitutto l'indirizzo MAC del destinatario del pacchetto. Se esso non trova alcun destinatario con quell'indirizzo MAC nella sua tabella, trasmette il messaggio in broadcast a tutte le porte, tranne quella in ingresso: si tratta della politica UUF (Unknown Unicast Flooding). Se, invece, trova una corrispondenza all'interno della sua tabella, allora legge il numero di porta associato all'indirizzo MAC del destinatario ed inoltra il pacchetto solo ed esclusivamente a quella porta. Normalmente, se un dispositivo viene scollegato da una porta e ricollegato a un'altra, lo switch è in grado di capire che non può esistere lo stesso indirizzo MAC per più porte, per cui procede ad eliminare il vecchio record nella tabella e crearne uno aggiornato.

Lo switch è un dispositivo intelligente, forse il più intelligente incontrato finora, in quanto esso è in grado di instradare effettivamente i pacchetti dati, di fatto scegliendo un percorso opportuno. Una tipica topologia a stella che sfrutta uno switch è la seguente:

<!-- to add -->
*In Figura: una tipica topologia a stella in cui il dispositivo centrale è lo switch*

Da notare la tabella dello switch: il dispositivo A con MAC A_MAC_ADDRESS è associato alla porta 1, il dispositivo B con MAC B_MAC_ADDRESS alla porta 2 ed il dispositivo C con MAC C_MAC_ADDRESS alla porta 3. In commercio esistono switch con tantissime funzionalità aggiuntive (come la rilevazione delle collisioni e la gestione ottimale del traffico, con algoritmi di instradamento del livello datalink molto sofisticati). Tipicamente, uno switch ha da alcune unità a svariate decine di porte.

Lo switch, rispetto all'hub, garantisce un traffico molto minore e realizza realmente le comunicazioni unicast (in cui il messaggio è diretto a un solo host). Si tratta di un dispositivo molto veloce, che permette una maggiore velocità di trasmissione dati e un numero sensibilmente minore di collisioni. A differenza dell'hub, in cui la rete LAN intera è un collision domain, lo switch ha tanti collision domain quante sono le sue porte: se un solo host è collegato a una porta, allora è teoricamente impossibile che accada una collisione.

Due sono le politiche che governano l'inoltro dei pacchetti da parte dello switch:

- Store and forward: prima lo switch attende che il pacchetto arrivi completamente e sia interamente memorizzato in una sua memoria, che prende il nome di buffer d'arrivo. Successivamente, lo switch elabora il pacchetto leggendo il MAC del destinatario e consultando la sua tabella. Infine, esso lo trasmette nella porta in cui risiede il destinatario.
- Cut through: lo switch attende che solo una parte del pacchetto sia stata completamente trasmetta e risieda nel suo buffer, dopo di ché procede alla sua elaborazione ed infine alla sua trasmissione solo alla porta in cui risiede il destinatario. Questo tipo di modalità consiste in due forme differenti:
    - Fragment-free: in questa modalità si attendono i primi 64 Byte del pacchetto (il cosiddetto header, che contiene molte altre informazioni di servizio, oltre all'indirizzo MAC di destinazione). Poi lo switch procede alla sua elaborazione ed al suo invio nella porta opportuna.
    - Fast-forward: in questa modalità si attendono solo i primi Byte del pacchetto, ovvero i Byte minimi ed indispensabili per la lettura dell'indirizzo MAC di destinazione. Poi lo switch procede alla sua elaborazione ed all'invio del pacchetto.

La seugente figura mostra la quantità di Byte analizzati del pacchetto ricevuto in ingresso per le tre modalità di inoltro analizzate in precedenza:

<!-- to add -->
*In Figura: "quntità" del pacchetto analizzato nelle tre varie modalità*

##### 02.08.05. Router

Un router è un dispositivo di rete che ha il compito di instradare i pacchetti dati tra reti differenti, per questo esso è classificato come dispositivo del livello network dello stack TCP/IP, poiché esso deve necessariamente conoscere la topologia delle reti. Il router sfrutta gli indirizzi IP per decidere il percorso migliore da seguire per raggiungere una destinazione.

Il router collega reti diverse tra loro, ad esempio una rete domestica e Internet, oppure due reti aziendali. Ogni interfaccia del router appartiene a una rete differente e possiede un proprio indirizzo IP: esattamente come lo switch e l'hub, un router possiede più interfacce (o porte).

Quando un pacchetto arriva al router, esso legge l’indirizzo IP di destinazione contenuto nell’header del pacchetto. Successivamente consulta la propria tabella di routing, che contiene informazioni sui percorsi disponibili verso le varie reti. In base a queste informazioni sceglie l’interfaccia di uscita più adatta e inoltra il pacchetto verso il nodo successivo. In realtà la tabella di routing è relativamente semplice: ciascun record è composto dall'indirizzo IP di destinazione e dall'interfaccia che lo collega.

La tabella di routing può contenere rotte statiche, configurate manualmente dall’amministratore della rete (conoscenza statica della topologia di rete), oppure rotte dinamiche apprese automaticamente tramite protocolli di routing (come RIP, OSPF o BGP, che studieremo ampiamente nel corso dei successivi paragrafi).

La seguente figura mostra la configurazione di un router che collega quattro reti LAN differenti: LAN1 presenta una tipologia a bus, LAN2 una topologia a stella (che sfrutta uno switch), mentre le due reti LAN3 e LAN4 sono collegate per mezzo di un bridge, a sua volta collegato a un router.

<!-- to add -->
*In Figura: un esempio di router che collega quattro reti LAN (LAN1, LAN2, LAN3 e LAN4)*

Il router non si limita a inoltrare i pacchetti, ma può anche eseguire altre funzioni, tra cui: NAT, firewalling, gestione della QoS, filtraggio del traffico e gestione delle VLAN. Il NAT è molto utilizzato nelle reti domestiche perché consente a più dispositivi privati di condividere un singolo indirizzo IP pubblico. In questo caso il router modifica gli indirizzi IP dei pacchetti quando transitano tra rete privata e rete pubblica. Per trasmettere correttamente un pacchetto sulla rete locale, il router utilizza il protocollo ARP per associare un indirizzo IP a un indirizzo MAC fisico. In questo modo può consegnare il frame Ethernet al dispositivo successivo. Analizzeremo tutti questi protocolli nel corso dei successivi capitoli.

Dal punto di vista logico, il routing può seguire diversi criteri. In genere il router seleziona il percorso con metrica migliore, ad esempio il minor numero di hop, il costo minore o la latenza più bassa. Una metrica è un valore numerico che indica quanto è soddisfacente, secondo il router, un determinato percorso relativamente ad una destinazione. I protocollid di routing dinamico permettono ai router di scambiarsi informazioni sulla topologia della rete e di adattarsi automaticamente in caso di guasti, o variazioni dei percorsi disponibili.

Infine, un router non deve necessariamente essere implementato via hardware: può essere un software eseguito da un vero e proprio computer posto tra una rete e l'altra, oppure può essere un dispositivo router (come i router CISCO) creato appositamente per il routing dei pacchetti. Analizzeremo anche questo aspetto quando parleremo del livello network dello stack TCP/IP.

##### 02.08.06. Gateway

Adesso parliamo di un dispositivo molto simile al router: il gateway. Il gateway, nelle reti di calcolatori, è un dispositivo hardware, o software che permette la comunicazione tra reti diverse utilizzando protocolli differenti, o comunque fungendo da punto di accesso verso un’altra rete. Un router, infatti, solitamente implementa uno specifico algoritmo di routing tra le varie reti che collega e può venire utilizzato per realizzare reti MAN, o WAN. Differentemente, un gateway è un dispositivo che collega reti più grandi, ossia reti che sfruttano protocolli differenti per l'instradamento dei pacchetti, o che rappresentano due domini distinti nell'ambito delle reti di calcolatori (capiremo meglio che cosa intendiamo con il termine "dominio" nel corso dei prossimi capitoli).

Il gateway riceve i dati provenienti da una rete, li interpreta e li inoltra verso la rete destinataria corretta. In molti casi esegue anche conversioni di protocollo, traduzione degli indirizzi o controlli di sicurezza. In pratica il gateway è un punto di collegamento tra reti anche molto differenti. Oltre a instradare i dati, può tradurre protocolli, formati, oppure modalità di comunicazione tra sistemi incompatibili.

Le principali funzioni di un gateway sono:

- Collegare reti differenti.
- Instradare il traffico dati.
- Tradurre protocolli e indirizzi.
- Controllare accessi e sicurezza.
- Consentire la comunicazione tra sistemi incompatibili.

Esistono diversi tipi di gateway:

- Gateway di rete: collega reti diverse.
- Gateway VoIP: converte comunicazioni telefoniche tradizionali in traffico IP, utilizzabile in Internet e nelle moderne infrastrutture basate su fibra ottica e onde elettromagnetiche.
- Gateway applicativi: filtrano e controllano traffico di specifiche applicazioni e tipicamente vengono implementati via software.
- Gateway IoT: collegano dispositivi intelligenti a reti o servizi cloud.

Il gateway si distingue dal router perché il router si occupa principalmente di instradare pacchetti tra reti compatibili, mentre il gateway può anche effettuare conversioni e adattamenti tra sistemi differenti. In una configurazione IP, il “default gateway” è l’indirizzo del dispositivo a cui un host invia i pacchetti destinati a reti esterne alla propria LAN. Senza gateway, reti con protocolli e/o struttura differenti non potrebbero comunicare correttamente tra loro.

### 02.09. Modulazione e demodulazione del segnale

Nell'ambito della modulazione e della demodulazione del segnale sono due le conversioni che vengono eseguite:

- Quando si vuole adattare un segnale digitale su un mezzo che supporta solo portanti analogiche (trasmissione analogica), si esegue sempre una conversione ADC (Analog-to-Digital Conversion). Il segnale digitale, mediante l'ADC, viene convertito in un segnale sinusoidale.
- Quando si riceve un segnale analogico che deve essere convertito in un segnale digitale si esegue sempre una conversione DAC (Digital-to-Analog Conversion). Il segnale analogico, mediante la DAC, viene convertito in un segnale digitale e l'informazione viene ricostruita in termini di bit.

Un qualsiasi mezzo trasmissivo ha una certa frequenza, misurata in Hz. La frequenza determina la velocità alla quale si possono trasmettere i dati: un doppino telefonico che lavora a 100 MHz può idealmente cambiare stato 100 milioni di volte al secondo, mentre una fibra ottica da 1 GHz può idealmente trasmettere 1 miliardo di bit alla volta (anche se non è proprio così, ma per adesso sorvoliamo). La logica secondo il quale viene attuata la modulazione è detta logica:

- Logica positiva: attribuisce tipicamente i valori alti di tensione al valore logico 1, mentre i valori bassi allo 0.
- Logica negativa: attribuisce tipicamente i valori alti di tensione al valore logico 0, mentre i valori bassi allo 1 (il contrario rispetto alla logica positiva).

La scelta di utilizzare la logica positiva, o negativa dipende dall'effettiva implementazioned del mezzo trasmissivo e della rete.

Altri due concetti fondamentali sono quelli di baseband e passband. La baseband (detta anche banda base) è rappresentata dal segnale trasmesso nella sua forma originale, senza modulazione su una portante; occupa frequenze vicine a 0 Hz ed è tipico delle comunicazioni cablate come Ethernet. In pratica si tratta del segnale nudo e crudo, che non subisce alcun tipo di variazione, adattamento, o trasformazione per fini trasmissivi. La passband (detta anche banda passante) è il segnale restituito a seguito della modulazione del segnale originale, ovvero il segnale basato su un segnale portante dotato di una frequenza più alta, in modo da poter essere trasmesso efficacemente attraverso un canale radio o altri mezzi di comunicazione.

Ma adesso veniamo al dunque: che cosa significa modulare un segnale? Un canale trasmissivo può essere dotato, o no di un segnale portante: si classificano quindi i canali trasmissivi senza e con portante (e questi ultimi si suddividono in segnali con una, o più portanti). Un segnale portante è un segnale analogico periodico e ripetitivo che funge da clock di trasmissione, dotato quindi di una certa frequenza. L'operazione di modulazione significa, dato il segnale originale, modificare una delle caratteristiche della portante (ampiezza, frequenza, fase) in modo da riprodurre il contenuto informativo presente nel segnale originale. In pratica la modulazione permette di passare dalla baseband (segnale originale) alla passband (segnale modulato). Esistono quindi varie tecniche di modulazione del segnale, esaminate di seguito.

Le quattro tecniche principale di modulazione del segnale sono descritte di seguito (come riferimento prendere la figura successiva al seguente elenco):

- ASK (Amplitude Shift Keying): prevede di variare solo l'ampiezza della portante, mentre frequenza e fase rimangono invariate. Nella logica positiva solitamente si sfrutta un'ampiezza elevata per trasmettere un 1, mentre un'ampeizza nulla per trasmettere uno 0 logico. La modulazione ASK è semplice da implementare e richiede circuiti relativamente poco complessi, motivo per cui è stata utilizzata in diverse applicazioni di comunicazione digitale a bassa velocità e nei sistemi di identificazione a radiofrequenza (come i dispositivi RFID ed alcune reti di sensori per l'IoT). Ma ASK è molto sensibile al rumore, oltre che causare problemi di desincronizzazione per le lunghe sequenze di 0 (in cui il segnale è costantemente nullo).
- FSK (Frequency Shift Keying): prevede di variare solo la frequenza della portante, mentre ampiezza e fase rimangono invariate. Nella logica positiva solitamente si utilizza una frequenza maggiore per trasmettere un 1, mentre una frequenza minore trasmette uno 0 logico. In realtà la FSK sfrutta altre due sottoportanti (la cui frequenza è un multiplo della portante di base): la portante con frequenza maggiore viene utilizzata per l'1, mentre la portante con la frequenza minore viene utilizzata per lo 0. Sebbene sia molto meno sensibile al rumore ed abbia una buona affidabilità, essa richiede una banda di frequenze maggiore ed ha anche una minore efficienza spettrale.
- PSK (Phase Shift Keying): prevede di variare solo la fase della portante, mentre ampiezza e frequenza rimangono inalterate. Un segnale è dotato di un periodo, solitamente indicato con $t$ e misurato in s (secondo). Quando il segnale è allo 0% del suo periodo, allora la sua fase è di 0°, quando è al 25% la sua fase è di 90°, al 50% è di 180° (la metà di un angolo giro, ossia un angolo piatto), al 75% la sua fase è di 270° e, infine, quando è al 100% la sua fase è di 360° (un angolo giro, che coincide con il punto iniziale). Per trasmettere un determinato bit si utilizza un cambiamento di fase all'inizio del periodo della portante: per esempio una fase di 180° per trasmettere l'1, mentre la trasmissione di uno 0 logico non ha alcun cambiamento di fase. Usando 4 fasi differenti si possono anche trasmettere 2 bit alla volta: 0° per trasmettere 00, 90° per trasmettere 01, 180° per trasmettere 10 e, infine, 270° per trasmettere 11.
- QAM (Quadrature Amplitude Modulation): è una tecnica di modulazione digitale che combina la modulazione di ampiezza ASK e PSK. L'informazione viene trasmessa variando contemporaneamente sia l'ampiezza sia la fase della portante, consentendo di rappresentare più bit con un singolo simbolo. Grazie a questa caratteristica, la QAM offre un'elevata efficienza spettrale, permettendo di trasmettere grandi quantità di dati utilizzando una banda relativamente ridotta. Esistono diverse versioni della QAM, come 16-QAM, 64-QAM, 256-QAM e superiori, dove il numero indica quanti simboli distinti possono essere trasmessi. Maggiore è il numero di simboli, maggiore è la velocità di trasmissione, ma aumenta anche la sensibilità al rumore.

<!-- to add -->
*In Figura: tecniche ASK, FSK e PSK di modulazione del segnale portante*

Nella seguente figura viene mostrata la tecnica 16-QAM, in grado di trasferire 16 bit in un singolo periodo della portante:

<!-- to add -->
*In Figura: la tecnica 16-QAM è in grado di trasmettere ben 16 bit in un singolo periodo del segnale portante*

### 02.10. Multiplexing del canale

Il multiplexing del canale (anche noto come channel multiplexing) è compiuto da un apposito apparato (il multiplexer) il cui obiettivo principale è garantire che più coppie di host possano essere poste in comunicazione ottimizzando quanto più possibile l'utilizzo del canale trasmissivo. Detto in altro modo, il multiplexing permette a più coppie di dispositivi di utilizzare lo stesso canale di comunicazione, ma in differenti porzioni di esso. Invece di dedicare un intero canale a un solo utente, o servizio, il multiplexing permette di combinare più comunicazioni sullo stesso collegamento. All'estremità ricevente, un apparato chiamato demultiplexer effettua il cosiddetto demultiplexing, azione che consiste nella separazione dei vari segnali.

Il modello che seguiamo qui per comprendere il multiplexing del canale è rappresentato nella seguente figura:

<!-- to add -->
*In Figura: il multiplexing del canale trasmissivo*

La comunicazione inizia con il mittente di una comunicazione, che genera il messaggio. Questo arriva in input ad un apparecchio chiamato MUX (MUltipleXer) che combina tutti i segnali in un'unica linea di trasmissione. Tale linea arriva fino al DEMU (DEMUltipleXer), che effettua l'operazione uguale ed opposta del MUX: preleva tutte le componenti di segnali presenti nella singola linee e le suddivide in più linee, ognuna diretta all'interessato: il destinatario della comunicazione. 

Esistono varie tecniche di multiplexing del canale, di seguito brevemente descritte:

- FDM (Frequency Division Multiplexing): in cui la banda viene suddivisa in più sottobande, ognuna dedicata ad un'apposita comunicazione (coppia di host mittente e destinatario). Alcune porzioni del canale potrebbero non essere utilizzate (ad esempio se i due host non si stanno scambiando alcuna informazione). Inoltre, il numero di host che possono comunicare è molto limitato.
- CDM (Code Division Multiplexing): in cui ogni host posto in comunicazione può utilizzare l'intera banda messa a disposizione dal canale trasmissivo, in quanto dispone di un codice univoco che viene combinato con il segnale trasmesso nel canale stesso, in modo che il ricevente riesca ad estrapolare correttamente il segnale. Si tratta di una tecnica molto innovativa che, a differenza della FDM, non spreca inutilmente porzioni del canale, ma anzi ne favorisce il suo completo utilizzo, vista l'intera banda a disposizione. 
- TDM (Time Division Multiplexing): in cui il tempo viene suddiviso in quanti temporali chiamati slot. Uno slot è associato a un particolare host posto in comunicazione e per questo vengono tipicamente numerati da 1 a N. Un frame (o data frame) è costituito da tutti gli slot utilizzati dagli host per comunicare. Uno slot concede l'intera banda delle frequenze a un particolare host, ma un tempo molto limitato. Anche TDM, come FDM, consente un numero molto limitato di host, ma ciascun host ha tutta la banda a disposizione (che difficilmente utilizzerà); quindi TDM potrebbe comunque causare un sottoutilizzo del canale trasmissivo. Solitamente viene utilizzata una politica RR (Round Robin) per consentire a tutti gli host collegati di trasmettere dati.
- WDM (Wavelength Division Multiplexing): WDM è molto simile a FDM, ma viene utilizzata con particolari mezzi trasmissivi (fibre ottiche) dotati di una portante avente una frequenza molto maggiore, anche dell'ordine di vari GHz.

La seguente figura mostra le varie tecniche di multiplexing del canale:

<!-- to add -->
*In Figura: le varie tecniche di multiplexing del canale di comunicazione*

Da notare come WDM e FDM vengono rappresentate come bande trasversali, mentre TDM come bande longitudinali (dei piccoli rettangoli).

### 2.11. Codifica di linea

La codifica del segnale (detta anche codifica di linea) è il processo mediante il quale le informazioni vengono trasformate in una forma adatta alla trasmissione o alla memorizzazione. In una rete di comunicazione, la codifica converte i dati digitali in segnali elettrici, ottici, o radio che possono essere trasportati dal mezzo trasmissivo. Questa operazione può essere effettuata dal MUX, o da un apparecchio presente all'interno del MUX. La decodifica di linea è l'operazione opposta a quella appena descritta: è il processo mediante il quale il segnale trasmesso sul canale viene convertito in informazioni adatte ad essere elaborate dall'host destinatario.

Lo scopo principale della codifica è rappresentare i livelli logici digitali 0 e 1 in modo che possano essere trasmessi in maniera efficiente e affidabile, facilitando la sincronizzazione tra trasmettitore e ricevitore e riducendo gli errori dovuti al rumore. La seguente figura mostra vari modi possibili per realizzare una codifica di linea efficiente:

<!-- to add -->
*In Figura: alcune tecniche di codifica di linea*

Le tecniche principalmente utilizzate per la codifica di linea sono:

- NRZ (Non-Return Zero): nonostante il nome, questa codifica associa due livelli differenti di tensione a ciascun bit, per esempio +5V per trasmettere un 1 logico e +0V per trasmettere uno 0 logico (in logica positiva). Questa codifica è afflitta da un grave problema: sequenze di bit uguali possono produrre un segnale che permane sempre nello stesso livello di tensione, causando disallineamenti e desincronizzazione tra trasmettitore e ricevitore. Ha un basso consumo di energia elettrica.
- AMI (Alternate Mark Inversion): in cui i valori 1 assumono livelli di tensione alternati tra +5V e -5V, ma i bit 0 rimangono sempre a +0V. Sebbene anche AMI abbia un basso consumo di energia elettrica, comunque per lunghe sequenze di bit 0 si possono avere problemi di desincronizzazione del segnale.
- Manchester: in cui vi è una transizione a metà di ciascun periodo. Per esempio: un segnale che inizia dal livello basso ed a metà passa a livello alto potrebbe rappresentare un 1, mentre un segnale che passa dal livello alto al livello basso potrebbe rappresentare uno 0. Sebbene non causi alcuna desincronizzazione, richiiede comunque il dobbio della banda (frequenza duplicata rispetto al segnale originale).
- Differential Manchester: molto simile alla codifica Manchester, è un codice di linea digitale in cui i dati binari vengono memorizzati in base alla presenza, o assenza di una transizione di segnale all'inizio del periodo di clock. A differenza della codifica Manchester standard (dove il valore del bit dipende dalla direzione della transizione centrale), la Manchester differenziale combina le informazioni sui dati e sul clock utilizzando esclusivamente le variazioni dello stato elettrico.
- 4B/5B: codifica in 4 bit di dati vengono mappati su una stringa di 5 bit di dati in modo opportuno ed intelligente, valutando le proprietà fisiche del canale di comunicazione. Questo metodo serve a evitare che il segnale rimanga piatto troppo a lungo, garantendo che ci siano sempre abbastanza cambi di tensione per mantenere sincronizzati i computer. Per esempio, se i bit dati sono tutti 1 (o la maggior parte sono a 1), il quinto bit aggiunto dalla codifica 4B/5B può essere 0, in modo da causare segnali piatti troppo a lungo.