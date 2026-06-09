# 03. Datalink Layer

### 03.01. Introduzione

Il livello datalink dell'architettura TCP/IP è il secondo livello dello stack, posizionato direttamente sopra il livello physical. Si tratta del primo livello in cui iniziamo a parlare di servizi offerti al livello superiore e servizi accettati dal livello superiore (il livello network dello stack TCP/IP, che analizzeremo nel prossimo capitolo).

##### 03.01.01. Panoramica del datalink layer dello stack TCP/IP

La IEEE ha pubblicato numerosi standard per questo livello, tra i quali spiccano i seguenti (che costituiscono una valida panoramica per comprendere che cosa fa nel concreto il livello datalink):

- 802: panoramica del livello datalink dello stack TCP/IP.
- 802.1: bridging end management.
- 802.2: LLC (Logic Link Control), definito anche "sottolivello LLC", esso si occupa di gestire la comunicazione end-to-end tra l'host corrente e l'host successivo. In pratica stabilisce come la PDU del livello datalink, chiamata frame, debba essere trasmessa nel mezzo trasmissivo (sia esso guided, o unguided).
- 802.3: CSMA/CD (Carrier Sense Multiple Access / Collision Detection) stabilisce il modo in cui è possibile accedere al mezzo trasmissivo, riconoscendo situazioni in cui è avvenuto un accesso simultaneo al mezzo e, di fatto, è stata causata una collisione. La topologia a cui si riferisce è la topologia a bus.
- 802.4: TPBAM (Token-Passing Bus Access Method) stabilisce il modo in cui si effettua l'accesso al mezzo trasmissivo in una rete a bus (,a che concettualmente può essere vista come una rete ad anello), in cui ciascun host può trasmettere solo se possiede un particolare elemento detto token. In pratica questo standard "atrae" la topologia a bus in modo da avere, concettualmente, una topologia token ring.
- 802.5: TRAM (Token Ring Access Method), invece, definisce il modo in cui in una rete di tipo token ring, ciascun host può accedere al mezzo trasmissivo.
- 802.6: DQDB (Distribuited Queue Dual Bus) che, anche se oramai in disuso in quanto ideato ed utilizzato agli inizi degli anni '90, definisce il modo in cui si inviano dei dati nelle reti MAN.
- 802.7: broadband per le reti LAN, ormai in disuso e non trattato.
- 802.8: fibra ottica per le reti LAN e MAN. Tratta anche le reti FDDI (Fiber Distributed Data Interface), ovvero un particolare tipo di rete LAN in cui la fibra ottica può raggiungere velocità massime di 100 Mbps. Si tratta di uno standard superato, quindi non trattato qui.
- 802.9: detto anche "isoEthernet", definisce le reti LAN che utilizzano Ethernet basati sull'assegnazione di quantità fisse di banda. Ethernet, in pratica, sarebbe l'utilizzo di CSMA/CD con il doppino telefonico, anche se oggigiorno si presenta in numerose varianti.
- 802.10: definisce gli standard di sicurezza per le reti LAN e WAN.
- 802.11: Wireless LAN, ovvero il conosciutissimo Wi-Fi, una rete wireless (senza guided media) che consente a più host di comunicare tra loro attraverso l'uso di onde elettromagnetiche.
- 802.12: standard che definisce le reti 100VG-AnyLAN, ovvero LAN che possono raggiungere velocità di trasmissione dati di 100 Mbps. La particolarità di questo standard è il modo in cui gli host della rete trasmettono: secondo un accesso al canale basato su richiesta (Demand Priority).
- 802.15: per le reti PAN wireless. In pratica questo standard definisce il Bluetooth, utilizzato ad esempio quando si collegano gli auricolari al proprio cellulare.
- 802.16: per le reti LAN broadband di tipo wireless (dette anche Broadband Wi-Fi).
- 802.17: per le reti RPR (Resilient Packet Ring), non analizzate qui.
- 802.18: Radio Regulatory.
- 802.19: che definisce il comportamento di reti wireless differenti e sovrapposte. In pratica, il titolo di questo standard è appunto "coexistence" e si riferisce alla coesistenza di più reti wireless nella stessa aree che utilizzano bande sovrapposte, o parzialmente sovrapposte per la trasmissione dei dati.
- 802.20: per le reti mobile di tipo broadband.

##### 03.01.02. Responsabilità e servizi forniti dal datalink layer

Il Data Link Layer (livello di collegamento dati) ha il compito di garantire una comunicazione affidabile tra due nodi direttamente connessi attraverso lo stesso mezzo trasmissivo. Esso riceve i dati dal Network Layer, li organizza in frame e li trasmette sul canale fisico.

Le principali responsabilità del Data Link Layer sono:

- Framing: suddivisione dei dati provenienti dal livello superiore in frame, aggiungendo intestazioni e informazioni di controllo.
- Indirizzamento fisico: utilizzo degli indirizzi MAC per identificare il mittente e il destinatario all'interno della stessa rete locale.
- Rilevamento degli errori: individuazione di eventuali errori introdotti durante la trasmissione mediante tecniche come il CRC (Cyclic Redundancy Check).
- Controllo degli errori: gestione delle ritrasmissioni e delle conferme di ricezione nei protocolli che lo prevedono.
- Controllo di flusso: regolazione della velocità di trasmissione per evitare che il ricevente venga sovraccaricato.
- Controllo dell'accesso al mezzo (MAC): coordinamento dell'utilizzo del mezzo trasmissivo condiviso da più dispositivi.

Tra i principali servizi forniti dal Data Link Layer vi sono la consegna affidabile dei frame tra nodi adiacenti, il controllo degli errori e la gestione dell'accesso al canale di comunicazione.

##### 03.01.03. Tipi di collegamenti: end-to-end e broadcast

Quando si parla del livello datalink, normalmente si ha ache fare con due tipi di collegamenti:

- Un collegamento end-to-end si ha quando un host è collegato attraverso un mezzo trasmissivo (come fibra ottica atmosfera terrestre, o doppino telefonico) a un altro host in modo diretto. Il collegamento end-to-end realizza ciò che comunemente viene denominata comunicazione unicast: un host invia un messaggio solo ed esclusivamente a un altro host, l'unico destinatario della comunicazione. La seguente figura mostra questa semplice situazione:

<!-- to add -->
*In Figura: due host A e B collegati in modo diretto attraverso un mezzo trasmissivo*

- Un collegamento broadcast si ha quando più di due host sono collegati tra loro dallo stesso mezzo trasmissivo. In pratica, l'invio di un segnale da parte di un qualsiasi host collegato coinvolge tutti gli altri host. In pratica la comunicazione broadcast prevede che un host invii un messaggio a tutti gli altri host della rete. Questa situazione è rappresentata nella seguente figura, in cui si ha una topologia a bus che collega cinque host:

<!-- to add -->
*In Figura: cinque host collegati secondo una topologia a bus attraverso un mezzo trasmissivo*

Esempi di reti broadcast sono le reti Wi-Fi, le reti radio e le reti Ethernet tradizionali. Esempi di reti end-to-end sono le reti ad hoc (due computer collegati in modo diretto, o un computer collegato via cavo ad una stampate), o le reti Bluetooth (ad esempio quando si collegano degli auricolari ad uno smartphone per ascoltare della musica).

##### 03.01.04. Introduzione ai sottolivelli LLC (Logical Link Control) e MAC (Media Access Control)

Nello standard IEEE 802 il datalink Layer è suddiviso in due sottolivelli: LLC (Logical Link Control) e MAC (Media Access Control). Questa suddivisione consente di separare le funzioni di controllo logico della comunicazione da quelle legate all'accesso al mezzo trasmissivo.

Il sottolivello LLC costituisce l'interfaccia tra il datalink layer e il network layer dello stack TCP/IP ed i servizi forniti al livello superiore sono:

- identificazione del protocollo di livello superiore;
- controllo degli errori (quando previsto, a seconda del tipo di comunicazione utilizzata dagli host);
- controllo di flusso;
- rendere indipendente il mezzo trasmissivo al livello network.

Il sottolivello MAC si occupa della gestione dell'accesso al mezzo trasmissivo da parte degli host e delle operazioni direttamente correlate alla trasmissione dei frame. Esso fornisce i seguenti servizi:

- gestione degli indirizzi MAC;
- controllo dell'accesso al mezzo condiviso;
- delimitazione e trasmissione dei frame;
- rilevamento degli errori tramite CRC;
- gestione delle collisioni nelle reti che le prevedono.

In sintesi, il sottolivello LLC fornisce i servizi logici ai livelli superiori, mentre il sottolivello MAC gestisce l'accesso fisico al mezzo di trasmissione e l'invio dei frame sulla rete. La seguente figura mostra come sono relazionati i sottolivelli LLC e MAC:

<!-- to add -->
*In Figura: come sono relazionati i sottolivelli LLC e MAC*

### 03.02. Servizi di connessione 

Il livello datalink fornisce vari servizi di connessione di tipo punto-a-punto, o point-to-point. in pratica sono tre i principali servizi di connessione utilizzati per trasferire i bit dall'host corrente a quello successivo. Ricordiamoci che una connessione punto-a-punto coinvolge solo due host, come rappresentato nella seguente figura:

<!-- to add -->
*In Figura: la connessione punto-a-punto tra due host A e B, collegati tramite un mezzo trasmissivo*

I principali servizi di connessione sono:

- Servizio connectionless senza ACK (unacknowledge connectionless service): non è necessario creareuna connessione prima di inviare i dati dal mittente al destinatario. Il termine connectionless si riferisce esattamente all'assenza di handshake tra i due host prima di iniziare a comunicare. Il destinatario non invia alcun tipo di conferma di ricezione, detta ACK (da ACKnowledge). In pratica si tratta del servizio più semplice possibile, senza alcuna forma di controllo del flusso: i dati vengono semplicemente analizzati e spediti dal mittente e, attraverso il mezzo trasmissivo, giungono a destinazione. Se il protocollo del livello datalink lo prevede, si ha una semplice forma di controllo degli errori (come i codici CRC, o LDPC -Low Density Parity Check-).
- Servizio connection-oriented con ACK (acknowledge connection-oriented service): i servizi orientati alla connessione sono molto più complessi ed inizia già ad esserci una vera e propria forma di controllo del flusso di dati. Anzitutto, prima di indivare i dati dal mittente al destinatario, quest'ultimo deve inviare un messaggio di richiesta di apertura della connessione ed il destinatario deve rispondere in modo affermativo, o negativo a seconda che possa effettivamente gestire la comunicazione. Successivamente, se il destinatario risponde affermativamente, allora il mittente può iniziare a spedire i dati. A seconda del protocollo scelto e della velocità di ricezione del destinatario, il flusso dati può rallentare, o velocizzare; inoltre, il destinatario invia una conferma di ricezione, detta ACK, per ogni messaggio (oppure ogni N messaggi). Si tratta di un servizio affidabile e ben controllato, ma anche più lento e che consuma più risorse sia lato mittente, sia lato destinatario.
- Servizio connectionless con ACK (acknowledge connectionless service): in pratica è un ibrido tra i due servizi descritti in precedenza. I protocolli del livello datalink che rientrano in questa categoria non prevedono handshake e primitive di apertura/chiusura di una connessione tra la coppia di host, bensì prevedono solo primitive di trasferimento dati e ACK: l'unica forma di controllo è l'ACK inviato dal destinatario (che può essere uno per ogni messaggio, oppure uno ogni N messaggi). Si tratta di un servizio con pochi fronzoli, che consuma un modesto numero di risorse, ma che allo stesso tempo non raggiunge una elevata affidabilità. Normalmente si opta per i primi due servizi: o si utilizza un protocollo connectionless, o un protocollo connection-oriented, anche se ciò dipende fortemente dalla rete e dalla tipologia di mezzo trasmissivo e di host. 

### 03.03. Frame

La struttura della PDU del livello datalink, chiamato frame, dipende dal tipo di protocollo scelto. La struttura generale di una PDU (e questo vale per tutti i livelli dello stack) è costituita da tre elementi principali:

<!-- to add -->
*In Figura: la struttura base di una PDU*

In pratica la struttura di base di una PDU prevede tre elementi:

- Header: in cui sono presenti i campi che descrivono con esattezza in che cosa consiste il protocollo utilizzato, come devono comunicare gli host, quali host sono coinvolti nella comunicazione e altre informazioni importanti. Dipende molto dal protocollo scelto.
- Payload: si tratta dei dati veri e propri (o di un PDU di un livello superiore incapsulata). Questi sono estratti dal livello superiore quando il controllo passa ad esso.
- Trailer: detta anche "coda" della PDU, essa contiene i codici di correzione, o rilevamento degli errori.

Come vedremo adesso e nei successivi capitoli, tutti i layer dello stack TCP/IP sono fortemente basati su questo tipo di struttura.

Partiamo dal frame più semplice: il frame LLC (Logic-Link Control), ovvero il frame più semplice trattato dal livello datalink, composto dalle seguenti sezioni:

- Header LLC: header costruito ed inserito nella PDU dal sottolivello LLC del datalink layer dello stack TCP/IP. La sua struttura dipende molto dal tipo di protocollo utilizzato.
- DSAP (Destination Service Access Point) - 1 Byte: identificativo del protocollo utilizzato dal livello superiore, ovvero il livello network.
- SSAP (Source Service Access Point) - 1 Byte: identificativo del protocollo utilizzato dal livello datalink, tra i due host posti in comunicazione (essi si dicono anche peer entity).
- Control - 2 Byte: utilizzato per scoprire il tipo di frame (se ha contenuto informativo, di controllo, o altro) e per il controllo del flusso di dati tra i due host. Normalmente il campo control distingue tra i seguenti tipi di frame: I-Frame (contengono dati), S-Frame (contengono informazioni di controllo) e U-Frame (senza alcun numero identificativo, essi sono usati per operazioni di controllo del flusso).
- Network PDU: la PDU del livello network dello stack TCP/IP, che tratteremo a dovere nel successivo capitolo.

La PDU LLC è mostrata di seguito:

<!-- to add -->
*In Figura: PDU del sottolivello LLC dello stack TCP/IP*

Più in basso del sottolivello LLC c'è il sottolivello MAC (Media Access Control) del livello datalink. Il frame LLC viene incapsulato all'interno di un frame più grande, detto frame MAC, la cui struttura di base prevede i seguenti campi:

- Header MAC: header costruito ed inserito nella PDU dal sottolivello MAC del datalink layer dello stack TCP/IP. La sua struttura dipende molto dal tipo di protocollo utilizzato.
- DSAP (Destination Service Access Point) - 6 Byte: indirizzo MAC della scheda di rete del dispositivo destinatario.
- SSAP (Source Service Access Point) - 6 Byte: indirizzo MAC della scheda di rete del dispositivio mittente.
- Frame LLC: il frame LLC (analizzato in precedenza) incapsulato all'interno del frame MAC.
- FCS (Frame Check Sequence) - 4 Byte: bit di controllo per l'intero frame, solitamente un CRC, o dei codici di parità (come LDPC).

La seguente figura mostra la struttura del frame MAC:

<!-- to add -->
*In Figura: struttura del frame MAC*

In realtà il frame MAC subisce un'ulteriore modifica prima di passare al livello physicial ed essere trasmesso, bit per bit, nel mezzo trasmissivo. All'inizio viene aggiunto un gruppo di bit (di numero variabile e strettamente dipendente dal mezzo trasmissivo utilizzato) che prende il nome di clock syn: si tratta di un gruppo di bit usato per la sincronizzazione tra i due host mittente e destinatario. Inoltre, esso indica l'inizio di un frame, per cui il frame non può contenere (al suo interno) un altro gruppo di bit uguale a quello presente dentro al clock syn. Un altro campo viene aggiunto alla fine del frame, che prende il nome di frame delimiter: quest'ultimo rappresenta la fine del frame, ovvero un gruppo di bit che identifica anche quando il frame successivo inizia. Come il clock syn, anche il frame delimiter è un gruppo di bit univoco, nel senso che non viene mai ripetuto all'interno del frame stesso. Questo nuovo frame è pronto per essere trasmesso direttamente sul mezzo trasmissivo ed è mostrato di seguito:

<!-- to add -->
*In Figura: frame con CLOCK SYN all'inizio e FRAME DELIMITER alla fine*

##### 03.03.01 Indirizzi MAC

Particolare attenzione la meritano gli indirizzi MAC. Ciascun host della rete che abbia la capacità di collegarsi ad Internet è dotato di particolare hardware che prende il nome di NIC (Network Interface Card, o scheda di rete): questa dispone di tutti gli strumenti per inviare e ricevere segnali e consentire al calcolatore di partecipare a Internet. Ciascuna NIC ha un indirizzo ben preciso e univoco a livello mondiale (teoricamente, nella pratica è sempre tutto più difficile) che prende il nome di indirizzo MAC (Media Access Control). Un indirizzo MAC ha una lunghezza di 48 bit ed è solitamente rappresentato da 12 cifre esadecimale (una singola cifra esadecimale può rappresentare ben quattro bit), specificate in gruppi di due cifre e separate per mezzo del trattino medio (-). Ecco un esempio di indirizzo MAC:

```
08-00-2B-C4-BE-F3
```

Negli indirizzi MAC, solitamente tutte le lettere esadecimali sono scritte con un case maiuscolo. Ogni coppia di cifre esadecimale rapprsenta 8 bit: si hanno quindi 6 gruppi da 8 bit, per un totale di 48 bit. L'indirizzo MAC rappresenta un identificativo di dispositivo a livello di rete locale, LAN: in pratica non potrebbe teoricamente mai esistere una situazione in cui due dispositivi appartenenti alla stessa rete locale abbiano lo stesso indirizzo MAC.

I primi 3 gruppi di cifre esadecimali, ovvero i primi 24 bit dell'indirizzo MAC, identificano il cosiddetto OUI (Organization Unique Identifier): ciascun produttore di schede di rete produce sempre schede che hanno i primi 24 bit come indirizzo MAC uguale. I successivi 3 gruppi di cifre esadecimali, ossia la restante metà dell'indirizzo MAC, rappresenta la specificità della scheda NIC.

Gli indirizzi MAC sono utilizzati solo ed esclusivamente dal livello datalink detto stack TCP/IP: il livello network sfrutta una altro tipo di indirizzi, detti indirizzi IP, che esamineremo dettagliatamente nel successivo capitolo. Gli indirizzi MAC possono essere di tre tipi:

- MAC unicast: inividua in modo diretto una stazione singola, come l'esempio precedente.
- MAC multicast: MAC destinati a un certo gruppo di bit all'interno della rete. In questo caso i primi tre gruppi di bit sono tutti a 1, mentre il quarto gruppo è costituito dalla prima cifra esadecimale che può andare da 0 a F, mentre le successive cifre possono assumere un qualsiasi valore. La rappresentazione formale è qualcosa di simile alla seguente: FF-FF-FF-[0:F]X-XX-XX, dove X indica che può esserci un qualsiasi valore esadecimale.
- MAC broadcast: in cui tutti i bit dell'indirizzo MAC sono posti a 1 (FF-FF-FF-FF-FF-FF). Questo indirizzo consente di inviare un messaggio a tutti gli host della rete ed è tipico quando si vuole scoprire l'identità degli altri host (per ottenere e conoscere il loro indirizzo MAC).

##### 03.03.02. Tecniche di framing

Il framing è una tecnica utilizzato nel livello datalink in modo da permettere al ricevitore di distinguere l'invio di un frame da un altro. In pratica le tecniche di framing cercano di fornire un modo intelligente e rapido per permettere al destinatario di ricevere più frame. In realtà questo tipo di tecniche nasce anche per un motivo ben preciso: dare la possibilità agli host della rete di inviare frame di lunghezza variabile (variable-length frame), senza vincolare la lunghezza di ciascun frame ed aggiungere del padding "temporaneo" (e del tutto immotivato). I frame di lunghezza fissa (fixed-length frame), infatti, per quanto possano funzionare bene in termini di sincornizzaizone e di invio, sono soggetti a padding: se il payload non ha abbastanza dati, si aggiunge del padding alla fine di esso, in modo da raggiungere la lunghezza prefissata. Aggiungere padding è relativamente costoso (in quanto sia il mittente, sia il destinatario devono essere a conoscenza di quale padding è stato aggiunto ed in che modo). Inoltre, i frame di lunghezza variabile si sposano relativamente bene con certi protocolli di rete.

La principali tecniche di framing sono le seguenti:

- Byte count, o character count: si inserisce un campo length di un certo numero di Byte all'interno dell'header del frame MAC che indica la lunghezza, in Byte, del frame stesso. Quando il destinatario riceve il frame, viene a conoscenza del campo length e sa in anticipo di quanti Byte è costituito il frame corrente.
- Byte stuffing: si utilizzano caratteri speciali per indicare sia l'inizio del frame, sia la fine del frame. La difficoltà di questa tecnica consiste nell'evitare che i gruppi di bit usati per l'inzio e per la fine del frame vengano ripetuti all'interno del payload, o del resto del frame (pena un disastro in fase di ricezione). I caratteri possono essere composti da uno, o più Byte (per questo tale tecnica si chiama "Byte" stuffind). Uno svantaggio di questa tecnica è che entrambi gli host defono sfruttrare la stessa codifica di caratteri, per esempio ASCII, o Unicode UTF-8. I caratteri più utilizzati per indicare l'inizio e la fine del frame sono, rispettivamente, FLAG ed ESC.
- Bit stuffing: il frame inizia e termina con una sequenza speciale di bit, che fungono da veri e propri marker di inizio e di fine del frame. Per evitare che questa sequenza compaia nei dati, il mittente inserisce automaticamente uno 0 dopo ogni sequenza di cinque 1 consecutivi: questo comporta che l'intero frame venga analizzato in fase di invio, anche se questa operazione può essere facilmente eseguita via hardware. Un marker tipico di inizio/fine frame è il seguente gruppo di 8 bit: 01111110 (uno zero, seguito da 6 bit impostati a 1, seguito infie da un altro 0). Si tratta di 2 Byte in più: 1 Byte posizionato all'inizio, uno posizionato alla fine.
- Violazione del codice fisico: alcuni schemi di codifica del livello fisico prevedono simboli, o combinazioni di bit che normalmente non possono apparire nei dati. Essi vengono riutilizzati per aggiungere dei marker di inizio e fine del frame, avendo la sicurezza che essi non potranno comparire all'interno del payload del frame (a meno ché non capiti un errore: in tal caso sarebbe necessaria una gestione apposita).

### 03.04. Controllo degli errori

Il datalink layer si occupa del controllo degli errori. In moltissime architettura basate sul layered model, come l'architettura delle reti di calcolatori oggigiorno usata da Internet (ovvero TCP/IP), è particolarmente importante rendere affidabile e sicuro lo scambio di informazioni sia tra due host collegati direttamente, sia tra due host collegati per mezzo di uno, o più switch, router, o altri dispositivi intermedi. Il controllo degli errori, come vedremo, viene attuato da più livelli dello stack TCP/IP, in particolare i livelli datalink e transport. In questo contersto parlaremo del controllo degli errori a basso livello, ossia quello che si ha quando un host invia un frame in uscita su un determinato collegamento. Il controllo degli errori viene attuato sia lato mittente, sia lato destinatario:

- Il mittente prepara appositi gruppi di bit ridondanti, detti anche redundant bits.
- Il destinatario, venendo a conoscenza di quale protocollo di controllo degli errori ha utilizzato il mittente, effettua un controllo sui redundant bits per comprendere se, durante la trasmissione dei dati, sia avvenuto qualche errore, oppure no.

Gli errori possono avvenire in due modalità (ed entrambi sono possibili nell'ambito di una comunicazione dati in Internet):

- Errori singoli: data una lunga sequenza di bit, si ha un errore isolato che coinvolge solo uno, o pochissimi bit isolati l'uno dall'altro.
- Errori multipli (o burst errors): si ha quando l'errore interessa un gruppo più ampio di bit consecutivi, per esempio interessando più Byte della PDU.

In entrambi i casi, il controllo degli errori attuato dal datalink layer nasce proprio per identificare gli errori e, s'é possibiel e s'é previsto dal codice di controllo degli errori, correggerlo lato ricevente (anche se non sempre questa operazione è possibile).

Quali sono le cause principali degli errori nei canali di comunicazione? Sono molteplici, ma ecco riassunte le più comuni:

- Rumore termico: generato dal movimento casuale degli elettroni nei circuiti elettronici e nei mezzi trasmissivi.
- Interferenze elettromagnetiche (EMI): causate da dispositivi elettrici, motori, linee di alimentazione o altri sistemi di comunicazione che operano nelle vicinanze.
- Attenuazione del segnale: diminuzione della potenza del segnale durante la propagazione, che rende più difficile distinguere correttamente i dati trasmessi.
- Distorsione: alterazione della forma del segnale dovuta alle caratteristiche non ideali del canale di trasmissione.
- Interferenza tra simboli (ISI - Inter Symbol Interference): sovrapposizione di simboli consecutivi causata dalla dispersione del segnale nel canale.
- Multipath propagation: ricezione dello stesso segnale attraverso percorsi differenti, che può generare ritardi, attenuazioni e cancellazioni del segnale.
- Diafonia (Crosstalk): interferenza prodotta da segnali che viaggiano su canali fisicamente vicini.
- Errori dovuti a ostacoli e condizioni ambientali: fenomeni atmosferici, ostacoli fisici, pioggia, nebbia o edifici possono degradare la qualità del segnale, soprattutto nelle comunicazioni wireless.
- Congestione della rete: in alcune tecnologie può provocare perdita di pacchetti e ritrasmissioni, aumentando la probabilità di errori nella comunicazione.

Tali fenomeni possono alterare uno o più bit durante la trasmissione, rendendo necessario l'impiego di tecniche di rilevamento e correzione degli errori per garantire l'affidabilità delle comunicazioni.

I codici di controllo degli errori, detti anche ECs (Error Codes) si suddividono in due categorie principali:

- EDCs (Error Detection Codes): codici di controllo degli errori che rilevano solo se c'è stato un errore singolo, o un errore multiplo.
- ECCs (Error Correction Codes): codici di controllo degli errori che non solo rilevano la presenza di uno, o più errori, ma cercano anche di correggerli.

In seguito esamineremo entrambi i tipi di ECs.

##### 03.04.02. EDCs (Error Detection Codes)

Analizzere i codici di rilevamento degli errori in modo progressivo, dal più semplice al più complesso. Il parity code (codice di parità) consiste di una stringa di un certo numero di bit a cui viene aggiunto un bit di parità, detto anche parity bit (o anche bit ridondante, o redundant bit). Ci sono due modi per decidere il valore che deve assumere il parity bit:

- Parità pari: il numero totale di 1 nella stringa di bit deve essere pari, per cui il parity bit diventa 1 solo se nella stringa originale di bit è presente un numero dispari di 1.
- Parità dispari: il numero totale di 1 nella stringa di bit deve essere dispari, per cui il parity bit diventa 1 solo se nella stringa originale di bit è presente un numero pari di 1.

Per esempio, se scegliamo di utilizzare la parità pari e la stringa di dati di 8 bit è: 11110010 (con 5 bit impostati al valore 1 ed i rimanenti al valore 0), allora il bit di parità da aggiungere dovrà essere 1, ottenendo la stringa di 8 + 1 bit (9 bit), ovvero: 111100101. Che succede in caso di errore? Essendo un codice di rilevamento degli errori, il parity bit singolo non riesce a correggerli, tuttavia è in grado di accorgersi dei seguenti casi (si consideri la parità pari):

- Se un bit dovesse subire un errore (ad esempio viene cambiato in 1, ma vale anche il viceversa), il parity bit se ne accorgerebbe.
- Se due bit dovessero subire un errore (ad esempio un bit cambia da 0 a 1, mentre un altro cambia da 1 a 0), il parity bit non se ne accorgerebbe, in quanto il numero totale di 1 è sempre pari.
- Se tre bit dovessero subire un errore (ad esempio due bit passano da 0 a 1 e un bit da 1 a 0), il parity bit se ne accorgerebbe, in quanto il numero totale di 1 diventerebbe dispari.

In pratica il parity bit singolo è in grado di accorgersi di un numero di errori dispari, ma non pari, aspetto che lo rende talvolta poco efficace.

La naturale evoluzione del parity bit singolo è il parity bit multiplo, in cui più bit di parità vengono aggiunti alla stringa originale di N bit, diciamo ogni M bit, ove M è solitamente detto gruppo di parità. Per esempio, se si ha una stringa di 12 bit di dati, si potrebbe pensare di aggiungere un bit di parità ogni 4 bit di dati, ottenendo una stringa di 15 bit. Eccola:

```
bbbbr bbbbr bbbbr
```

dove `b` indica un bit dati, mentre `r` indica un bit ridondante (bit di parità). Ciascun bit di parità effettua il rilevamento degli errori solo ed esclusivamente all'interno del proprio gruppo di bit. Scegliendo la parità pari, per esempio, e avendo a disposizione i bit di dati 1111 0010 1101, la stringa completa diventa:

```
11110 00101 11011
```

Il primo bit di parità è 0, in quanto il gruppo 1111 contiene quattro 1; il secondo bit di parità è 1, in quanto il gruppo di bit 0010 contiene un solo uno; infine, il gruppo 1101 contiene tre uno, per cui il bit di parità diventa 1. I parity bit multipli possono rilevare sia errori dispari, sia errori pari: in quest'ultimo caso, però, in due (o più gruppi) deve avvenire lo stesso numero di errori. Un numero pari di errori che si verificano all'interno dello stesso gruppo, scegliendo la parità pari, non è rilevabile.

Ora esamineremo un codice di rilevamento degli errori molto interessante. Si tratta di un codice di rilevamento di tipo bidimensionale, utilizzato sia nell'ambito della trasmissione dati, sia nell'ambito della memorizzazione e/o archiviazione di grandi quantità di dati su una memoria secondaria, o terziaria, come un HD (Hard Drive), o una SSD (Solid State Drive). In sostanza, i bit di dati vengono organizzati in una matrice di N righe e di M colonne. Si aggiungono N bit di parità (uno per ciascuna riga) ed M bit di parità (uno per ciascuna colonna), ovvero si hanno in totale N + M bit di parità. La parità nel 2D parity check (2 dimensional parity check) si calcola nel seguente modo:

1. Si sceglie quale parità utilizzare (se dispari, o pari). Per esempio la parità pari.
2. Per ciascuna riga si calcola il valore del bit di parità, ovvero si effettua un VRC (Vertical Redundancy Check). Per esempio, se la riga è costituita da un numero pari di 1, il bit di parità deve essere 0; differentemente, se la riga è costituita da un numero dispari di 1, il bit di parità deve essere 1.
3. Per ciascuna colonna si calcola il valore del bit di parità, ovvero si effettua un LRC (Longitudinal Redundancy Check). Se la colonna ha un numero pari di 1, il bit di parità da aggiungere deve assumere il valore 0; se ha un numero dispari di 1, deve avere il valore 1.
4. Si aggiunge il bit di parità delle righe, calcolato considerando i bit di parità delle righe (capiremo meglio a breve).

Ma facciamo un esempio molto semplice. Immaginiamo di avere 18 bit di dati, organizzati in 3 righe di 6 bit (normalmente vengono utilizzati valori corrisopondenti alle potenze del 2, ma ciò funziona ugualmente anche con valori differenti):

```
1 1 0 0 1 0
0 1 1 1 0 0
1 0 0 1 1 1
```

Aggiungiamo i bit di parità, sempre tenendo la nostra struttura a matrice:

```
      c0  c1  c2  c3  c4  c5
----------------------------
r0  | 1 | 1 | 0 | 0 | 1 | 0
r1  | 0 | 1 | 1 | 1 | 0 | 0
r2  | 1 | 0 | 0 | 1 | 1 | 1
```

I bit di parità delle righe sono `r0`, `r1` e `r2`, ovvero 3. I bit di parità delle colonne vanno da `c0` a `c5` e sono 6 in totale. Scegliendo la parità pari, possiamo calcolare il valore di ciascun bit nel seguente modo:

```
     0   0   1   0   0   1
----------------------------
1  | 1 | 1 | 0 | 0 | 1 | 0
1  | 0 | 1 | 1 | 1 | 0 | 0
0  | 1 | 0 | 0 | 1 | 1 | 1
```

Ora calcoliamo il parity bit delle rige, ovvero aggiungiamo un bit di parità in alto a sinistra che considera solo i bit di parità di ogni riga:

```
0  | 0   0   1   0   0   1
----------------------------
1  | 1 | 1 | 0 | 0 | 1 | 0
1  | 0 | 1 | 1 | 1 | 0 | 0
0  | 1 | 0 | 0 | 1 | 1 | 1
```

Bene, a questo punto i dati si possono trasmettere sul canale. Il ricevente, una volta ricevuti tutti i dati, ricalcola i bit di parità e, poiché si tratta di un codice di rilevamento degli errori con struttura a matrice, il ricevente è in grado di scoprire errori multipli a seconda dei bit di parità che differiscono. Si tratta di un codice dispendioso dal punto di vista computazionale, anche se oggigiorno esiste dell'hardware apposito che realizza tutte queste funzionalità.

Il CRC (Cyclic Redundancy Check) è una tecnica matematica utilizzata per rilevare errori nei dati durante la trasmissione, o la memorizzazione di dati. Funziona calcolando un codice univoco (detto resto, o remainder) basato su un polinomio generatore e aggiungendolo al messaggio originale. La tecnica CRC è molto affidabile (considerata tra le più affidabili presenti oggi), ma necessita di una standardizzazione apposita. Inoltre è dispendiosa a livello di calcolo (in quanto si effettuano divisioni e si calcolano resti, operazioni normalmente svolte in più cicli di clock). Ma andiamo dritti al nocciolo della questione. Nei CRC si utilizza quella che normalmente viene denominata rappresentazione polinomiale di una stringa di bit, in cui tutti i bit di un messaggio sono considerati come dei veri e propri coefficienti di un polinomio di un certo grado. Ad esempio, la sequenza binaria 1011 corrisponde al seguente polinomio:

$$
(1 \cdot x^3 + 0 \cdot x^2 + 1 \cdot x^1 + 1 \cdot x^0 = x^3 + x + 1)
$$

La posizione di ciascuna cifra indica l'esponente al quale deve essere elevata la variabile $x$ del polinomio stesso. Il processo di generazione di un codice CRC è il seguente:

1. Si sceglie anzitutto un polinomio generatore, detto $G(x)$. La standardizzazione dei codici CRC permette di scegliere tra diversi polinomi generatori che, dal punto di vista matematico, hanno caratteristiche particolari e molto interessanti (ma non le tratteremo qui).
2. Dato il messaggio di m bit di dati, ad esso si aggiungono tanti 0 quanto è il grado del polinomio generatore, solitamente indicato con $G(x)$. Per esempio, se si utilizza un polinomio generatore il cui grado è $13$, allora si aggiungono $13$ bit ridondanti al messaggio, ottenendo una stringa di m + r bit. Inizialmente, tutti questi bit sono posti a 0. Nell'ambito dei CRC si dice spesso che il messaggio costituito dai soli m bit è un polinomio $M(x)$, mentre gli r bit ridondanti sono un polinomio detto $R(x)$. Ma questa è pura nomenclatura.
3. Il messaggio "esteso" di m + r bit viene diviso sfruttando l'aritmetica in modulo due per il polinomio generatore scelto, $G(x)$. Possiamo indicare il messaggio esteso come un terzo polinomio, $N(x)$. In pratica si effettua la divisone in modulo 2: $N(x) / G(x)$.
4. Si calcola il resto (remainder) della divisione $N(x) / G(x)$, ovvero il codice CRC vero e proprio, lungo esattamente r bit. In pratica esiste una proprietà matematica che afferma quanto segue: dato il grado r di un certo polinomio $G(x)$, se si divide un qualsiasi altro polinomio per $G(x)$, esso genererà sempre un resto di al massimo r cifre. Queste r cifre sono il codice di ridondanza ciclica, ovvero il CRC.
5. Il mittente invia il messaggio originale, a cui accoda il CRC calcolato al punto precedente.
6. Il ricevitore, una volta ricevuti dati e CRC, effettua la stessa divisione sull'intero pacchetto ricevuto. Se il resto è zero, non ci sono errori.

Ora parliamo del codice di rilevamento degli errori più utilizzato nel mondo delle reti di calcolatori: insieme al CRC analizzato precedenemente, il checksum è un codice considerato tra i più efficienti ed affidabili presenti oggigiorno e viene realmente usato nella comunicazione via Internet, sia dai livelli inferiori dello stack TCP/IP (come il livello datalink), sia da quelli superiori. Il metodo checksam sfrutta un generatore di bit (checksum generator) lato mittente della comunicazione, mentre sfrutta un controllore dei bit generati (checksum checker) lato destinatario della comunicazione. Una checksum non è altro che un gruppo di bit generato a partire dai bit da inviare nel mezzo trasmissivo considerato univoco ed usato per verificare l'integrità dei dati stessi. In pratica, dati N bit di dati (con N anche molto grande), si produce un insieme di M bit di checksum, dove solitamente M è di 8, 16, 32, o 64 bit (esistono checksum anche di lunghezza maggiore). Se la checksum calcolata lato ricevente combacia con la checksum calcolata e inviata dal mittente, allora i dati sono giunti a destinazione senza erore. Questo metodo è schematizzato nella seguente figura:

<!-- to add -->
*In Figura: il modo in cui funziona la checksum*

Lato mittente, i bit di dati vengono suddivisi in segmenti lunghi solitamente 16 bit. Sfruttando l'aritmetica in complemento a 1, tutti i segmenti dei dati vengono sommati. Infine, si effettua il complemento a uno del risultato ottenuto, ovvero la checksum. Questo processo è descritto nella precedente figura utilizzando blocchi, somme e frecce: sebbene per grandi quantità di dati possa sembrare un processo dispendioso, in realtà qualsiasi calcolatore moderno dispone di hardware apposito in grado di eseguire somme (specie se di pochi bit, come 16 bit) in modo diretto, in un singolo ciclo di clock. Nel canale viene trasmessa prima la checksum calcolata e, successivamente, i dati originali.

Lato destinatario, una volta ricevuti tutti i bit di dati, essi vengono suddivisi in segmenti di 16 bit ciascuno. Il processo consiste nella somma in complemento a uno di ciascun segmento di dati, esattamente come è stato fatto lato mittente. La differenza rispetto a quanto fatto dal mittente, però, è che il ricevente aggiunge anche la checksum ricevuta al risultato dell'intera somma. Il valore ottenuto da tutte le somme (segmenti di dati e checksum), una volta fatto il suo complemento a uno, deve essere interpretato nel seguente modo:

- Se il valore calcolato è costituito da tutti i bit 0, allora i dati inviati non hanno subito alcun errore.
- Se il valore calcolato è un valore diverso da 0, allora i dati inviati hanno subito uno, o più errori.

Attenzione a una particolarità della checksum: questa non indica alcuna posizione in cui si è verificato l'errore all'interno dei dati, bensì essa rileva solamente se si è verificato un errore.

##### 03.04.03. ECCs (Error Correction Codes)

I codici di correzione degli errori, detti ECCs (Error Correction Codes) sono più difficili da comprendere rispetto ai codici di rilevamento degli errori, in quanto hanno dei meccanismi mediante il quale, fino ad un certo numero di errori, si può ricostruire il messaggio originale. Gli ECCs sono quindi in grado non solo di rilevare gli errori, ma comprendere anche i bit afflitti da errore e, fin a un numero opportuno, correggerli.

Prima di tutto, consideriamo due sequenze di bit aventi la stessa lunghezza $N$, per esempio con $N = 4$:

```
A   1101
B   0001
```

Definiamo distanza di Hamming tra due sequenze di bit $A$ e $B$ aventi la stessa lunghezza $N$, indicandola con $d_h(A, B)$, il numero di bit che differiscono tra le due sequenze. Nell'esempio fatto prima, notiamo come i due bit più significativi di $A$ siano $11$, mentre quelli più significativi di $B$ sono $00$ (il resto dei bit è uguale), per cui si ha:

$$
d_h(A B) = 2
$$

ossia la loro distanza di Hamming è pari a $2$, in quanto due soli bit differiscono tra $A$ e $B$. La distanza di Hamming è fondamentale nell'ambito dello studio e dell'applicazione degli ECCs nelle reti di calcolatori, in quanto essa parmette di scoprire la capacità di un codice di rilevare e correggere un certo numero di errori. In generale:

- Per rilevare fino a un numero $k$ di errori occorre una distanza di Hamming minima di almeno $k + 1$ tra le due sequenze di bit.
- Per correggere fino a $k$ errori è necessario avere una distanza di Hamming minima di almeno $2k + 1$.

Partiamo con uno dei primissimi tra gli ECCs proposti nel corso della storia delle reti di calcolatori. Il codice di Hamming è una tecnica di rilevamento e correzione degli errori che permette di identificare e correggere un errore su un singolo bit in un messaggio trasmesso. Il principio di funzionamento di un codice di Hamming è molto semplice: si aggiungono dei bit di parità in specifiche posizioni all'interno della stringa di bit da trasmettere, in cui ciascun bit di parità (detto anche bit di controllo) calcola la parità di un insieme ben preciso di bit. Facciamo un semplice esempio considerando 4 bit da trasmettere sul canale (nella realtà possono essere molti di più, come 256, 512, 1024, o molti di più). I bit del messaggio vanno da $m_1$ a $m_4$ e sono quattro in totale, mentre i bit di controllo sono tre in totale e vanno da $p_1$ a $p_3$. La parola di codice, detta anche codeword, da trasmettere sul canale è quindi la seguente:

$$
p_1\ p_2\ m_1\ p_3\ m_2\ m_3\ m_4 
$$

In pratica: $p_1$ è il primo bit di parità e deve andare alla posizione $2^0 = 1$. Nell'ambito dei codici di Hamming, la posizione di un certo bit si conta sempre partendo dall'estrema sinistra e procedendo verso destra. Poi abbiamo $p_2$, il secondo bit di parità, che deve andare alla posizione $2^1 = 2$. Poi abbiamo il primo bit del messaggio, $m_1$, che sta nella posizione 3. Successivamente abbiamo il terzo e ultimo bit di parità, $p_3$, che sta nella posizione $2^2 = 4$. La codeword si conclude con i successivi tre bit del messaggio. In pratica i bit di parità stanno nelle posizioni che sono delle potenze di due:

- $2^0 = 1$: primo bit di parità, o $p_1$.
- $2^1 = 2$: secondo bit di parità, o $p_2$.
- $2^2 = 4$: terzo bit di parità, o $p_3$.
- $2^3 = 8$: quarto bit di parità, o $p_4$.
- ...
- $2^N = M$: N-esimo bit di parità, o $p_M$.

Torniamo al nostro esempio di bit da inviare di quattro bit e poniamo che siano: 1011. La precedente codeword diventa:

$$
p_1\ p_2\ 1\ p_3\ 0\ 1\ 1
$$

Ma come vengono calcolati i bit di parità? Ogni bit di parità copre posizioni specifiche in base al codice binario della loro posizione. Utilizziamo una parità pari (il numero totale di bit a 1 nei bit controllati deve essere un numero pari). Ciascun bit di parità copre un ben preciso insieme di posizioni:

- Il bit di controllo $p_1$ controlla i bit nelle posizioni 1, 3 5 e 7, che attualmente è $p_1\ 1\ 0\ 1$. Poiché abbiamo scelto una parità pari, $p_1$ deve essere 0.
- Il bit di controllo $p_2$ controlla i bit nelle posizioni 2, 3 6 e 7, che attualmente è $p_2\ 1\ 1\ 1$. Poiché abbiamo scelto una parità pari, $p_2$ deve essere 1.
- Il bit di controllo $p_3$ controlla i bit nelle posizioni 4, 5 6 e 7, che attualmente è $p_1\ 0\ 1\ 1$. Poiché abbiamo scelto una parità pari, $p_3$ deve essere 0.

La codeword finale da trasmettere sul canale è la seguente:

```
0110011
```

Lato ricevente, se durante la trasmissione il quinto bit subisce un'inversione e il ricevitore ottiene 0110[1]11 (dove il bit tra parentesi quadre è quello errato), il sistema esegue dei test di parità (sindrome) per scoprire l'errore.Ripetendo lo stesso calcolo di parità, il sistema individua quali bit di controllo rilevano un errore. Sommando le posizioni dei bit di controllo errati, si ottiene direttamente l'indice esatto del bit danneggiato. L'algoritmo individua la posizione 5, permettendo al ricevitore di invertire l'1 in 0 e ripristinare il messaggio originale. Questo è il modo principale in cui sono utilizzati i codici di Hamming. Ma ve ne sono molti altri parecchio interessanti, che qui ci limiteremo solo a descrivere. 

FEC (Forward Error Correction) è una tecnica di elaborazione del segnale utilizzata nelle trasmissioni digitali per rilevare e correggere gli errori di trasmissione senza richiedere la ripetizione dei dati. Un pò come i codici di Hamming, il trasmettitore aggiunge dei bit di controllo al messaggio da trasmettere sul canale, mentre il ricevitore ricalcola i bit di controllo e valuta il messaggio per comprendere se si è verificato un errore e dove si è verificato. In pratica, il principio di base dei codici FEC è il seguente: anziché sprecare tempo chiedendo al mittente di inviare nuovamente un pacchetto danneggiato (come accade in tantissimi protocolli del livello transport, giusto per fare un esempio), l'algoritmo FEC trasforma matematicamente i dati stessi. Se una parte del messaggio viene persa, o viene alterata durante il transito per via del rumore, o di un guasto improvviso del canale trasmissivo, il ricevitore applica la formula opposta per ricostruire perfettamente le informazioni originali. In pratica lo schema dei codici FEC è il seguente:

<!-- to add -->
*In Figura: come funziona, in generale, un codice FEC*

I codici FEC sono una famiglia di codici vasta, ma che grossomodo si può classificare in due categorie. I codici FEC includono quindi entrambi i seguenti tipi di codici:

- Codici a blocchi: in cui i dati vengono suddivisi in blocchi della stessa lunghezza e, per ciascun blocco, vengono calcolati i relativi bit di controllo. Il codice Reed-Solomon è l'esempio più celebre, anche se viene utilizzato soprattutto nei supporti di memorizzazione secondaria, come i CD ed i DVD.
- Codici convoluzionali (o continui): in cui si elaborano i dati in modo continuo, basandosi non solo sul messaggio attuale, ma anche su quelli precedenti.

Per quanto i codici FEC richiedano generalmente una banda maggiore, riducono drasticamente un indice della qualità della comunicazione che prende il nome di BER (Bit Error Rate, tasso di errore dei bit).

Ma approfondiamo il codice Reed-Solomon. Quest'ultimo è un codice a blocchi lineare che rientra nella famiglia dei codici FEC. I codici lineari (detti anche codici a blocchi lineari) sono speciali tecniche matematiche utilizzate nelle reti e nelle telecomunicazioni per aggiungere ridondanza ai dati. Questo permette di rivelare e correggere gli errori introdotti da disturbi (rumore) durante la trasmissione dei pacchetti sul canale fisico. Il codice Reed-Solomon:
- è un codice a blocchi in quanto i dati da trasmettere sul canale trasmissivo vengono suddivisi in blocchi di dimensione fissa prima della trasmissione, o della memorizzazione.
- è un codice lineare perché consiste nella somma (o combinazione lineare) di due codeword valide, che genera sempre un'altra parola di codice valida appartenente allo stesso spazio vettoriale.

In sostanza, ciò che fa il codice Reed-Solomon prende un blocco di $k$ simboli informativi e aggiunge $2t$ simboli di ridondanza, creando una parola di codice lunga $n = k + 2t$. Il numero massimo di errori rilevabili e correggibili è pari esattamente a $t$. Attenzione al termine che abbiamo utilizzato: simboli, non bit. Infatti, a differenza di molti altri codici (basati prettamente sui bit), il codice Reed-Solomon non lavora sui singoli bit, ma su insiemi di bit raggruppati in simboli (come interi Byte, composti da 8 bit). Questo lo rende formidabile nel correggere i cosiddetti errori a raffica (burst errors), ovvero pacchetti di dati contigui danneggiati. Il codice Reed-Solomon è anche un codice pasato sulle rappresentazioni polinomiali di un gruppo di bit, che abbiamo già visto (in parte, almeno) per i CRC, analizzati nel precedente paragrafo, ma non la tratteremo in questo contesto.

Adesso passiamo alla seconda categoria dei FEC: i codici convoluzionali. Spiegato in breve, un codice convoluzionale è un tipo di codice per la correzione d'errore nel quale:

- Ogni simbolo d'informazione a m bit (ogni stringa a m bit) da codificare è trasformato in un simbolo a n bit, dove $\frac{m}{n}$ è il rapporto (rate) del codice (con n che è sempre maggiore, o al massimo uguale a m).
- La trasformazione è una funzione degli ultimi k simboli d'informazione, dove k è la lunghezza dei vincoli (constraint length) del codice.

I codici convoluzionali si utilizzano in numerose applicazioni allo scopo di ottenere un trasferimento di dati affidabile, comprese il video digitale, la radio, la telefonia mobile e le comunicazioni via satellite. I codici convoluzionali sono fortemente basati sui registri a scorrimento (shift registers) e sull'operazione logica XOR: lato trasmettitore, man mano che si inseriscono i bit nel buffer di invio, un piccolo circuito (formato da registri a scorrimento e porte logiche XOR) elabora il bit attualmente in fase di trasmissione con un numero preciso di bit precedenti. Questo processo crea gruppi di bit di output maggiori rispetto all'input, rendendo il segnale più robusto. Inoltre, non è necessario rieasaminare più e più volte l'intero messaggio: c'è un supporto hardware diretto per l'implementazione di questa tipologia di codici di errore, per cui non è molto dispendiosa come tecnica dal punto di vista computazionale. Lato ricevente quando i dati arrivano, il ricevitore conosce le regole usate per creare il codice. Uno degli algoritmi più famosi per fare questa operazione è l'algoritmo di Viterbi, che confronta la sequenza ricevuta con tutte le possibili sequenze originali e sceglie quella più logica, ricostruendo eventuali bit corrotti.

<!-- to do - LDPC (Low-Density Parity Check) -->

### 03.05. Controllo del flusso

Il controllo del flusso è l'insieme delle pratiche utilizzate nel datalink layer dello stack TCP/IP per garantire una trasmissione dati efficacie ed efficiente dal punto di vista sia del mittente (trasmissione dati), sia del destinatario (ricezione dati). Il controllo del flusso è un insieme di tecniche che consentono di regolare la velocità di trasmissione dei dati tra mittente e destinatario, evitando che il ricevente venga sovraccaricato da una quantità di dati superiore alla sua capacità di elaborazione, o memorizzazione. Lo scopo principale del controllo del flusso è garantire che il mittente trasmetta dati a una velocità compatibile con quella del ricevente, prevenendo la perdita di informazioni e migliorando l'affidabilità della comunicazione. In assenza di controllo del flusso, un dispositivo molto veloce potrebbe inviare dati più rapidamente di quanto il destinatario sia in grado di processarli (perché magari si tratta di un dispositivo più lento), causando l'esaurimento dei buffer di ricezione e la conseguente perdita di dati.

Tra le principali tecniche di controllo del flusso vi sono:

- Stop-and-Wait: il mittente trasmette un frame e attende la conferma (ACK) prima di inviare il successivo. Si tratta di una famiglia di protocolli molto semplici, ma meno efficienti.
- Sliding Window: il mittente può trasmettere più frame consecutivamente senza attendere un ACK per ciascuno di essi, migliorando l'efficienza della comunicazione. Si tratta di una famiglia di protocolli più complessi, ma anche più efficeinte.

Il problema del mittente veloce e del destinatario lento è particolarmente rilevante quando si parla di controllo di flusso. Se il destinatario è più veloce del mittente, non c'è alcun problema: il mittente spedisce i dati alla propria velocità e, dal momento che il destinatario è più veloce, riesce tranquillamente a ricevere, memorizzare ed elaborare ciascun frame. Ma nella situazione contraria, con un destinatario lento e un mittente veloce, si potrebbe congestionare il collegamento tra i due host, fino anche a saturare la memoria del destinatario: questo è un problema grave che deve essere gestito, altrimenti ne risente l'intera comunicazione, che inizia a subire ritardi sempre più lunghi.

Uno dei principali motivi per cui è necessario il controllo del flusso è il problema del buffering. Ogni dispositivo ricevente dispone infatti di una memoria temporanea, detta buffer, utilizzata per memorizzare i dati ricevuti prima che vengano elaborati dall'applicazione, o dal sistema operativo. Se il mittente trasmette dati a una velocità superiore rispetto a quella con cui il destinatario riesce a elaborarli, i dati si accumulano nel buffer di ricezione. Quando il buffer si riempie completamente (buffer overflow), i nuovi dati in arrivo non possono più essere memorizzati e vengono scartati, causando perdita di informazioni e possibili ritrasmissioni. Il controllo del flusso ha quindi il compito di evitare la saturazione del buffer del ricevente, regolando la velocità di trasmissione del mittente in funzione della capacità disponibile presso il destinatario. In sintesi, il problema del buffering consiste nel possibile riempimento dei buffer di ricezione quando il mittente è più veloce del destinatario; il controllo del flusso nasce proprio per prevenire questa situazione e garantire una trasmissione affidabile dei dati.

Infine, il problema del ritardo di propagazione. Il ritardo di propagazione può causare un utilizzo inefficiente del canale: il mittente, dopo aver inviato un frame, deve attendere che l'ACK raggiunga nuovamente la sorgente prima di poter continuare la trasmissione. Se il ritardo è elevato, il collegamento rimane inutilizzato per una parte significativa del tempo, riducendo il throughput complessivo.

Quindi i problemi da risolvere sono sostanziamente i seguenti:

- Problema del mittente lento e del destinatario veloce: massimizzare l'invio dei dati da parte del mittente.
- Problema del mittente veloce e del destinatario lento: limitare l'invio dei dati da parte del mittente.
- Problema del buffering: limitare l'invio dei dati da parte del mittente in modo che la memoria di ricezione del destinatario non si saturi.
- Problema del ritardo di propagazione: regolare la quantità di ACK restituiti dal destinatario in modo da minimizzare i ritardi dovuti all'invio ed alla ricezione degli ACK stessi.

##### 03.05.01. Comunicazione simplex senza restrizione
<!-- to do -->

##### 03.05.02. Comunicazione simplex stop-and-wait
<!-- to do -->

##### 03.05.03. Comunicazione con ACK e NACK
<!-- to do -->

##### 03.05.04. Comunicazione con timeout
<!-- to do -->

##### 03.05.05. Comunicazione con numerazione dei frame
<!-- to do -->

##### 03.05.06. Comunicazione con gestione dei duplicati
<!-- to do -->

##### 03.05.067. Comunicazione rate-based
<!-- to do -->

### 03.06. SWPs (Sliding Window Protocols)
<!-- to do - concetto di window -->
<!-- to do - concetto di sliding window -->
<!-- to do - pipeline dei frame -->
<!-- to do - protocollo Go-Back-N ARQ (Automatic Repeat reQuest) -->
<!-- to do - protocollo Selective Repat ARQ (Automatic Repeat reQuest) -->

### 03.07. Accesso al mezzo trasmissivo 
<!-- to do - problema dell'accesso condiviso -->
<!-- to do - problema delle collisioni -->
<!-- to do - canali condivisi e dedicati -->
<!-- to do - allocazione static dei canali -->
<!-- to do - allocazione dinamica dei canali -->

##### 03.07.01. ALOHA puro
<!-- to do -->

##### 03.07.02. Slotted ALOHA
<!-- to do -->

##### 03.07.03. CSMA (Carrier Sense Multiple Access)
<!-- to do -->

##### 03.07.04. CSMA/CD (Carrier Sense Multiple Access with Collision Detection)
<!-- to do -->

##### 03.07.05. Backoff esponenziale
<!-- to do -->

##### 03.07.06. CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)
<!-- to do -->

### 03.08. Ethernet
<!-- to do -->

### 03.09. Reti Wireless
<!-- to do -->

##### 03.09.01. Problema del dispositivo nascosto
<!-- to do -->

##### 03.09.02. Problema del dispositivo esposto
<!-- to do -->

##### 03.09.03. Meccanismo RTS (Request To Send)
<!-- to do -->

##### 03.09.04. Meccanismo CTS (Clear To Send)
<!-- to do -->

##### 03.09.05. Wi-Fi
<!-- to do -->

##### 03.09.06. Bluetooth
<!-- to do -->

##### 03.09.07. Controllo degli errori nelle reti wireless
<!-- to do -->

### 03.10. Sicurezza e problematiche del livello datalink
<!-- to do - problematiche di Ethernet -->
<!-- to do - MAC spoofing -->
<!-- to do - ARP spoofing -->
<!-- to do - VLAN hopping -->
<!-- to do - WPA -->