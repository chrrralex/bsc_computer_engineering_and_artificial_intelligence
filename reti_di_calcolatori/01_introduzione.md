# 01. Introduzione

### 01.01. Che cosa è una rete di calcolatori?
Una rete di calcolatori (computer network) è un insieme di dispositivi di elaborazione digitale opportunamente interconnessi. I nodi della rete, detti anche sistemi finali (end systems, o hosts), sono utilizzati da utenti e aziende per eseguire programmi, o erogare servizi. I nodi della rete possono essere di vario tipo: dagli smartphone utilizzati dagli adolescenti durante la lezione di matematica, passando per i personal computer risiedenti nella propria abitazione, ai server di fascia alta posseduti dalle grandi aziende (le cosiddette "big tech") per erogare tantissimi servizi ai propri utenti. Ciascun nodo è connesso mediante un apposito mezzo di comunicazione (o canale di comunicazione, o communication link): esso può essere fisico, come la fibra ottica, oppure può essere non fisico e sfruttare le onde elettromagnetiche (come le frequenze radio, o infrarosse). Una rete è la somma dei nodi e dei collegamenti e possiamo riassumere tutto quanto appena detto con una semplice formula:

```
Network = Nodes + Links
```

### 01.02. Internet
La rete Internet è l'insieme di tutte le reti di computer accessibili dal mondo esterno ed interconnesse tra loro mediante appositi mezzi di comunicazione. Internet è la rete più grande esistente oggi, nonché la rete più vasta (sia per estensione geografica, sia per quantità di dispositivi) mai creata dall'essere umano. Si può dire che Internet ricopre il mondo intero. La rete Internet si può rappresentare come tante circonferenze, ognuna di una certa grandezza, collegate tra loro mediante appositi mezzi trasmissivi, come viene presentato nella seguente figura:

<!-- to add -->
*In Figura: la rete Iternet come la intendiamo oggi, ossia come un insieme di reti (i cerchi) tutti collegati tra loro (linee)*

### 01.03. Network edges e cores
Una rete è costituita da due porzioni principali:

- Network edge (i "bordi" della rete): costituita dagli host, ove ciascuno esegue una, o più applicazioni di rete, come i browser web ed i client per accedere all'email. Qui si parla della grande varietà di dispositivi usati dagli utenti: smartwatch, smartphone, tablet, dispositivi palmari, computer laptop e personal computer sono solo alcuni dei vari tipi di dispositivi connessi ad Internet oggi.
- Network core (il "cuore" della rete): cotituita dai dispositivi che gestiscono le varie comunicazioni tra più dispositivi all'interno della rete, o tra reti differenti. Qui parliamo di switch, hub, router e molti altri dispositivi che hanno il compito di instradare e gestire le comunicazioni.

La seguente figura mostra graficamente la differenza tra network edges e network cores:

<!-- to add -->
*In Figura: come è strutturata una rete di calcolatori, composta da "bordi" (network edges) e "nuclei" (network cores)*

### 01.04. Classificazione delle reti

Una prima classificazione delle reti differisce tra:

- Intranet: reti privata interna riservata solo ed esclusivamente a personale abilitato, tipicamente i dipendenti di un'azienda. La gestione delle utente e delle credenziali per effettuare l'accesso è svolta esclusivamente da apposito personale (con appositi ruoli) all'interno dell'azienda.
- Extranet: estensione sicura della internat, in cui oltre ai dipendenti dell'azienda possono accedere anche soggetti esterni (come partner commerciali, stakeholder di progetti, collaboratori, fornitori, o eventualmente dei clienti). Ciascun soggetto dispone di credenziali controllate esclusivamente dall'azienda che mantine la extranet.

Una seconda classificazione ha a che fare con l'estensione geografica della rete. Avremo, quindi, le seguenti tipologie di reti di calcolatori:

- PAN (Personal Area Network): reti molto piccole e costruite ad hoc (come gi auricolari collegati tramite Bluetooth al proprio cellulare) che risiedono nell'area personale. Anche Zigbee è un esempio di rete personale. Questo tipo di reti si estendono per pochissimo spazio, raramente oltre la decina di metri.
- LAN (Local Area Network): reti che coprono al massimo un edificio, o un campus. Le scuole e le sedi di un'azienda sono esempi perfetti per questo tipo di rete. I dispositivi della rete sono collegati attraverso un server, o un host centrale (come uno switch).
- MAN (Metropolitan Area Network): reti che ricoprono un'intera area urbana, dal piccolo paese in montagna, fino alla grande città nelle vicinanze di una costa. Una rete MAN può avere centinaia, o addirittura migliaia di reti LAN.
- WAN (Wide Area Network): si estende su distanze molto maggiori, occupandosi di collegare intere città di diverse regioni, o nazioni, oppure diverse nazioni. Una WAN può anche interessare due continenti differenti. Le reti WAN racchiudono tantissime reti MAN e LAN.
- GAN (Global Area Network): si tratta di Internet, ovvero la rete globale che ogni giorno produce tantissimi dati ed è costantemente attiva. La GAN ha a che fare con infrastrutture satellitari e addirittura sottomarine ed ha una copertura globale.

Un terzo modo di classificare le reti di calcolatori è osservare il modo in cui i singoli host della rete sono collegati:

- Point-to-point: in cui si ha una "linea" di dispositivi collegati tra loro punto per punto. Il primo dispositivo è collegato solo al secondo. Il secondo e il penultimo dispositivo sono collegati al prissimo, ma anche al precedente. L'ultimo dispositivo è collegato solo al precedente. Se un host vuole inviare un messaggio, il messaggio deve passare anche tra gli host posti in mezzo ai due dispositivi in comunicazione. Tutto ciò genera molta latenza, in quanto il messaggio deve essere elaborato da più host (a meno ché non siano adiacenti).
- Bus: un singolo bus pone in comunicazione tutti gli host della rete. Questo genera, solitamente, un elevato traffico, specialmente nel caso in cui molti host vogliono comunicare. Inoltre, nella topologia a bus è particolarmente importante l'accesso al canale: cosa succede se due, o più host cercano di inviare un segnale sul mezzo trasmissivo contemporaneamente? Accade una collisione. Se si rompe un collegamento, ne risente l'intera rete.
- Ring: in cui tutti i dispositivi sono collegati al successivo e al precedente, formando un anello di comunicazione chiuso. Dal punto di vista concettuale, è molto simile alla topologia point-to-point: la differenza è che ciascun host può comunicare solo quando "è il suo turno" (vedremo meglio che cosa vuol dire questa espressione). Se un collegamento si guasta, l'intera rete è compromessa, o parzialmente compromessa.
- Tree: costituita da un dispositivo root (tipicamente uno switch, o un router che si occupa di instradare le comunicazioni) e i vari host possono essere le foglie dell'albero, oppure a loro volta altri nodi radice da cui si diramano altre strade. Solitamente questa topologia viene preferita quando si vuole introdurre una gerarchia di reti LAN (come all'interno di una sede aziendale). Ha lo svantaggio di richiedere più host intermedi (come switch, hub e router), il ché si traduce in costi generalmente maggiori. Tuttavia, è molto robusta, in quanto se il collegamento si rompe, il resto della rete può continuare a funzionare correttamente.
- Mesh: detta completa se ogni nodo della rete è collegato a tutti gli altri nodi della rete; altrimenti è detta parziale. La mesh completa è la topologia più sicura e robusta in assoluto, mentre la mesh parziale non lo è per niente. La topologia mesh è, infatti, basata sui collegamenti ridondanti: se un collegamento tra due host si rompe, il messaggio può seguire un altro percorso. Questo si traduce in costi maggiori sia per attivare gli altri percorsi, sia per organizzare e progettare la rete nel modo più fault tolerance possibile.

La seguente figura mostra le varie tipologie di una rete di computer:

<!-- to add -->
*In Figura: la classificazione delle reti per mezzo della topologia*

### 01.05. Protocolli e standard

Un protocollo è un insieme di regole ben definite e concordate da ambedue le parti, all'interno di una comunicazione, che definiscono:

- il formato del messaggio;
- l'ordine con il quale devono essere scambiati, o inviati i messaggi;
- le azioni che devono essere intraprese in determinate casistiche.

Un protocollo stabilisce, in pratica, il modo in cui due, o più host della rete possono comunicare. Per esempio, un possibile esempio di protocollo è rappresentato nella seguente figura:

<!-- to add -->
*In Figura: un esempio di protocollo che permette a due host di una rete di comunicare*

Il protocollo prevede:

1. Che il mittente richieda l'apertura di una connessione mediante un messaggio del tipo `CONNECTION_REQUEST`.
2. Che il destinatario, se è tutto pronto, apra la connessione e restituisca un messaggio del tipo `CONNECTION_OK`.
3. Che il mittente invii una richiesta di elaborazione con un messaggio del tipo `REQUEST_DATA`.
4. Che il destinatario, dopo aver ricevuto ed elaborato i dati, restituisca un messaggio del tipo `SEND_DATA`.

Si tratta di un esempio molto semplice, ma la struttura di una comunicazione è questa nelle moderne reti di calcolatori. Da notare come, nella figura, la comunicazione avviene nel corso del tempo: le freccie inclinate e le due linee frapposte tra host mittente e host destinatario rappresentano lo scorrere del tempo. L'IP (Internet Protocol) e il TCP (Transfer Control Protocol) sono due esempi di protocolli molto famosi ed utilizzati nell'ordierna Internet.

Uno standard è un insieme di scelte ufficiali e soprattutto effettuate da organizzazioni internazionali (che si occupano appositamente di reti e telecomunicazioni) che delinano i protocolli da utilizzare all'interno di una comunicazione.

Standard e protocolli sono in stretto rapporto tra loro ed ognuno di essi cerca di delinare tutti gli aspetti tecnici utili per raggiungere effiicenza, prestazioni, affidabilità e sicurezza maggiori. 

### 01.06. Il layered model

Il layered model (modello a strati, o a livelli) è un tipo di modello costituito da una pila di strati posti l'uno sopra l'altro, in cui la comunicazione può avvenire dallo strato più alto a quello più basso (top-to-down communication), o viceversa, dallo strato più basso a quello più alto (down-to-top communication). Caiscuno strato rappresenta un livello d'astrazione ben preciso: lo strato N accetta i servizi forniti sia dallo strato soprastante N + 1, sia dallo statro sottostante N - 1. Analogamente, lo strato N fornisce servizi in modo diretto agli strati N + 1 e N - 1 e in modo indiretto a tutti gli altri strati della pila. Ciò che, nell'ambito delle reti di calcolatori, rappresenta un determinato layer è un protocollo, oppure un insieme di protocolli. La comunicazione in Internet ha stabilito due layered model molto importanti dal punto di vista didattico e tecnico: il modello OSI ed il modello TCP/IP.

Lo stack di protocolli TCP/IP, il cui nome deriva dai due protocolli "principe" TCP (Transfer Control Protcol) e IP (Internet Protocol) della pila stessa rappresenta un vero e proprio standard de-facto delle reti di calcolatori e consiste in cinque livelli, numerati da 1 a 5. Lo stack TCP/IP è rappresentato di seguito:

<!-- to add -->
*In Figura: lo stack TCP/IP con i suoi cinque livelli, numerati da 1 a 5*

- Layer 1: il physical layer si occupa della trasmissione di un segnale da un host a un altro. Esso è costituito dal vero e proprio mezzo trasmissivo che, dal punto di vista fisico, trasmette bit per bit dal mittente al destinatario. Diciamo che si occupa di "spostare" i bit in un collegamento punto-a-punto.
- Layer 2: il datalink layer si occupa di gestire gli errori di trasmissione di un'intero messaggio trasmesso nell'ambito di un collegamento punto-a-punto. In realtà il datalink layer ha anche a che fare con l'indirizzo MAC (Media Access Control) del dispositivo fisico, ovvero della NIC (Network Interface Card). Inoltre governa le politiche per accedere al canale di comunicazione, andando a occuparsi di tematiche importanti come reti Ethernet e Token Ring, di cui parleremo ampiamente in seguito.
- Layer 3: ed ecco il network layer, forse il livello più noto di tutti. Esso utilizza degli host intermedi chiamat router per instradare il messaggio tra reti diverse. In questo livello si affrontano tutti i problemi legati al routing ed alla comunicazione tra due reti differenti. Il protocollo IP è di gran lunga quello più usato nel network layer.
- Layer 4: il transport layer gestisce l'intera comunicazine, vista come un flusso di bit, o di Byte da un dispositivo all'interno di una determinata rete a un altro dispositivo che risiede in un'altra rete, differente e magari completamente lontana. Qui è il protocollo TCP a governare. Spesso qui lavorano i programmatori di applicazioni.
- Layer 5: l'application layer presenta i dati all'utente e gli consentete di stabilire connessioni e comunicazioni ad altissimo livello. In pratica l'utente non ha la minima idea di tutti i dettagli implementativi e dell'infrastruttura di rete sottostante a questo livello. I programmatori di applicazioni (come microservizi, backend e molto altro) lavorano soprattutto in questo livello.

Infine, presentiamo di seguito il modello ISO/OSI (International Standardization for Organization / Open System Interconnect). Si tratta di un modello creato e proposto dalla ISO, un'ente internazionale che si occupa di emanare e gestire standard. Si tratta però di un modello difficile da implementare nella pratica e, sopratuttto, datato per via delle nuove emergenti tecnologie che non erano ancora state commercializzate quando il modello OSI venne proposto. Ad ogni modo, lo stack di protocolli TCP/IP deriva direttamente dallo stack di protocolli OSI, che è di seguito rappresentato con i suoi 7 livelli, numerati da 1 a 7:

<!-- to add -->
*In Figura: lo stack di protocolli ISO/OSI con i suoi 7 livelli*

Esistono vari modi per analizzare lo stack di protocolli TCP/IP. L'approccio bottom-up prevede di analizzare prima i livelli più bassi e, man mano che si va avanti, diminuire la complessità analizzando via via PDU e servizi relativamente più semplici, in quanto più orientati all'utente. Una seconda modalità prevede di utilizzare l'approccio top-down, in cui si parte dal layer didatticamente più semplice, l'application layer, per poi man mano passare ai livelli inferiore ed aumentare gradualmente la complessità. Entrambi gli approcci sono molto validi ed hanno pro e contro. Noi seguiremo un approccio bottom-up.


### 01.07. La PDU
Un messaggio all'interno di un determinato layer viene genericamente detto PDU (Protocol Data Unit, unità di dati del protocollo), anche se si sente spesso il termine packet (pacchetto). Man man che dal livello di applicazione si passa ai livelli sottostanti, i dati che un host mittente vuole trasmettere a un host destinatario vengono decorati da informazioni aggiuntive. Per esempio, il livello application dello stack TCP/IP consiste nei dati puri e semplici che si devono trasmettere, ma quando si passa la PDU del livello application al livello transport, quest'ultimo aggiunge una serie di informazioni (tra cui la porta dei servizi posti in comunicazione di mittente e destinatario), di fatto ottenendo una PDU con più dati. Questi ultimi dati sono utili solo ed esclusivamente al transport layer. Analogamente, quando il transport layer consegna la sua PDU al network layer, quest'ultimo aggiunge alcune altre informazioni utili per i router (tra cui indirizzi IP di mittente e destinazione). Infine, quando il network layer consegna la PDU al datalink layer, quest'ultimo aggiunge gli indirizzi MAC dei dispositivi mittente e destinatario. In realtà le informazioni dette prima non sono le uniche ad essere aggiunte, bensì ne vengono aggiunte molte altre in realazione ai servizi che può offrire ciascun livello. La seguente figura mostra quanto appena detto per lo stack TCP/IP:

<!-- to add -->
*In Figura: il modo in cui la PDU di ciascun layer viene dettagliata con informazioni utili per ciascun livello*

La comunicazione tra due host può non consistere per forza in tutti i livelli. Per esempio, due router appartenenti a due reti differenti possono tranquillamente dialogare solo fino a livello network (e, nell'effettiva pratica, è esattamente così che funzionano): a loro non interessa conoscere le porte a cui stanno comunicando due servizi presenti in mittente e destinatario, ma solo i relativi indirizzi IP per comprendere come instradare il pacchetto attraverso la rete. In generale, ciascun host della rete considera solo lo stack fino a quale è interessato a dover operare. Ecco che, ad esempio:

- Un router opererà fino al livello network.
- Uno switch opererà fino al livello datalink.
- Un hub opererà fino al livello datalink.
- Un programma browser web in un host dell'utente opererà fino al livello application.
- Uno script Python che sfrutta il protocollo TCP in esecuzione su una macchina può operare, a seconda del caso, fino al livello transport, o fino al livello application.

La PDU a livello application è genericamente detta data, quella a livello transport è detta segment (o datagram), a livello network è detta packet, a livello datalink è chiamata frame e, infine, nel livello physical si hanno i bit, o signals. Quando una PDU passa dal un layer inferiore a un layer superiore, si dice che essa viene decapsulata (o estratta) dalla PDU del livello sottostante. Viceversa, quando una PDU passa dal layer superiore al layer inferiore, si dice che essa viene incapsulata (o inserita) nella PDU del livello sottostante.

La PDU viene incapsulata e deincapsulata tra i livelli. L'host mittente spedisce la PDU, che passa dal livello più alto del layered model al livello più basso: da un passaggio all'altro, la PDU si arricchisce di informazioni relative a quel particolare strato dell'architettura. In pratica l'incapsulamento consiste nel prelevare la PDU del livello superiore ed aggiungere un'intestazione (header) e una terminazione (come un codice d'errore, una guardia, o altro), per ottenre una nuova PDU contenente più informazioni. Il processo di deincpsulazione è l'azione inversa rispetto alla precedente: la PDU passa dal livello più basso a quello più alto. Una PDU che risiede nel livello più basso e passa ad un livello più alto viene sprovvista dell'header e della terminazione del livello più basso. In pratica solo il contenuto "interno" della PDU interessa al livello soprastante. L'ultimo livello dell'architettura ottiene il messaggio puro e semplice che sarà letto ed interpretato direttamente dall'utente finale. I due processi sono rappresentati nella figura seguente:

<!-- to add -->
*In Figura: incapsulamento e deincapsulamento della PDU (Protocol Data Unit)*

### 01.08. Struttura moderna della rete Internet

Un ISP (Internet Service Provider) è un'azenda il cui compito è fornire l'accesso ad Internet ai propri clienti, situati ognuno presso la propria abitazione. Esistono tantissimi tipi di ISP:

- L'ISP di accesso è una cabina, o un insieme di cabine poste nei centri urbani, o comunque vicino alle abitazioni dei clienti e fornisce l'accesso ad Internet ad uno, o più quartieri, o vie.
- L'ISP provinciale è un centralino che collega più ISP d'accesso volto a collegare clienti situati in centri urbani differenti.
- L'ISP regionale è un centralino che collega più ISP d'accesso e/o ISP provinciali, il cui scopo è collegare clienti situati in province differenti (idealmente l'intera regione di un paese).
- L'ISP nazionale è una centrale molto grande a cui convergono tutti gli ISP regionali, provinciali, o d'accesso, il cui obiettivo è collegare tutti i clienti della nazione ad Internet.
- Infine, l'ISP globale: si tratta di una vasta centrale che intercollega tantissimi ISP nazionali, regionali, provinciali, o d'accesso.


Un IXP (Internet eXchange Point) è una struttura fisica dove più reti (ISP, operatori, cloud provider, CDN, aziende) si collegano tra loro per scambiarsi traffico Internet direttamente. Senza un IXP, il traffico tra due reti potrebbe dover passare attraverso operatori intermedi. Con un IXP, le reti possono realizzare ciò che normalmente viene chiamato peering, cioè scambiarsi dati in modo diretto. In pratica un IXP è una grande stanza dove sono allocati più cabine, ognuna di un determinato ISP.

Un PoP (Point of Presence) è un punto di accesso di una rete in una determinata area geografica. In pratica è una sede tecnica dove un operatore installa apparati di rete (router, switch, server, collegamenti in fibra) per fornire connettività ai clienti, o interconnettersi con altre reti. In pratica un PoP permette a un ISP di estendere la propria presenza geografica.

Una CDN (Content Delivery Network) è una rete di server distribuiti geograficamente che serve contenuti agli utenti dal nodo più vicino a loro. L'obiettivo principale è ridurre la latenza, aumentare la velocità di caricamento e diminuire il carico sui server originari. In pratica una CDN è costituita da un insieme di macchine contenenti lo stesso contenuto, oppure una parte di un contenuto più grande e che sono sempre e costantemente pronti a fornirlo agli utenti che ne fanno richiesta.

La seguente figura mostra la moderna struttura della rete Internet:

<!-- to add -->
*In Figura: la struttura moderna di Internet*

### 01.09. Ritardi nelle reti

Ciascun nodo all'interno della rete presente un determinato ritardo. Esistono almeno quattro tipi di ritardi che affliggono la comunicazione tra due, o più host posizionati nella stessa rete, o in reti differenti:

- Processing delay (ritardo di elaborazione): il tempo necessario da parte del nodo della rete per elaborare la PDU arrivata in input. Normalmente è dell'ordine di pochissimi microsecondi, o addirittura nanosecondi.
- Queuing delay (ritardo di accodamento): ciascun nodo intermedio della rete presenta una coda (o buffer) nel quale vengono man mano memorizzati i pacchetti ricevuti in ingresso. Più è grande la coda, maggiore è questo ritardo; meno è grande la coda, minore è questo ritardo. Si tratta di un ritardo molto variabile, che può variare dall'essere nullo fino a qualche decina (e talvolta centinaia) di millisecondi.
- Trasmission delay (ritardo di trasmissione): il tempo impiegato dal nodo per prelevare la PDU dalla propria memoria centrale (o buffer) e trasmetterlo nella corrispettiva interfaccia di uscita. Si tratta di un tempo che dipende dalla lunghezza della PDU stessa, anche se normalmente richiede non più di qualche decina di microsecondi.
- Propagation delay (ritardo di propagazione): sebbene sia spesso confuso con il precedente ritardo (che dipende dalla velocità di trasmissione del nodo e dalla lunghezza della PDU), il ritardo di propagazione dipende solo ed esclusivamente dalle caratteristiche fisiche del mezzo trasmissivo (come la fibra ottica, o il doppino telefonico). Il ritardo di propagazione è dominante quando si parlad i reti di vaste dimensioni e, solitamente, varia da qualche microsecondo a svariate centinaia di millisecondi (come, ad esempio, nel caso delle comunicazioni satellitari).

Interessante è comprendere il peso di ciascun tipo di ritardo nella trasmissione dati. In una LAN che utilizza fibre ottiche, per esempio, il peso del ritardo di propagazione è relativamente minore, nel senso che difficilmente si subiranno ritardi per via della propagazione del segnale, che nelle fibre ottiche è circa la metà della velocità della luce. In pratiga il ritardo $d_{prop}$ è più che trascurabile. Tra due host collegati direttamente, il ritardo di accodamento, $d_{queue}$ è trascurabile, in quanto non vi è alcun host intermedio tra i due dispositivi posti in comunicazione (in questo scenario anche il ritardo di elaborazione $d_{elab}$ è trascurabile). Al contrario, se si considera una reete WAN in cui partecipano attivamente molti router per instradare i pacchetti, allora i ritardi $d_{elab}$ e $d_{queue}$ assumono sicuramente un peso maggiore, così come anche il ritardo di propagazione $d_{prop}$. Bisogna sempre considerare con quale tipo di rete si ha a che fare per comprendere quali possono essere i ritardi dominanti e quali no. In genere, maggiori sono le dimensioni geografiche della rete e gli host coinvolti, maggiore è la latenza (o ritardo) end-to-end che affligge la trasmissione dati tra gli host posit in comunicazione tra loro. Ma il ritardo totale non dipende solo dalla rete, anche dalla dimensione dei pacchetti: maggiore è quest'ultima, maggiore sarà il ritardo di trasmissione $d_{transm}$ e, viceversa, minore sarà la lunghezza del pacchetto, minore sarà $d_{trans}$.

Se si hanno $N - 1$ host intermedi che collegano due host, diciamo A e B, attraverso $N$ mezzi trasmissivi la cui velocità è uniforme, ossia tutti gli $N$ collegamenti hanno un throughput di $R$ bps, possiamo facilmente calcolare il ritardo end-to-end (end-to-end delay) tra A e B, indicato con $d$, si può calcolare nel seguente modo:

$$
d = N (d_{trans​} + d_{prop​}) + (N − 1) (d_{elab} + d_{queue​})
$$

Essendo $N$ i collegamenti, ciascuno di essi ha un proprio ritardo di trasmissione $d_{trans}$ e un ritardo di propagazione $d_{prop}$. Essendo $N - 1$ gli host intermedi tra A e B, ciascuno di essi ha lo stesso ritardo di elaborazione del pacchetto $d_{elab}$ e lo stesso ritardo di accodamento $d_{queue}$. Questa situazione, con collegamenti omogenei, è mostrata nella seguente figura:

<!-- to add -->
*In Figura: end-to-end delay su collegamenti omogenei*

Ovviamente la precedente situazione non è realistica: ciascun mezzo trasmissivo ha il proprio throughput, ovvero i propri ritardi $d_{trans}$ e $d_{prop}$. Analogamente, ciascun dispositivo intermedio ha il proprio hardware, ossia ha il proprio processore e la propria memoria, per cui ha anche i propri ritardi di elaborazione $d_{elab}$ e ritardi di accodamento $d_{queue}$: quest'ultimo, in particolare, dipende anche da quanto è trafficata la rete. Ecco la formula per calcolare il ritardo end-to-end (end-to-end delay) tra gli host A e B in una rete con collegamenti eterogenei:

$$
d = \sum_{i = 1}^{N} (d_{trans_i​} + d_{prop_i​}) + \sum_{i = 1}^{N - 1} (d_{elab_i} + d_{queue_i​})
$$

Le due sommatorie sfruttano l'indice $i$ da $1$ a $N$ (nel caso dei collegamenti), o $N - 1$ (nel caso degli host intermedi) per indicare ciascun ritardo in modo specifico. Immagina di numerare i collegamenti da $1$ a $N$ e gli host intermedi da $1$ a $N - 1$. Questa situazione, con collegamenti eterogenei, è mostrata nella seguente figura:

<!-- to add -->
*In Figura: end-to-end delay su collegamenti eterogenei*

Infine, parliamo dell'indice di intensità di traffico. L'indice di intensità di traffico misura il grado di utilizzo di un collegamento di rete e rappresenta il rapporto tra il traffico offerto e la capacità del collegamento stesso. L'indice di intensità di traffico si indica solitamente con $I$ ed è definito dalla seguente formula:

$$
I = \frac{La}{R}
$$

Analizziamo ciascuna variabile della precedente formula:

- $I$ è l'indice di intensità di traffico.
- $L$ è la lunghezza media del pacchetto (espressa in bit, o suoi multipli).
- $a$ è il tasso medio di arrivo dei pacchetti (si misura in pacchetti arrivati all'host intermedio al secondo).
- $R$ è la velocità di trasmissione del collegamento in uscita espressa in bps (bit per second).

Il prodotto $La$ rappresenta il traffico generato dalla sorgente espresso in bit/s, mentre $R$ rappresenta la capacità del collegamento.

L'indice di intensità di traffico $I$ è fondamentale per comprendere che cosa succederà alla rete:

- $I < 1$: il traffico generato è inferiore alla capacità del collegamento; il sistema è stabile, per cui non ci sarà alcuna congestione.
- $I \approx 1$: il collegamento è vicino alla saturazione. Man mano che $I$ si avvicina a $1$, l'host si avvicina alla saturazione del collegamento.
- $I > 1$: il traffico supera la capacità disponibile. Questo significa che l'host corrente sta avendo una saturazione nel collegamento in ingresso, in quanto i pacchetti arrivano ad un tasso maggiore rispetto a quanto possa elaborare e trasmettere l'host stesso. La coda cresce fino alla saturazione del buffer di ingresso dei pacchetti (un'area della memoria). Si avrà quindi congestione e perdita di pacchetti.

L'andamento del ritardo di accodamento in funzione dell'intensità di traffico mostra una crescita lenta per valori bassi di $I$ e una crescita molto rapida quando $I$ si avvicina a 1. Quando l'intensità di traffico tende a 1, il ritardo di accodamento tende a crescere rapidamente poiché i pacchetti arrivano quasi alla stessa velocità con cui possono essere trasmessi. Questa situazione è rappresentata dal seguente grafico:

<!-- to add -->
*In Figura: grafico dell'indice di intensità di traffico*
