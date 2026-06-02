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
<!-- to do -->

##### 03.04.01. Introduzione agli errori di trasmissione
<!-- to do - cause degli errori nei canali -->
<!-- to do - rumore e interferenze -->
<!-- to do - errori singoli e burst errors -->

##### 03.04.02. EDCs (Error Detection Codes)
<!-- to do - parity bit singolo -->
<!-- to do - parity bit multipli -->
<!-- to do - parity bit bidimensionale -->
<!-- to do - checksum -->
<!-- to do - CRC (Cyclic Redundancy Code) e polinomi generatori -->

##### 03.04.03. ECCs (Error Correction Codes)
<!-- to do - distanza di Hamming -->
<!-- to do - codici di Hamming -->
<!-- to do - FEC (Froward Error Correction) -->
<!-- to do - codici lineari -->
<!-- to do - codici Reed-Solomon -->
<!-- to do - LDPC (Low-Density Parity Check) -->
<!-- to do - codici convoluzionali -->

### 03.05. Controllo del flusso
<!-- to do - introduzione al controllo del flusso -->
<!-- to do - il problema del buffering -->
<!-- to do - il problema del mittente veloce e ricevente lento -->
<!-- to do - il problema del ritardo di propagazione -->
<!-- to do - throughput ed efficienza -->

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