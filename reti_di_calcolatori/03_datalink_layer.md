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

Ora parliamo di uno dei codici di correzione degli errori più utilizzati oggigiorno nell'ambito delle reti di calcolatori: il LDPC (Low Density Parity Check, controllo di parità a bassa densità). Il LDPC è un algoritmo matematico ad alta efficienza utilizzato nelle telecomunicazioni e nell'informatica per correggere gli errori nei dati trasmessi attraverso canali di comunicazione soggetti a rumore, o durante l'archiviazione su supporti di memorizzazione digitali, come HD, SSD, CD e DVD. Così come il codice Reed-Solomon, anche il codice LDPC è un codice a blocchi e lineare. Il significato di tali due termini è già stato spiegato in precedenza. LDPC è talmente efficiente e relativamente semplice da utilizzare che viene impiegato perfino nelle reti wireless (senza fili), come le reti Wi-Fi e le reti 5G. Il principio di funzionamento, descritto in modo molto semplificato, è il seguente:

1. Prima di inviare i dati, il sistema aggiunge dei bit di controllo (bit di parità). Tali bit non sono casuali, ma contengono informazioni matematiche collegate ai bit originali: in pratica vengono calcolati scegliendo un opportunoo protocollo (parità pari, o dispari) considerando i bit del messaggio che risiedono in una determinata posizione.
2. Il nome bassa densità deriva dal modo in cui vengono calcolati questi controlli. La struttura matematica (matrice) usata per legare i dati contiene moltissimi 0 e pochissimi 1: questa è una caratteristica importante per questo tipo di codici. Questo rende i calcoli molto efficienti.
3. All'arrivo, il ricevitore controlla se i dati soddisfano le regole matematiche. Se trova un errore (ad esempio, uno 0 che è diventato un 1 a causa di un'interferenza), l'algoritmo effettua dei tentativi successivi (iterazioni) analizzando i bit vicini, riuscendo a ricostruire e correggere il dato originale con estrema precisione.

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

La comunicazione simplex senza restrizione è la più semplice che si possa immaginare. In pratica, in questo tipo di comunicazione si ragiona come se il canale trasmissivo fosse perfetto:

- Si hanno due soli host in comunicazione tra loro: il mittente (che trasmette i dati) e il destinatario (che li legge, o li riceve).
- Si ha un solo verso in cui possono scorrere i dati: dal mittente al destinatario. Si tratta di una comunicazione simplex.
- Non c'è alcun ritardo nella comunicazione.
- Il mittente trasmette i dati alla massima velocità consentita.
- Il destinatario non iniva alcuna conferma di ricezione, detta ACK.
- Assenza di qualsiasi forma d'errore.
- Nessun buffer di invio, o di ricezione necessario.

Questo protocollo non viene (e probabilmente non verrà mai) implementato nell'effettiva pratica, in quanto non esiste un canale trasmissivo perfetto. Anche se il BER con le moderne tecnologie è stato decrementato parecchio, è quasi impossibile ottenere un canale trasmissivo perfetto. Il minimo rumore, o qualche interferenza elettromagnetica potrebbe causare disallineamenti della sincronizzazione, o fluttuazioni improvvise del segnale, che scambiano i valori 1 con 0 e viceversa.

##### 03.05.02. Comunicazione simplex stop-and-wait

Qui il gioco inizia a farsi più carino. A differenza della comunicazione simplex senza restrizione, in questo caso si valuta la possobilità che un frame possa subire errori, oppureche possa non arrivare a destinazione (magari a causa di un guasto improvviso di qualche apparato di livello datalink frapposto tra gli host, o che affligge il mezzo trasmissivo stesso). Questo tipo di comunicazione è basata sui seguenti presupposti:

- Si hanno due soli host in comunicazione tra loro: il mittente (che trasmette i dati) e il destinatario (che li legge, o li riceve).
- Si ha un solo verso in cui possono scorrere i dati: dal mittente al destinatario. Si tratta di una comunicazione simplex.
- Non c'è alcun ritardo nella comunicazione.

Bisogna fare una piccolaprecisazione: i dati scorrono in una sola direzione (dal mittente al destinatario), ma i messaggi di controllo possono scorrere in ambedue le direzioni. Ad esempio, gli ACK restituiti dal destinatario possono scorrere nel verso opposto rispetto a quello dei dati. Questi sono gli stessi punti della comunicazione precedente. In aggiunta ad essi vanno considerati i seguenti:

- C'è la possibile che il segnale subisca degli errori, o venga perso.
- Il mittente trasmette un frame alla volta e, dopo l'invio di ciascun frame, si mette in attesa di un'ACK da parte del destinatario.
- Il destinatario iniva una conferma di ricezione (ACK) ogni volta che riceve un frame.
- Assenza di qualsiasi forma d'errore.
- Nessun buffer di invio, o di ricezione necessario.

La situazione descritta dai precedenti punti è la seguente:

<!-- to add -->
*In Figura: la comunicazione simplex stop-and-wait*

In pratica, il mittente invia il frame si mette in attesa di una ACK (fase stop), nel mentre che il messaggio arriva il destinatario e quest'ultimo invia l'ACK, il mittente rimane in attesa (wait). Dopo che il mittente ha ricevuto l'ACK, invia il frame successivo.

##### 03.05.03. Comunicazione con ACK e NACK e timeout

In questi protocolli di comunicazione il modo con il quale si inviano frame i due host è molto simile a quanto abbiamo analizzato per la comunicazione simplex stop-and-wait, ma vi è l'aggiunta di un altro elemento: la conferma di non ricezione, detta anche UNACK, o più comunemente NACK. Si tratta di un frame di controllo molto simile al frame ACK, ma che al posto di indicare che un determinato frame è stato ricevuto con successo, indica che un frame (o un determinato gruppo di frame) non è stato ricevuto, per cui il mittente, alla ricezione del NACK, iniva nuovamente i frame non ricevuti dal destinatario.

Vi è l'introduzione di un secondo elemento: il timeout. In pratica, esiste un tempo ben definito e prestabilito secondo il quale, una volta inviato il frame, il mittente si aspetta un'ACK, o un NACK. Questa finestra temporale è fondamentale nei protocolli del livello datalink e dipende in genere sia dalla velcoità di trasmissione dell'host stesso, sia dal mezzo trasmissivo. Che succede se il mittente riceve un'ACK, o un NACK fuori dal tempo di timeout? Gli scarta. Analogamente, che succede se il mittente non riceve alcun ACK, o NACK entro il timeout per uno, o più frame? Invia nuovamente i frame che aveva inviato. In alcuni protocolli esiste una politica per il quale se il mittente arriva ad inviare per un certo numero di volte lo stesso frame senza ricevere ACK, o NACK, allora c'è un problema nel mezzo trasmissivo, oppure nell'host destinatario.

I due nuovi elementi, NACK e timeout, si possono rappresentare in modo molto schematico in questo modo:

<!-- to add -->
*In Figura: comunicazione con ACK e NACK e timout*

##### 03.05.06. Comunicazione con numerazione dei frame

In questo nuovo tipo di comunicazione, si aggiunge un nuovo elemento alla comunicazione con ACK/NACK e timeout: la numerazione dei frame. A seconda del protocollo del livello datalink utilizzato, esiste un campo di una certa lunghezza (2 Byte, solitamente) per la numerazione dei frame: si possono numerare 65536 frame, da 0 a 65525. L'idea di base è questa: il mittente spedisce i frame contenenti ciascuno una determinata porzione del messaggio originale (che può essere un file di grandi dimensioni, o altro), ma numera i frame della comunicazione partendo da 0 e incremento di una unità ciascun frame che invia. Quindi il mittente invia il frame numero 0, poi il frame numero 1, poi il 2 e così via, fino ad arrivare a 65 535. Che succede quando si raggiunge il massimo valore possibile per la numerazione dei frame? Molto semplice, a rotaazione, si riparte da 0 e la numerazione riprende da capo. Esistono protocolli che consentono anche al destinatario di comprendere questo tipo di casistica: se un host riceve il frame 65 535 e poi, successivamente, per la stessa comunicazione riceve il frame 0, allora quest'ultimo frame è il successivo del frame precedente, anche se ha un numero inferiore. Il numero dei frame viene anche detto sequence number (numero di sequenza).

Ecco che i frame ACK/NACK assumono un ruolo leggermente diverso: all'interno di essi il destinatario specifica il numero di frame che ha ricevuto, per cui il mittente dovrà occuparsi di spedire solo i frame con numero di sequenza maggiore a quello indicato nella ACK. Il caso è differente nel caso di una NACK, in quanto quest'ultima indica che proprio uno specifico frame, con un determinato numero di sequenza, non è stato ricevuto (magari per un guasto improvviso, o per un elevato traffico sul mezzo trasmissivo). In questo caso il mittente invia solo il frame con lo stesso numero di sequenza indicato nel NACK.

In questo modo si rende possibile una cosa molto interessante: perché inviare un ACK/NACK ad ogni frame, come accade nei protocolli di tipo stop-and-wait puro, in cui si invia un frame e ci si mette in attesa di un ACK? Ebbene, grazie alla numerazione di sequenza, il mittente può inviare più frame senza aspettarsi un ACK (tipicamente da 2 a 8 frame, o più se il protocollo lo prevede), ma esso si aspetta solo l'ACK dopo aver inviato l'ultimo frame del gruppo. Questa situazione è tipica dei protocolli a finestra scorrevole (SWPs, Sliding Window Protocols), che esamineremo in seguito.

Questa situazione si può rappresentare nel seguente modo:

<!-- to add -->
*In Figura: utilizzare il sequence number per numerare i frame ed anche una ACK per un gruppo di frame*

C'è una piccola cosa che abbiamo detto in precedenza, ma che in realtà in questo nuovo modo di comunicare potrebbe tranquillamente non essere vera. Prima abbiamo detto che se il mittente dovesse ricevere un ACK dopo il timeout, questo verrebbe scartato. Ma in realtà un ACK può giungere al mittente in ritardo per svariati motivi ed alcuni protocolli non associano un timeout particolare all'invio degli ACK: così, se il mittente riceve un ACK anche dopo molto tempo, questo lo accetta ed invia i frame che hanno sequence number maggiore rispetto a quello indicato nel frame.

##### 03.05.07. Comunicazione con gestione dei duplicati

La gestione dei duplicati nel datalink layer si basa sull'uso dei sequence number, gli stessi di cui abbiamo parlato nel paragrafo precedente. I sequence number inseriti nell'header del frame sono fortemente usati dai protocolli di ritrasmissione con riscontro, anche noti con l'acronimo (ARQ -Automatic Repeat Request-).

Il meccanismo per evitare che lo stesso frame venga elaborato più volte segue questi principi:

- Numerazione dei frame: ogni frame inviato riceve un numero di sequenza univoco.- Controllo del destinatario: quando il ricevitore ottiene un frame, confronta il numero di sequenza con il valore atteso.
- Scarto dei duplicati: se il numero di sequenza è già stato ricevuto ed elaborato, il frame viene scartato, inviando comunque un ACK al mittente.

I protocolli più noti che gestiscono i duplicati sono Stop-and-Wait ARQ, Go-Back-N ARQ e Selective Repeat ARQ.

##### 03.05.08. Comunicazione rate-based

Ed ecco che qui analizziamo la comunicazione più complessa (e realmente utilizzata nell'Internet odierna). La comunicazione rate-based a livello datalink è un meccanismo che regola la velocità di trasmissione dei frame tra due host adiacenti, posti in diretta comunicazione tra loro mediante un opportuno mezzo trasmissivo. A differenza dei sistemi guidati dalle sole richieste del ricevitore (flow control reattivo), il rate-based pacing impone un limite preciso al flusso di bit. I due punti chiave secondo il quale funziona questo tipo di comunicazione sono i seguenti:

- Regolazione del ritmo: il mittente della comunicazione invia i frame a una velocità fissa, o concordata (ad esempio tramite un speciale frame che prende il nome di token bucket) per evitare di congestionare il ricevitore, oppure i nodi intermedi. Ricordiamo che per "nodi intermedi" si intendono gli host intermedi del livello datalink (come switch, hub, bridge e ripetitori, nel caso di LAN più estese).
- Controllo della congestione: previene il riempimento dei buffer del ricevitore. L'invio è spaziato nel tempo per adattarsi esattamente alla capacità di elaborazione del dispositivo adiacente. I protocolli rate-based evitano il più possibile di saturare il buffer del ricevitore (ma anche quello del mittente), avendo un controllo diretto sulla congestione del traffico.

In pratica questo protocollo di comunicazione prevede:

- Un meccanismo stop-and-wait basato su gruppi di frame.
- Il sequence number da utilizzare nell'header dei frame.
- Il timeout per l'invio di un frame, o un gruppo di frame.
- L'utilizzo di ACK per confermare la ricezione di uno, o più frame.
- L'utilizzo di NACK per confermare la non-ricezione di un frame preciso.
- Meccanismi di rate limiting dell'invio dei dati lato mittente.
- Meccanismi di feedback per limitare la congestione del traffico lato destinatario.
- Finestre temporali e finestre a scorrimento (elementi molto importanti analizzati nel prossimo paragrafo).

### 03.06. SWPs (Sliding Window Protocols)

Gli SWPs (Sliding Window Protocols) sono una famiglia di protocolli molto utilizzata nel livello datalink dello stack TCP/IP che prevede la trasmissione di più frame in sequenza, senza attendere una ACK da parte del destinatario. Questa famiglia di protocolli consente una comunicazione rate-based tra i due host collegati in modo diretto, quindi si parla di protocolli molto complessi e dotati di numerosi meccanismi per gestire la congestione del traffico.

Ma che cosa è una finestra? Una finestra (o finestra a scorrimento) è un insieme di numeri di sequenza che sono tenuti sotto controllo da parte del mittente nell'ambito di una determinata comunicazione. Una finestra scorrevole (in inglese sliding window) è una finestra che si inizia al sequence number $n$ e termina al sequence number $m$, ovviamente con $n < m$: l'ampiezza (o larghezza) della finestra è data dalla differenza $m - n$. Solitamente l'ampiezza è uguale ad una potenza di due, ma è un parametro che varia a seconda della comunicazione, della congestione e del servizio richiesto da mittente e destinatario. Alcune comunicazioni possono avere finestre molto ampie, mentre altri finestre molto corte.

Esistono due tipi principali di finestre:

- Finestra del mittente (sender window): contiene i sequence number dei frame che devono essere spediti. Attenzione che, in un dato momento, la finestra del mittente può avere alcuni frame già trasmessi, mentre altri ancora da trasmettere: la finestra NON indica i frame inviati, ma solo quelli che sono abilitati all'invio.
- Finestra del ricevente (receiver window): definisce i sequence number dei frame che il ricevitore è consentito a ricevere. Questo significa che qualsiasi frame con numero di sequenza al di fuori di quelli indicati nella propria finestra vengono automaticamente scartati.

Normalmente, la finestra del ricevente è più ampia rispetto a quella del mittente. Il meccanismo fondamentale di tutti i protocolli SWPs è il seguente: quando il ricevente invia un'ACK con un certo numero di sequenza, le sliding window di mittente e ricevitore si spostano in avanti, includendo i successivi sequence number dei frame che devono essere trasmessi. Ciò garantisce un controllo diretto e molto preciso del traffico.

##### 03.06.01. Protocollo Go-Back-N ARQ (Automatic Repeat reQuest)

Il protocollo Go-Back-N ARQ è uno dei più importanti protocolli a finestra scorrevole del livello datalink. L'idea centrale è molto semplice: il mittente non si limita ad inviare un solo frame e attendere il relativo ACK, ma può inviare consecutivamente un intero gruppo di frame, purché i loro sequence number rientrino all'interno della propria sender window. Il valore $N$ del nome del protocollo indica proprio il numero massimo di frame che il mittente può avere "in volo" (cioè trasmessi ma non ancora confermati) nello stesso istante.

Nel protocollo Go-Back-N il ricevente adotta un comportamento molto rigido: accetta soltanto il frame che possiede esattamente il sequence number atteso. Se riceve correttamente il frame atteso, lo consegna al livello superiore e aggiorna il numero di sequenza successivo atteso. Se invece riceve un frame fuori ordine, lo scarta. In altre parole, il ricevente non memorizza i frame arrivati in anticipo rispetto a quello mancante, ma li considera inutilizzabili finché non giunge il frame corretto. Per questo motivo si dice che, dal punto di vista logico, la receiver window del protocollo Go-Back-N ha ampiezza pari a 1.

La conferma di ricezione utilizzata in Go-Back-N è cumulativa. Questo significa che un ACK non conferma solo un singolo frame, ma tutti i frame ricevuti correttamente fino a quel momento in ordine. Se, ad esempio, il destinatario invia un ACK riferito al frame 4, ciò significa che tutti i frame fino al 4 sono stati ricevuti correttamente e che il prossimo frame atteso è il 5. Questo meccanismo riduce il numero di messaggi di controllo necessari e rende il protocollo più efficiente rispetto allo stop-and-wait.

Il comportamento del mittente può essere riassunto così:

- mantiene una finestra di ampiezza $N$ contenente i frame che può trasmettere;
- invia tutti i frame consentiti dalla finestra senza fermarsi dopo ciascuno di essi;
- avvia un timer per il frame meno recente ancora privo di conferma;
- quando riceve un ACK cumulativo, fa scorrere in avanti la finestra e può inviare nuovi frame;
- se scade il timeout del frame più vecchio non confermato, ritrasmette quel frame e tutti i successivi già inviati ma non ancora confermati.

È proprio quest'ultimo comportamento a dare il nome al protocollo: go back significa infatti "tornare indietro". Se, per esempio, il mittente invia i frame 0, 1, 2, 3 e 4 e il frame 2 viene perso, il destinatario riceverà magari i frame 3 e 4, ma li scarterà perché sta ancora aspettando il frame 2. Quando il timer del frame 2 scade, il mittente non ritrasmette soltanto il frame mancante, bensì riparte dal frame 2 e invia nuovamente anche i frame 3 e 4. In pratica torna indietro al primo frame non confermato e ritrasmette tutto il blocco successivo.

La seguente situazione può essere rappresentata come segue:

<!-- to add -->
*In Figura: funzionamento del protocollo Go-Back-N con perdita di un frame e ritrasmissione cumulativa*

I vantaggi principali del protocollo Go-Back-N sono la relativa semplicità di implementazione e la buona efficienza quando il canale trasmissivo è poco rumoroso, cioè quando gli errori e le perdite di frame sono rari. In queste condizioni, il mittente riesce a sfruttare bene il canale inviando più frame consecutivamente e ricevendo ACK cumulativi.

Tuttavia, il protocollo presenta anche un importante svantaggio: se un singolo frame viene perso, o arriva con errore, tutti i frame successivi già trasmessi e ricevuti fuori ordine devono essere inviati nuovamente, anche se erano arrivati correttamente al destinatario. Questo può causare uno spreco significativo di banda nei canali soggetti a rumore, o nelle reti con ritardi elevati. Proprio per ridurre questo problema è stato introdotto un protocollo più evoluto, chiamato Selective Repeat ARQ, che analizzeremo nel prossimo paragrafo.

##### 03.06.02. Protocollo Selective Repeat ARQ (Automatic Repeat reQuest)

Il protocollo Selective Repeat ARQ rappresenta una evoluzione del Go-Back-N ARQ ed è stato progettato proprio per evitare la ritrasmissione inutile di frame che, in realtà, erano già arrivati correttamente al destinatario. L'idea fondamentale è che non tutti gli errori devono obbligare il mittente a tornare indietro e reinviare un intero blocco di frame: è spesso sufficiente ritrasmettere soltanto i frame effettivamente persi, o danneggiati. Da qui deriva il termine selective repeat, cioè "ritrasmissione selettiva".

Nel protocollo Selective Repeat sia il mittente, sia il destinatario utilizzano una vera finestra scorrevole di ampiezza maggiore di 1. Questo significa che il ricevente non si limita più ad accettare il solo frame atteso, ma può anche accettare frame arrivati fuori ordine, purché il loro sequence number rientri all'interno della receiver window. I frame ricevuti correttamente ma fuori ordine non vengono scartati: vengono temporaneamente memorizzati in un buffer, in attesa che arrivino i frame mancanti che permettono di ricostruire la corretta sequenza dei dati.

Il comportamento del protocollo può essere descritto così:

- il mittente invia più frame consecutivi, purché rientrino nella propria sender window;
- ciascun frame trasmesso ha normalmente un proprio timer associato;
- il destinatario conferma singolarmente i frame ricevuti correttamente, oppure segnala esplicitamente quelli mancanti;
- i frame arrivati fuori ordine vengono memorizzati dal ricevente e non scartati;
- se scade il timeout di un certo frame, il mittente ritrasmette soltanto quel frame, e non l'intero gruppo successivo.

Questo è il punto di maggiore differenza rispetto al Go-Back-N. Supponiamo, per esempio, che il mittente invii i frame 0, 1, 2, 3 e 4 e che il frame 2 venga perso. Se il destinatario riceve i frame 3 e 4, non li elimina: li conserva nel proprio buffer e invia gli opportuni ACK per segnalare che quei frame sono stati ricevuti. Quando il mittente si accorge, tramite timeout o tramite un NACK, che il frame 2 non è arrivato, ritrasmette soltanto il frame 2. Appena il ricevente lo riceve, può ricostruire l'intera sequenza e consegnare al livello superiore anche i frame 3 e 4 che aveva già memorizzato.

La situazione può essere rappresentata nel seguente modo:

<!-- to add -->
*In Figura: funzionamento del protocollo Selective Repeat con memorizzazione dei frame fuori ordine e ritrasmissione selettiva*

Affinché il protocollo funzioni correttamente, bisogna prestare particolare attenzione alla dimensione della finestra e all'intervallo dei numeri di sequenza. Poiché i sequence number vengono riutilizzati ciclicamente, una finestra troppo ampia potrebbe generare ambiguità tra frame nuovi e frame vecchi duplicati. Per questo motivo, nei protocolli Selective Repeat la dimensione della finestra è scelta in modo più restrittivo rispetto al Go-Back-N: in termini generali, essa non deve superare la metà dello spazio totale dei numeri di sequenza disponibili.

I vantaggi del Selective Repeat ARQ sono evidenti nei canali rumorosi, o nelle reti con ritardi elevati. Poiché vengono ritrasmessi solo i frame realmente persi o corrotti, si ha un utilizzo della banda molto più efficiente rispetto al Go-Back-N. Inoltre, il destinatario non spreca il lavoro già svolto sui frame ricevuti correttamente fuori ordine, ma li conserva per usarli non appena la sequenza diventa completa.

Naturalmente questi benefici si pagano con una maggiore complessità implementativa. Il mittente deve gestire più timer contemporaneamente, uno per ciascun frame non ancora confermato. Il destinatario, invece, deve mantenere un buffer per i frame fuori ordine e una logica più sofisticata per decidere quando la sequenza è completa e può essere consegnata al livello superiore. In sintesi, il Selective Repeat è più efficiente del Go-Back-N, ma anche più costoso in termini di memoria, controllo e logica di gestione.

### 03.07. Accesso al mezzo trasmissivo 

Uno dei problemi più importanti che il livello datalink deve affrontare è quello dell'accesso al mezzo trasmissivo, ovvero il modo in cui più host che condividono lo stesso mezzo trasmissivo possono trasmettere i propri dati senza interferire l'uno con l'altro. Questo problema, noto anche come problema dell'accesso condiviso, si presenta in tutte quelle situazioni in cui il mezzo trasmissivo non è dedicato a una singola coppia di host (come avviene, ad esempio, in una connessione punto-a-punto tra due dispositivi collegati direttamente da un cavo), ma è condiviso da più host che possono potenzialmente voler trasmettere nello stesso istante. Esempi tipici sono le reti Ethernet basate su hub, le reti Wi-Fi, le reti radio, le reti satellitari ed in generale tutte le reti con topologia a bus, o ad anello.

Il principale problema che nasce dalla condivisione del mezzo trasmissivo è quello delle collisioni. Una collisione si verifica quando due, o più host, trasmettono contemporaneamente sullo stesso mezzo trasmissivo: i segnali generati dai diversi host si sovrappongono, dando origine a un segnale risultante che, nella maggior parte dei casi, è completamente illeggibile per qualsiasi host della rete. Quando si verifica una collisione, i frame coinvolti vengono persi e devono essere ritrasmessi, con conseguente spreco di banda e aumento dei tempi di latenza della comunicazione. Nel caso peggiore, se le collisioni avvengono con una frequenza molto elevata (ad esempio in una rete molto congestionata, con tanti host che cercano di trasmettere contemporaneamente), il throughput effettivo della rete può crollare drasticamente, rendendo la comunicazione di fatto impraticabile. Per questo motivo, è fondamentale che il livello datalink disponga di meccanismi efficaci per gestire l'accesso al mezzo trasmissivo, riducendo al minimo la probabilità di collisioni e, quando queste si verificano, gestendole in modo appropriato.

Prima di analizzare le varie tecniche di accesso al mezzo trasmissivo, è utile distinguere tra due categorie principali di canali: i canali dedicati ed i canali condivisi. Un canale dedicato è un canale trasmissivo riservato esclusivamente a una determinata coppia di host: tutto il traffico che vi transita è generato da uno dei due host e destinato all'altro, per cui non esiste il problema delle collisioni e non sono necessari meccanismi particolari di accesso al mezzo. Un esempio tipico di canale dedicato è il collegamento punto-a-punto tra due router di un'azienda, oppure il collegamento via cavo tra un computer ed una stampante. Un canale condiviso, invece, è un canale trasmissivo utilizzato da più host contemporaneamente, ciascuno dei quali può potenzialmente voler trasmettere i propri dati in un qualsiasi istante. In questo caso, è necessario adottare opportune tecniche per regolare l'accesso al mezzo trasmissivo, in modo da evitare (o gestire) le collisioni e garantire una comunicazione efficiente tra gli host. Esempi tipici di canali condivisi sono le reti Wi-Fi (in cui più dispositivi condividono la stessa banda radio) e le reti Ethernet tradizionali basate su hub (in cui più dispositivi condividono lo stesso cavo).

Per quanto riguarda i canali condivisi, le tecniche utilizzate per gestire l'accesso al mezzo trasmissivo si suddividono in due grandi famiglie: l'allocazione statica e l'allocazione dinamica. L'allocazione statica prevede che la banda disponibile sul canale trasmissivo venga suddivisa a priori tra tutti gli host della rete, assegnando a ciascuno una porzione fissa della banda totale. Le tecniche più note di allocazione statica sono il TDM (Time Division Multiplexing), in cui ciascun host può trasmettere solo in determinati intervalli di tempo prestabiliti, ed il FDM (Frequency Division Multiplexing), in cui ciascun host può trasmettere solo su una determinata banda di frequenze. L'allocazione statica è semplice da implementare e garantisce l'assenza di collisioni, ma è anche estremamente inefficiente: se un host non ha dati da trasmettere, la sua porzione di banda rimane inutilizzata e non può essere sfruttata dagli altri host della rete. Inoltre, l'allocazione statica funziona bene solo quando il numero di host della rete è noto a priori e rimane costante nel tempo, situazione che si verifica raramente nelle reti moderne.

L'allocazione dinamica, invece, prevede che la banda disponibile sul canale trasmissivo venga assegnata agli host in modo dinamico, in base alle effettive esigenze di trasmissione di ciascuno. In altre parole, ciascun host può accedere al mezzo trasmissivo solo quando ha effettivamente dei dati da trasmettere, lasciando libero il canale negli altri istanti. Questo approccio è molto più efficiente dell'allocazione statica, in quanto consente di sfruttare al meglio la banda disponibile, ma introduce il problema della gestione delle collisioni, in quanto più host possono potenzialmente cercare di trasmettere contemporaneamente. Per questo motivo, sono state sviluppate numerose tecniche di allocazione dinamica, ciascuna delle quali adotta un approccio diverso per ridurre la probabilità di collisioni e gestirle quando si verificano. Tra le tecniche più note, che analizzeremo nei prossimi sottoparagrafi, vi sono ALOHA puro, Slotted ALOHA, CSMA (con le sue varianti CSMA/CD e CSMA/CA) ed il meccanismo del backoff esponenziale.

##### 03.07.01. ALOHA puro

ALOHA puro è uno dei primi protocolli di accesso dinamico al mezzo trasmissivo sviluppati nella storia delle reti di calcolatori. Fu ideato per reti radio, quindi per canali condivisi nei quali più host possono tentare di trasmettere nello stesso istante senza avere un controllo centralizzato del mezzo. L'idea di base del protocollo è estremamente semplice: quando un host ha un frame da trasmettere, lo trasmette immediatamente, senza attendere alcun istante particolare e senza verificare in anticipo se il canale sia libero, oppure occupato.

Questa scelta rende il protocollo molto semplice da implementare, ma introduce un problema evidente: due host potrebbero decidere di trasmettere quasi nello stesso istante. In tal caso i frame si sovrappongono nel mezzo trasmissivo, generando una collisione. Poiché il canale è condiviso, il destinatario non riesce più a distinguere correttamente i dati ricevuti e i frame coinvolti devono essere considerati persi.

Il funzionamento di ALOHA puro può essere descritto nei seguenti passi:

- un host genera un frame da inviare;
- il frame viene trasmesso immediatamente sul canale condiviso;
- il mittente attende una conferma di ricezione, oppure un tempo massimo di risposta;
- se la conferma arriva correttamente, la trasmissione è considerata completata;
- se la conferma non arriva entro il tempo previsto, il mittente assume che si sia verificata una collisione e ritrasmette il frame dopo un intervallo di tempo casuale.

L'attesa di un intervallo casuale prima della ritrasmissione è fondamentale. Se due host che hanno colliso ritrasmettessero immediatamente il frame nello stesso istante, colliderebbero di nuovo. Introducendo un ritardo casuale, si aumenta la probabilità che le successive ritrasmissioni avvengano in istanti differenti, riducendo quindi il rischio di nuove collisioni ripetute.

Il principale limite di ALOHA puro è che il protocollo non impone alcuna sincronizzazione temporale tra gli host. Un frame può iniziare in qualsiasi istante e può quindi collidere con un altro frame che sia iniziato poco prima, o poco dopo. In termini teorici, se indichiamo con $T$ il tempo necessario a trasmettere un frame, un frame è vulnerabile alle collisioni per un intervallo totale pari a $2T$: può infatti entrare in collisione con un altro frame iniziato fino a un tempo $T$ prima, oppure fino a un tempo $T$ dopo il suo inizio. Questo intervallo prende il nome di periodo vulnerabile (vulnerable period).

La seguente situazione può essere rappresentata nel seguente modo:

<!-- to add -->
*In Figura: funzionamento di ALOHA puro con trasmissione immediata e possibile collisione tra due frame*

Dal punto di vista delle prestazioni, ALOHA puro è piuttosto inefficiente. Il massimo throughput teorico del protocollo è pari a circa il 18% della capacità del canale. Questo significa che, anche nelle condizioni migliori, una parte molto ampia della banda disponibile viene sprecata a causa delle collisioni e delle conseguenti ritrasmissioni. Per questo motivo ALOHA puro è importante soprattutto dal punto di vista storico e concettuale: ha mostrato che era possibile progettare protocolli distribuiti per l'accesso al mezzo, ma ha anche evidenziato la necessità di meccanismi più efficienti.

I vantaggi di ALOHA puro sono quindi la semplicità, la totale decentralizzazione e la facilità di utilizzo in reti radio molto semplici. Gli svantaggi, invece, sono numerosi: elevata probabilità di collisione, scarso sfruttamento della banda, numero elevato di ritrasmissioni e throughput ridotto. Proprio per migliorare questi aspetti è stato introdotto il protocollo Slotted ALOHA, che analizzeremo nel prossimo paragrafo.

##### 03.07.02. Slotted ALOHA

Il protocollo Slotted ALOHA nasce come miglioramento diretto di ALOHA puro. L'idea fondamentale è introdurre una sincronizzazione temporale tra tutti gli host della rete, in modo da ridurre la probabilità di collisione. Invece di permettere l'inizio della trasmissione in un qualsiasi istante, il tempo viene suddiviso in intervalli discreti di uguale durata, detti slot temporali (time slots). Ciascuno slot ha una durata sufficiente a trasmettere esattamente un frame.

La regola del protocollo è molto semplice: un host che ha un frame da inviare può iniziare a trasmettere solo all'inizio di uno slot. Se il frame viene generato mentre uno slot è già in corso, il mittente deve attendere l'inizio dello slot successivo. In questo modo vengono eliminate tutte le collisioni parziali tipiche di ALOHA puro: due frame non possono più sovrapporsi solo in parte, ma collidono soltanto se due o più host iniziano a trasmettere esattamente nello stesso slot.

Il funzionamento di Slotted ALOHA può essere riassunto nei seguenti punti:

- il tempo del canale è suddiviso in slot consecutivi, tutti della stessa lunghezza;
- ogni host conosce la sincronizzazione comune degli slot;
- se un host ha un frame da trasmettere, aspetta l'inizio del primo slot disponibile;
- se nello stesso slot trasmette un solo host, il frame viene ricevuto correttamente;
- se nello stesso slot trasmettono due o più host, si verifica una collisione e tutti i frame di quello slot vengono persi;
- in caso di collisione, ciascun mittente ritenta la trasmissione in uno slot successivo scelto secondo un criterio casuale.

La differenza rispetto ad ALOHA puro è quindi sostanziale. In ALOHA puro un frame è vulnerabile alle collisioni per un intervallo totale pari a $2T$, dove $T$ è il tempo di trasmissione del frame. In Slotted ALOHA, invece, il periodo vulnerabile si riduce a $T$, perché le collisioni possono avvenire soltanto all'interno dello stesso slot temporale. Questo semplice accorgimento raddoppia, in termini teorici, l'efficienza massima del protocollo.

La situazione può essere rappresentata nel seguente modo:

<!-- to add -->
*In Figura: funzionamento di Slotted ALOHA con tempo suddiviso in slot e collisione solo se più host trasmettono nello stesso slot*

Dal punto di vista delle prestazioni, Slotted ALOHA è sensibilmente migliore di ALOHA puro. Il throughput teorico massimo raggiunge circa il 37% della capacità del canale, cioè circa il doppio rispetto ad ALOHA puro. Questo miglioramento deriva proprio dalla riduzione del periodo vulnerabile e dal fatto che le collisioni sono possibili solo in corrispondenza degli allineamenti sugli slot.

Nonostante questo miglioramento, Slotted ALOHA presenta ancora limiti importanti. Se molti host desiderano trasmettere contemporaneamente, più nodi tenderanno comunque a scegliere gli stessi slot, provocando collisioni e ritrasmissioni. Inoltre, la sincronizzazione degli slot richiede un meccanismo comune di temporizzazione, che rende il protocollo più complesso rispetto ad ALOHA puro. Esiste poi un'ulteriore inefficienza: se in uno slot nessun host trasmette, quello slot resta completamente inutilizzato e la banda va persa.

I vantaggi principali di Slotted ALOHA sono quindi il miglior sfruttamento del canale rispetto ad ALOHA puro, la riduzione delle collisioni parziali e una migliore prevedibilità temporale delle trasmissioni. Gli svantaggi sono la necessità di sincronizzazione globale, la persistenza delle collisioni quando più host scelgono lo stesso slot e un'efficienza ancora limitata rispetto ai protocolli più evoluti. Proprio per superare anche questi limiti sono stati sviluppati protocolli che ascoltano il canale prima di trasmettere, come il CSMA, che analizzeremo nel prossimo paragrafo.

##### 03.07.03. Backoff esponenziale

Il backoff esponenziale è una tecnica utilizzata per gestire le ritrasmissioni dopo una collisione in un canale condiviso. L'idea di base è molto intuitiva: quando due, o più host collidono, non devono ritentare immediatamente la trasmissione, perché rischierebbero di collidere di nuovo nello stesso istante. Occorre invece introdurre un tempo di attesa casuale prima del nuovo tentativo. Il termine esponenziale indica proprio il fatto che, al crescere del numero di collisioni consecutive, cresce anche l'intervallo di tempo entro cui il nodo sceglie casualmente quando ritrasmettere.

Questa tecnica è estremamente importante perché consente di ridurre la probabilità di collisioni ripetute nelle reti in cui più host competono per lo stesso mezzo trasmissivo. Il backoff esponenziale non è, di per sé, un protocollo completo di accesso al mezzo, ma un meccanismo di supporto utilizzato da protocolli più complessi, come per esempio CSMA/CD e, in forme differenti, anche in altri sistemi di accesso distribuito.

Il funzionamento generale è il seguente:

- un host tenta di trasmettere un frame;
- se non si verifica alcuna collisione, la trasmissione procede normalmente;
- se si verifica una collisione, il frame viene considerato non trasmesso con successo;
- il mittente attende un intervallo di tempo casuale prima di ritentare;
- se la collisione si ripete, l'intervallo casuale da cui scegliere il ritardo viene ampliato progressivamente.

L'idea matematica alla base del backoff esponenziale consiste nell'aumentare la finestra di attesa dopo ogni collisione. Dopo il primo insuccesso il nodo sceglie casualmente un piccolo ritardo; dopo il secondo, sceglie il ritardo da un insieme più ampio; dopo il terzo, da un insieme ancora più grande, e così via. Se indichiamo con $k$ il numero di collisioni consecutive subite da un frame, il nodo sceglie tipicamente un numero casuale in un intervallo proporzionale a $2^k$. In termini qualitativi, quindi, la finestra di attesa raddoppia dopo ciascuna collisione, almeno fino a un limite massimo stabilito dal protocollo.

Questo comportamento ha un vantaggio fondamentale: quando la rete è poco congestionata, i ritardi introdotti restano molto piccoli e l'efficienza è elevata. Quando invece molti host stanno collidendo tra loro, il meccanismo allarga rapidamente l'intervallo di ritrasmissione, distribuendo meglio nel tempo i successivi tentativi e diminuendo così la probabilità che i nodi si scontrino ancora tutti insieme.

La situazione può essere rappresentata nel seguente modo:

<!-- to add -->
*In Figura: backoff esponenziale con aumento progressivo della finestra casuale di ritrasmissione dopo collisioni successive*

Il caso più noto di utilizzo del backoff esponenziale è il binary exponential backoff impiegato nelle reti Ethernet classiche con CSMA/CD. In quel contesto, dopo la prima collisione il nodo sceglie un ritardo casuale tra due possibili valori; dopo la seconda collisione sceglie tra quattro; dopo la terza tra otto, e così via, fino a un massimo fissato dallo standard. Se si supera un certo numero di tentativi senza successo, il frame viene scartato e il protocollo segnala un errore ai livelli superiori.

I vantaggi del backoff esponenziale sono la semplicità concettuale, la capacità di adattarsi dinamicamente al livello di congestione del canale e la riduzione delle collisioni ripetute. Tuttavia, esistono anche alcuni limiti: in condizioni di traffico molto elevato il ritardo medio può crescere notevolmente, aumentando la latenza; inoltre, il meccanismo non elimina del tutto le collisioni, ma si limita a renderle meno probabili. In sintesi, il backoff esponenziale è un meccanismo di stabilizzazione del traffico molto efficace, ma dà il meglio di sé quando è integrato all'interno di protocolli di accesso al mezzo più completi, come quelli che analizzeremo nel prossimo paragrafo.

##### 03.07.04. CSMA (Carrier Sense Multiple Access), CSMA/CD e CSMA/CA

Il CSMA (Carrier Sense Multiple Access) rappresenta un importante passo avanti rispetto ai protocolli ALOHA. L'idea centrale è semplice ma molto efficace: prima di trasmettere, un host ascolta il canale per capire se esso sia libero, oppure occupato. Il termine carrier sense indica proprio questa operazione di ascolto della portante, cioè del segnale presente sul mezzo trasmissivo. Se il canale risulta libero, l'host tenta la trasmissione; se invece il canale risulta occupato, l'host attende prima di riprovare. Come fa l'host che vorrebbe trasmettere a capire se qualcuno sta già trasmettendo? Semplicemente, esso conosce già la forma della portante (una specie di segnale di base che è sempre presente nel mezzo trasmissivo): se tale forma è modificata, allora significa che qualcuno sta già trasmettendo; diversamente, significa che il canale è libero.

Questa strategia riduce notevolmente il numero di collisioni rispetto ad ALOHA puro e Slotted ALOHA, perché evita che un host trasmetta mentre un altro sta già utilizzando il mezzo. Tuttavia, il CSMA non elimina completamente le collisioni. Infatti, a causa del ritardo di propagazione del segnale, può accadere che due host lontani tra loro verifichino quasi contemporaneamente che il canale è libero e inizino entrambi a trasmettere. In questa situazione la collisione si verifica comunque, anche se con probabilità inferiore rispetto ai protocolli studiati in precedenza.

Esistono diverse politiche con cui un nodo CSMA decide come comportarsi quando trova il canale occupato:

- 1-persistent CSMA: l'host continua ad ascoltare il canale e trasmette immediatamente non appena lo trova libero;
- non-persistent CSMA: l'host, se trova il canale occupato, aspetta un tempo casuale prima di effettuare un nuovo controllo;
- p-persistent CSMA: tipico dei sistemi a slot temporali; quando il canale diventa libero, l'host trasmette con probabilità $p$ e rimanda al successivo slot con probabilità $1 - p$.

La seguente situazione descrive l'idea generale del CSMA:

<!-- to add -->
*In Figura: un host ascolta il canale e trasmette solo quando il mezzo risulta libero*

Il CSMA costituisce la base di due famiglie di protocolli molto importanti, che si differenziano nel modo in cui gestiscono le collisioni residue: CSMA/CD e CSMA/CA.

Il protocollo CSMA/CD (Carrier Sense Multiple Access with Collision Detection) è stato storicamente utilizzato nelle reti Ethernet cablate tradizionali, specialmente quelle basate su bus e hub. In questo caso non basta ascoltare il canale prima di trasmettere: durante la trasmissione, l'host continua anche a monitorare il mezzo per accorgersi se si sta verificando una collisione. Se il nodo rileva una collisione, interrompe immediatamente l'invio del frame, trasmette un apposito segnale di disturbo (jam signal) per informare gli altri nodi dell'evento e poi attende un tempo casuale determinato dal backoff esponenziale prima di ritentare.

Il funzionamento del CSMA/CD può essere riassunto così:

- l'host ascolta il canale;
- se il canale è libero, inizia a trasmettere;
- mentre trasmette, continua a controllare il mezzo;
- se non rileva collisioni, la trasmissione termina con successo;
- se rileva una collisione, interrompe immediatamente la trasmissione, invia il jam signal e applica il backoff esponenziale prima del nuovo tentativo.

Il vantaggio principale del CSMA/CD è che la collisione viene rilevata rapidamente, evitando di sprecare l'intero tempo necessario a trasmettere un frame completo danneggiato. Tuttavia, esso funziona bene soprattutto nei mezzi cablati condivisi, nei quali è tecnicamente possibile trasmettere e ascoltare contemporaneamente il canale. Con l'avvento degli switch Ethernet moderni e delle connessioni full-duplex, le collisioni nelle reti Ethernet locali sono diventate di fatto assenti, per cui il ruolo pratico del CSMA/CD è oggi molto meno centrale rispetto al passato.

Il protocollo CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance), invece, è tipico delle reti wireless, come le reti Wi-Fi. Nelle comunicazioni senza fili è molto difficile, e spesso impossibile, rilevare una collisione mentre si sta trasmettendo: il segnale inviato dal dispositivo è molto più forte di quello che esso potrebbe ricevere nello stesso istante, per cui il nodo non riesce a capire con affidabilità se un altro host stia trasmettendo contemporaneamente. Per questo motivo, nelle reti wireless si preferisce evitare le collisioni, piuttosto che tentare di rilevarle durante la trasmissione.

Nel CSMA/CA il nodo ascolta il canale e, se lo trova libero, non trasmette sempre immediatamente. Spesso attende ancora per un piccolo intervallo di sicurezza e utilizza meccanismi casuali di attesa per ridurre la probabilità che più nodi inizino a trasmettere nello stesso istante. Dopo la trasmissione, il ricevitore invia normalmente un ACK per confermare la corretta ricezione del frame. Se l'ACK non arriva, il mittente presume che si sia verificata una collisione, o un errore, e ritrasmette successivamente. In molte reti wireless si usano anche meccanismi aggiuntivi, come RTS (Request To Send) e CTS (Clear To Send), che analizzeremo nei prossimi paragrafi.

Le differenze essenziali tra CSMA/CD e CSMA/CA possono essere riassunte in questo modo:

- CSMA/CD: ascolta prima di trasmettere e rileva le collisioni durante la trasmissione;
- CSMA/CA: ascolta prima di trasmettere e cerca di prevenire le collisioni prima che esse avvengano;
- CSMA/CD: è adatto soprattutto alle reti cablate condivise;
- CSMA/CA: è adatto soprattutto alle reti wireless.

In sintesi, il CSMA migliora nettamente l'efficienza rispetto ai protocolli ALOHA perché introduce l'ascolto del canale prima dell'invio. Le sue varianti CSMA/CD e CSMA/CA adattano poi questa idea a contesti differenti: il primo è orientato alle reti cablate con possibilità di rilevare direttamente le collisioni, mentre il secondo è pensato per le reti wireless, dove è più realistico tentare di evitarle. Questi protocolli costituiscono la base teorica per comprendere il funzionamento di Ethernet e delle reti Wi-Fi moderne.

### 03.08. Ethernet

Ethernet è lo standard più diffuso per le reti LAN cablate. Le sue principali caratteristiche sono le seguenti:

- utilizza frame come PDU del livello datalink;
- identifica i dispositivi tramite indirizzi MAC a 48 bit;
- è definita principalmente dallo standard IEEE 802.3;
- nasce storicamente come tecnologia a mezzo condiviso con accesso CSMA/CD;
- nelle reti moderne opera quasi sempre con switch e collegamenti point-to-point;
- supporta modalità half-duplex e full-duplex;
- può funzionare su diversi mezzi trasmissivi, come doppino intrecciato, fibra ottica e, storicamente, cavo coassiale;
- supporta velocità di trasmissione molto differenti, ad esempio 10 Mbps, 100 Mbps, 1 Gbps, 10 Gbps e superiori;
- utilizza un campo FCS per il rilevamento degli errori mediante CRC;
- è una tecnologia economica, scalabile e semplice da integrare nelle reti locali;
- costituisce la base di gran parte delle infrastrutture LAN moderne, sia domestiche sia aziendali.

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

Il livello datalink, pur essendo un livello relativamente basso dello stack TCP/IP, è soggetto a numerose problematiche di sicurezza. Storicamente, infatti, i protocolli del livello datalink sono stati progettati ponendo l'attenzione principalmente sull'efficienza e sull'affidabilità della comunicazione, trascurando in larga parte gli aspetti di sicurezza. Questo ha portato, nel corso degli anni, alla scoperta di numerose vulnerabilità che possono essere sfruttate da attaccanti malintenzionati per compromettere la riservatezza, l'integrità e la disponibilità dei dati scambiati nella rete locale. In questo paragrafo analizzeremo le principali problematiche di sicurezza del livello datalink, partendo dalle vulnerabilità intrinseche di Ethernet e proseguendo con alcuni dei più noti attacchi che possono essere messi in atto a questo livello, come il MAC spoofing, l'ARP spoofing ed il VLAN hopping. Concluderemo, infine, parlando del protocollo WPA, utilizzato per proteggere le comunicazioni nelle reti wireless.

##### 03.10.01. Problematiche di Ethernet

Ethernet è, senza ombra di dubbio, lo standard più diffuso al mondo per le reti LAN cablate. La sua semplicità, la sua efficienza ed il suo costo contenuto lo hanno reso lo standard de facto per il collegamento di host all'interno di reti locali, sia in ambito domestico, sia in ambito aziendale. Tuttavia, Ethernet presenta alcune problematiche di sicurezza intrinseche, dovute principalmente al modo in cui è stato progettato:

- Assenza di cifratura nativa: i frame Ethernet vengono trasmessi in chiaro sul mezzo trasmissivo, senza alcuna forma di cifratura. Questo significa che chiunque abbia accesso fisico al mezzo trasmissivo (ad esempio collegando un proprio dispositivo a uno switch, oppure intercettando il segnale su un cavo) può leggere il contenuto dei frame trasmessi. Sebbene oggigiorno le reti Ethernet siano basate prevalentemente su switch (che inviano i frame solo al destinatario, riducendo notevolmente la possibilità di sniffing), in passato le reti Ethernet erano basate su hub (dispositivi che ripetono il segnale su tutte le porte), rendendo banale l'intercettazione del traffico.
- Assenza di autenticazione: i frame Ethernet non prevedono alcuna forma di autenticazione del mittente. Questo significa che un host malintenzionato può facilmente falsificare il proprio indirizzo MAC (MAC spoofing, vedremo a breve) e fingersi un altro host della rete, ingannando gli altri dispositivi.
- Vulnerabilità a livello di switch: gli switch Ethernet mantengono una tabella, detta MAC address table (o CAM table, da Content Addressable Memory), in cui associano ciascun indirizzo MAC alla porta dello switch a cui è collegato l'host corrispondente. Questa tabella ha una dimensione limitata e può essere saturata da un attaccante che invii un grande numero di frame con indirizzi MAC differenti, costringendo lo switch a comportarsi come un hub (situazione detta MAC flooding, o CAM table overflow), inoltrando i frame su tutte le porte e rendendo possibile lo sniffing del traffico.
- Vulnerabilità a livello di STP (Spanning Tree Protocol): lo STP è un protocollo utilizzato dagli switch per evitare la formazione di loop nella topologia della rete. Un attaccante può inviare appositi messaggi BPDU (Bridge Protocol Data Unit) per manipolare la topologia logica della rete, ad esempio facendo in modo che il proprio dispositivo diventi il root bridge della rete e, di conseguenza, vedendo passare la maggior parte del traffico attraverso di sé.
- Vulnerabilità a livello di DHCP: sebbene il DHCP sia un protocollo del livello applicativo, esso viene spesso utilizzato nelle reti Ethernet per assegnare automaticamente gli indirizzi IP agli host. Un attaccante può attivare un server DHCP malevolo (rogue DHCP server) all'interno della rete, distribuendo configurazioni di rete falsificate (ad esempio impostando il proprio dispositivo come gateway predefinito), riuscendo così a intercettare e/o manipolare il traffico degli altri host.

Queste vulnerabilità intrinseche di Ethernet hanno portato allo sviluppo di numerose contromisure, come ad esempio l'utilizzo di switch managed che supportano funzionalità di sicurezza avanzate (port security, DHCP snooping, dynamic ARP inspection, BPDU guard, ecc.), oppure l'utilizzo di VLAN per segmentare la rete e ridurre la superficie d'attacco.

##### 03.10.02. MAC spoofing

Il MAC spoofing è una tecnica con cui un attaccante modifica l'indirizzo MAC della propria scheda di rete in modo da fingersi un altro host della rete. Come abbiamo visto nel paragrafo 03.03.01, l'indirizzo MAC è teoricamente un identificativo univoco a livello mondiale di una scheda di rete. Tuttavia, nella pratica, l'indirizzo MAC può essere modificato in modo molto semplice via software, in quanto non c'è alcun meccanismo hardware che impedisca tale operazione. La maggior parte dei sistemi operativi moderni (Linux, macOS, Windows, ecc.) consente di modificare l'indirizzo MAC di una scheda di rete in pochi semplici passaggi.

Gli scopi del MAC spoofing possono essere molteplici, e non sono sempre malevoli. Alcuni esempi di utilizzo legittimo del MAC spoofing sono i seguenti:

- Aggirare restrizioni basate sull'indirizzo MAC: alcuni provider di servizi Internet (ISP) associano la connessione a un indirizzo MAC specifico (ad esempio quello del router fornito in comodato). Sostituendo il router con uno proprio, è necessario impostare lo stesso indirizzo MAC del router originale per mantenere la connessione attiva.
- Garantire la privacy: alcuni sistemi operativi (come iOS e Android) consentono di utilizzare un indirizzo MAC casuale quando ci si collega a una rete Wi-Fi, in modo da impedire il tracciamento degli utenti basato sull'indirizzo MAC.

Tuttavia, il MAC spoofing può essere utilizzato anche per scopi malevoli, come ad esempio:

- Aggirare l'autenticazione basata sull'indirizzo MAC: alcuni sistemi di controllo dell'accesso alla rete (NAC, Network Access Control) si basano sull'indirizzo MAC per autenticare gli host. Un attaccante che riesca a scoprire l'indirizzo MAC di un host autorizzato (ad esempio attraverso lo sniffing del traffico) può falsificare il proprio indirizzo MAC e fingersi quell'host, ottenendo accesso alla rete.
- Effettuare attacchi di tipo man-in-the-middle: combinando il MAC spoofing con altre tecniche (come l'ARP spoofing, vedremo a breve), un attaccante può intercettare il traffico tra due host della rete, leggendolo, modificandolo, oppure bloccandolo.
- Effettuare attacchi di tipo denial of service: un attaccante può falsificare il proprio indirizzo MAC per fingersi un host legittimo, causando conflitti di indirizzi e impedendo all'host legittimo di comunicare correttamente nella rete.

Per mitigare il MAC spoofing, è possibile utilizzare diverse contromisure, come ad esempio la port security sugli switch managed (che consente di limitare il numero di indirizzi MAC associabili a una determinata porta dello switch), oppure l'utilizzo di sistemi di autenticazione più robusti basati su standard come 802.1X (che prevede l'autenticazione dell'host tramite credenziali, certificati digitali, o altri meccanismi).

##### 03.10.03. ARP spoofing

L'ARP spoofing (detto anche ARP poisoning, o ARP cache poisoning) è uno degli attacchi più noti e più diffusi a livello datalink. Per comprenderlo, è necessario prima fare un breve cenno al protocollo ARP (Address Resolution Protocol), che verrà comunque trattato più nel dettaglio nel capitolo successivo, dedicato al livello network. Il protocollo ARP è utilizzato per associare un indirizzo IP (utilizzato dal livello network) a un indirizzo MAC (utilizzato dal livello datalink) all'interno di una rete locale. Quando un host vuole inviare un pacchetto a un altro host della stessa rete locale, conosce l'indirizzo IP del destinatario, ma non il suo indirizzo MAC. Per scoprirlo, invia un messaggio ARP request in broadcast a tutti gli host della rete, chiedendo: "Chi ha l'indirizzo IP X.X.X.X? Mi dica il suo indirizzo MAC". L'host che ha quell'indirizzo IP risponde con un messaggio ARP reply, contenente il proprio indirizzo MAC. A questo punto, il mittente può inviare il pacchetto al destinatario. Per ottimizzare le prestazioni, ciascun host mantiene una cache locale (detta ARP cache, o ARP table) in cui memorizza le associazioni IP-MAC degli altri host con cui ha comunicato di recente.

Il problema del protocollo ARP è che non prevede alcuna forma di autenticazione. Qualsiasi host della rete può inviare un messaggio ARP reply, anche se non è stato richiesto, e gli altri host lo accetteranno come valido, aggiornando la propria ARP cache. Questo apre la strada all'attacco di ARP spoofing, che funziona nel seguente modo:

1. L'attaccante invia messaggi ARP reply falsificati ai due host che vuole attaccare (ad esempio un host vittima ed il gateway della rete). Nei messaggi falsificati, l'attaccante associa il proprio indirizzo MAC all'indirizzo IP dell'altro host. Ad esempio, all'host vittima invia un messaggio che dice: "L'indirizzo IP del gateway è associato al mio indirizzo MAC". Al gateway, invece, invia un messaggio che dice: "L'indirizzo IP della vittima è associato al mio indirizzo MAC".
2. I due host, ricevendo i messaggi ARP reply falsificati, aggiornano la propria ARP cache con le associazioni errate.
3. Da questo momento in poi, tutto il traffico tra l'host vittima ed il gateway passerà attraverso l'attaccante, che potrà leggerlo, modificarlo, oppure bloccarlo a piacimento. Si tratta di un classico attacco di tipo man-in-the-middle.

L'attacco di ARP spoofing è particolarmente pericoloso perché è molto semplice da realizzare (esistono numerosi tool open source, come Ettercap, Bettercap, o arpspoof, che lo automatizzano completamente) ed è difficile da rilevare per un utente comune. Inoltre, può essere utilizzato come base per attacchi più sofisticati, come ad esempio il DNS spoofing, l'intercettazione di credenziali di accesso, o la sostituzione di contenuti web.

Per mitigare l'ARP spoofing, è possibile utilizzare diverse contromisure, come ad esempio:

- ARP statico: configurare manualmente le associazioni IP-MAC nella ARP cache degli host, in modo che non possano essere modificate dai messaggi ARP reply ricevuti dalla rete. Questa soluzione è efficace, ma poco scalabile e di difficile gestione in reti di grandi dimensioni.
- Dynamic ARP Inspection (DAI): funzionalità disponibile sugli switch managed che ispeziona i messaggi ARP in transito sulla rete e blocca quelli che non corrispondono a una mappatura IP-MAC valida (basata, ad esempio, sulle informazioni fornite dal DHCP snooping).
- Utilizzo di software di rilevamento dell'ARP spoofing: esistono diversi tool (come ArpWatch, XArp, ecc.) che monitorano la rete e rilevano eventuali anomalie nelle associazioni IP-MAC, segnalandole all'amministratore di rete.
- Utilizzo di protocolli sicuri: anche se l'ARP spoofing non può essere completamente prevenuto a livello datalink, l'utilizzo di protocolli sicuri ai livelli superiori (come HTTPS, SSH, VPN, ecc.) consente di proteggere la riservatezza e l'integrità dei dati scambiati, anche in presenza di un attaccante che intercetti il traffico.

##### 03.10.04. VLAN hopping

Le VLAN (Virtual LAN) sono una tecnologia che consente di segmentare logicamente una rete LAN fisica in più reti LAN virtuali, ciascuna delle quali costituisce un dominio di broadcast separato. Le VLAN sono ampiamente utilizzate nelle reti aziendali per separare il traffico di diversi dipartimenti, di diversi gruppi di utenti, o di diversi servizi, migliorando sia la sicurezza, sia le prestazioni della rete. Ad esempio, è comune avere una VLAN dedicata al personale amministrativo, una VLAN dedicata agli ospiti, una VLAN dedicata ai server, e così via. Gli host appartenenti a VLAN differenti non possono comunicare direttamente tra loro a livello datalink: per farlo, devono passare attraverso un router (o uno switch layer 3) che effettua il routing tra le VLAN.

Il VLAN hopping è un attacco con cui un attaccante riesce a inviare traffico a una VLAN diversa da quella a cui è effettivamente assegnato, aggirando le restrizioni imposte dalla segmentazione VLAN. Esistono due principali varianti dell'attacco di VLAN hopping:

- Switch spoofing: in questa variante, l'attaccante configura il proprio dispositivo in modo da fingersi uno switch, sfruttando il protocollo DTP (Dynamic Trunking Protocol) utilizzato dagli switch Cisco per negoziare automaticamente le trunk link (collegamenti tra switch che trasportano traffico di più VLAN). Se la porta dello switch a cui è collegato l'attaccante è configurata in modalità auto, o desirable (modalità di default su molti switch Cisco), l'attaccante può negoziare con successo una trunk link e ricevere, quindi, il traffico di tutte le VLAN configurate sullo switch. Per mitigare questo attacco, è sufficiente disabilitare il DTP sulle porte degli utenti finali e configurarle esplicitamente in modalità access (ovvero come porte appartenenti a una singola VLAN).
- Double tagging: in questa variante, l'attaccante sfrutta il modo in cui gli switch gestiscono i tag VLAN nei frame Ethernet (standard 802.1Q). L'attaccante invia un frame con due tag VLAN: il primo tag corrisponde alla VLAN nativa del trunk link (ovvero la VLAN i cui frame vengono trasmessi senza tag sul trunk link), mentre il secondo tag corrisponde alla VLAN di destinazione dell'attacco. Quando il frame raggiunge il primo switch, quest'ultimo rimuove il primo tag (perché corrisponde alla VLAN nativa) e inoltra il frame sul trunk link. Quando il frame raggiunge il secondo switch, quest'ultimo legge il secondo tag e inoltra il frame alla VLAN di destinazione, anche se l'attaccante non appartiene a quella VLAN. Per mitigare questo attacco, è possibile utilizzare diverse contromisure, come ad esempio configurare la VLAN nativa del trunk link in modo che sia una VLAN dedicata e non utilizzata da alcun host, oppure abilitare la funzionalità di tagging esplicito anche per i frame della VLAN nativa.

Il VLAN hopping è un attacco particolarmente insidioso perché consente all'attaccante di aggirare la segmentazione della rete, accedendo a risorse che dovrebbero essere protette. Per questo motivo, è fondamentale configurare correttamente gli switch e seguire le best practice di sicurezza per le VLAN, come ad esempio: disabilitare il DTP sulle porte degli utenti finali, utilizzare una VLAN nativa dedicata, disabilitare le porte non utilizzate, configurare la port security, ecc.

##### 03.10.05. WPA (Wi-Fi Protected Access)

Le reti wireless, come abbiamo visto nel paragrafo 03.09, sono particolarmente esposte a problematiche di sicurezza, in quanto il mezzo trasmissivo (l'aria) è condiviso e chiunque si trovi nel raggio di copertura della rete può potenzialmente intercettare il segnale. Per questo motivo, è fondamentale utilizzare protocolli di sicurezza che garantiscano la riservatezza, l'integrità e l'autenticazione delle comunicazioni wireless. Il primo protocollo di sicurezza utilizzato nelle reti Wi-Fi è stato il WEP (Wired Equivalent Privacy), introdotto nel 1997 insieme allo standard 802.11. Tuttavia, il WEP si è rivelato fin da subito molto debole, a causa di numerose vulnerabilità nel suo design (ad esempio l'utilizzo di un vettore di inizializzazione troppo corto per l'algoritmo di cifratura RC4, che consente di recuperare la chiave di cifratura analizzando un sufficiente numero di frame). Oggigiorno il WEP è considerato completamente insicuro e non deve essere utilizzato.

Per superare le vulnerabilità del WEP, la Wi-Fi Alliance ha introdotto nel 2003 il protocollo WPA (Wi-Fi Protected Access), che ha rappresentato un significativo passo avanti in termini di sicurezza. Il WPA è stato progettato per essere compatibile con l'hardware esistente (in modo da poter essere implementato come aggiornamento firmware sui dispositivi già in uso) e introduce diverse migliorie rispetto al WEP, tra cui:

- TKIP (Temporal Key Integrity Protocol): un protocollo di gestione delle chiavi che genera dinamicamente una nuova chiave di cifratura per ciascun frame, eliminando il problema della chiave statica del WEP. Inoltre, TKIP utilizza un vettore di inizializzazione di 48 bit (rispetto ai 24 bit del WEP), riducendo la probabilità di collisioni.
- MIC (Message Integrity Check): un codice di controllo dell'integrità del messaggio (detto anche Michael) che protegge i frame da modifiche non autorizzate, sostituendo il debole CRC-32 del WEP.
- Autenticazione robusta: il WPA supporta due modalità di autenticazione: WPA-Personal (detta anche WPA-PSK, Pre-Shared Key), in cui tutti gli host condividono una chiave segreta comune; e WPA-Enterprise, in cui ciascun host si autentica utilizzando credenziali individuali (ad esempio username e password, o certificati digitali) tramite un server RADIUS (Remote Authentication Dial-In User Service) e il protocollo 802.1X.

Tuttavia, anche il WPA ha mostrato nel tempo alcune vulnerabilità (in particolare il TKIP, che pur essendo significativamente più sicuro del WEP, presenta comunque debolezze sfruttabili da attaccanti esperti). Per questo motivo, nel 2004 è stato introdotto il WPA2, basato sullo standard IEEE 802.11i. Il WPA2 sostituisce TKIP con il protocollo CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol), basato sull'algoritmo di cifratura AES (Advanced Encryption Standard) a 128 bit, considerato estremamente sicuro. Come il WPA, anche il WPA2 supporta le due modalità di autenticazione Personal ed Enterprise. Per molti anni il WPA2 è stato considerato lo standard di sicurezza per le reti Wi-Fi, anche se nel 2017 è stata scoperta una vulnerabilità nel meccanismo di handshake a quattro vie (4-way handshake) utilizzato dal WPA2, nota come KRACK (Key Reinstallation Attack), che consente a un attaccante di decifrare il traffico di un host vittima sfruttando la reinstallazione di una chiave già utilizzata.

Per superare le vulnerabilità del WPA2 e fornire un ulteriore livello di sicurezza, nel 2018 la Wi-Fi Alliance ha introdotto il WPA3, l'attuale standard di sicurezza per le reti Wi-Fi. Le principali migliorie introdotte dal WPA3 rispetto al WPA2 sono:

- SAE (Simultaneous Authentication of Equals): un nuovo meccanismo di handshake che sostituisce il 4-way handshake del WPA2, rendendo molto più difficili gli attacchi di tipo dictionary attack (in cui un attaccante prova a indovinare la chiave provando un gran numero di combinazioni) e proteggendo il traffico anche in caso di compromissione della chiave (forward secrecy).
- Cifratura individuale per ciascun host: nelle reti WPA3-Personal, ciascun host utilizza una chiave di cifratura individuale, anche se la chiave segreta condivisa è la stessa per tutti. Questo significa che, anche se un attaccante riuscisse a intercettare il traffico di un host, non sarebbe in grado di decifrare il traffico degli altri host della rete.
- Maggiore protezione per le password deboli: il WPA3 introduce meccanismi che proteggono gli host anche quando vengono utilizzate password deboli, rendendo molto più difficili gli attacchi di tipo brute force.
- WPA3-Enterprise a 192 bit: una modalità di sicurezza avanzata pensata per ambienti che richiedono il massimo livello di protezione (ad esempio enti governativi, militari, o finanziari), basata su algoritmi crittografici a 192 bit.

In sintesi, l'evoluzione dei protocolli di sicurezza wireless (WEP &rarr; WPA &rarr; WPA2 &rarr; WPA3) riflette la continua ricerca di un equilibrio tra sicurezza, prestazioni e compatibilità con l'hardware esistente. Oggigiorno, quando si configura una rete Wi-Fi, è fortemente consigliato utilizzare il WPA3 (se supportato da tutti i dispositivi della rete) o, in alternativa, il WPA2 con AES/CCMP. L'utilizzo del WEP, o del WPA con TKIP, è invece da evitare, in quanto offre un livello di sicurezza del tutto inadeguato per gli standard moderni.