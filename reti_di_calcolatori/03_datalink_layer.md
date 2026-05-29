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
<!-- to do -->

##### 03.02.01. Connessione ACK (ACKnowledge) e connessione UNACK (UNACKnowledge)
<!-- to do -->

##### 03.02.02. Servizio connectionless senza ACK
<!-- to do -->

##### 03.02.03. Servizio connectionless con ACK
<!-- to do -->

##### 03.02.04. Servizio connection-oriented con ACK
<!-- to do -->

### 03.03. Frame
<!-- to do -->

##### 03.03.01. Struttura generale di un frame
<!-- to do -->

##### 03.03.02. Header e trailer di un frame
<!-- to do -->

##### 03.03.02. Tecniche di framing
<!-- to do - byte count (o character count) -->
<!-- to do - byte stuffing -->
<!-- to do - bit stuffing -->
<!-- to do - fixed-size framing -->
<!-- to do - violazione del physical layer -->

##### 03.03.03. Sincronizzazione del frame
<!-- to do -->

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

##### 03.07.01. NIC (Network Interface Card)
 <!-- to do -->

##### 03.07.02. Indirizzi MAC (Media Access Control)
<!-- to do -->

##### 03.07.03. ALOHA puro
<!-- to do -->

##### 03.07.04. Slotted ALOHA
<!-- to do -->

##### 03.07.05. CSMA (Carrier Sense Multiple Access)
<!-- to do -->

##### 03.07.06. CSMA/CD (Carrier Sense Multiple Access with Collision Detection)
<!-- to do -->

##### 03.07.07. Backoff esponenziale
<!-- to do -->

##### 03.07.08. CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)
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