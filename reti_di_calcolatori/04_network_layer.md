# 04. Network Layer

### 04.01. Introduzione

Siamo finalmente giunti al network layer, forse il livello più rappresentativo dello stack TCP/IP. Il livello network è il terzo livello dell'architettura, preceduto dal livello datalink (quello sottostante) e seguito dal livello transport (quello soprastante). Il livello network è di fondamentale importanza per svariati motivi, che riassunti in un'unica parola (o meglio acronimo) indicano: IP (Internet Protocol). In questo capitolo ci addentreremo nelle profondità di questo livello e cercheremo di analizzare tutti gli aspetti di questo livello.

##### 04.01.01. Panoramica del network layer dello stack TCP/IP

Il network layer ha il compito di permettere il trasferimento dei dati tra host che non sono necessariamente collegati in modo diretto. Mentre il livello datalink si occupa della consegna di frame tra due nodi adiacenti sullo stesso collegamento, il livello network si occupa di portare i dati da un host sorgente a un host destinazione anche attraversando molte reti differenti e numerosi dispositivi intermedi, come router e gateway. In generale, il livello network entra in gioco quando i due dispositivi posti in comunicazione risiedono in reti differenti, anche molto lontani (sia dal punto di vista geografico, sia in termini di host -salti- che li separano).

La PDU tipica del livello network nello stack TCP/IP prende il nome di pacchetto IP, o più precisamente datagramma IP. Questo livello costituisce quindi il cuore dell'interconnessione tra reti eterogenee: consente a reti fisiche e logiche differenti di cooperare tra loro, purché tutte siano in grado di trasportare datagrammi IP. È proprio per questo motivo che il network layer è spesso considerato il livello che realizza concretamente l'idea di internetworking, cioè di rete di reti.

Dal punto di vista architetturale, il livello network riceve i segmenti dal livello transport, li incapsula in datagrammi IP e decide come farli avanzare verso la destinazione. Nel nodo destinatario avviene l'operazione opposta: il datagramma viene elaborato, il suo header interpretato e il contenuto consegnato al livello superiore. Nei nodi intermedi, invece, il pacchetto non viene consegnato ai livelli superiori dell'host, ma viene semplicemente esaminato e inoltrato verso il prossimo host intermedio, o verso l'host destinatario.

In questo capitolo analizzeremo quindi il livello network da più punti di vista: il modello di servizio offerto, il routing, la struttura degli indirizzi IP, il controllo del traffico, il QoS (Quality of Service) e i principali protocolli collegati, come ICMP, ARP, DHCP, OSPF e BGP.

##### 04.01.02. Responsabilità e servizi forniti dal network layer

Le responsabilità del network layer sono numerose e riguardano soprattutto la consegna dei dati attraverso reti multiple. Le più importanti sono le seguenti:

- indirizzamento logico degli host mediante indirizzi IP;
- instradamento (routing) dei pacchetti dalla sorgente alla destinazione;
- inoltro (forwarding) dei pacchetti nei router intermedi;
- interconnessione tra reti eterogenee;
- gestione della frammentazione e del riassemblaggio dei pacchetti quando necessario;
- supporto al controllo del traffico e, in alcuni casi, alla qualità del servizio.

Il servizio fondamentale offerto dal livello network consiste quindi nella consegna di un datagramma da un host sorgente a un host destinatario attraverso una rete composta da più sottoreti intermedie. Questo servizio può essere visto come un servizio host-to-host a livello logico, anche se la consegna reale del pacchetto avviene passo dopo passo, da un nodo intermedio al successivo.

È importante osservare che il network layer, nello stack TCP/IP classico, non garantisce di per sé né affidabilità assoluta, né ordine di consegna, né assenza di duplicati. Tali aspetti, quando richiesti, vengono in genere gestiti dal livello transport. Il network layer fornisce invece un servizio più generale e scalabile, orientato principalmente all'instradamento efficiente dei pacchetti su grandi reti interconnesse.

##### 04.01.03. Servizi connectionless e connection-oriented

Anche a livello network è possibile distinguere tra servizi connectionless e servizi connection-oriented. Un servizio connectionless non richiede la creazione preventiva di una connessione logica tra sorgente e destinazione prima dell'invio dei dati. Ogni pacchetto viene trattato come un'unità autonoma e può essere instradato indipendentemente dagli altri. Questo è il modello tipico adottato da IP nello stack TCP/IP ed è anche quello più diffuso nelle reti moderne su larga scala.

Nel servizio connectionless ciascun datagramma contiene tutte le informazioni necessarie per raggiungere il destinatario, in particolare l'indirizzo IP di destinazione. Di conseguenza, pacchetti appartenenti alla stessa comunicazione possono anche seguire percorsi differenti all'interno della rete, arrivare fuori ordine, oppure subire ritardi diversi.

Un servizio connection-oriented, invece, prevede che prima della trasmissione dei dati venga stabilito un percorso logico, o una connessione virtuale, tra i due estremi della comunicazione. Solo dopo questa fase i dati possono iniziare a fluire lungo il cammino stabilito. In questo caso i nodi della rete mantengono alcune informazioni di stato relative alla connessione attiva.

In sintesi:

- il servizio connectionless è più semplice, flessibile e robusto su grandi reti distribuite;
- il servizio connection-oriented permette un controllo maggiore del percorso e delle risorse di rete;
- Internet classica si basa soprattutto su un servizio network di tipo connectionless;
- alcune reti, soprattutto storiche, o specializzate (come certe reti militari), hanno adottato modelli connection-oriented con circuiti virtuali.

##### 04.01.04. Circuit switching (o virtual switching) e packet switching (o datagram switching)

Per comprendere bene il funzionamento del livello network è utile distinguere tra due grandi modelli di comunicazione: circuit switching e packet switching.

Nel circuit switching, prima che la comunicazione abbia inizio, viene stabilito un percorso dedicato tra sorgente e destinazione. Le risorse della rete lungo tale percorso vengono riservate per tutta la durata della comunicazione. Questo modello è tipico delle reti telefoniche tradizionali: quando due utenti comunicano, si crea un circuito logico dedicato che rimane occupato fino al termine della chiamata. Il vantaggio principale è la prevedibilità del servizio, mentre lo svantaggio è lo scarso sfruttamento delle risorse quando il canale resta temporaneamente inutilizzato.

Nel packet switching, invece, i dati vengono suddivisi in pacchetti autonomi che attraversano la rete condividendo dinamicamente le risorse disponibili. Ogni pacchetto può essere memorizzato temporaneamente nei router intermedi, analizzato e inoltrato verso il prossimo nodo. Questo modello è molto più efficiente nell'utilizzo della banda, perché le risorse non vengono riservate in modo esclusivo, ma condivise tra molte comunicazioni concorrenti.

Quando si parla di packet switching si distinguono spesso due casi:

- datagram switching: ogni pacchetto viene instradato in modo indipendente, come avviene in Internet con IP;
- virtual circuit switching: prima della trasmissione si crea un circuito virtuale, ma i dati viaggiano comunque sotto forma di pacchetti.

In sintesi, il circuit switching privilegia continuità e prevedibilità, mentre il packet switching privilegia flessibilità, condivisione delle risorse e scalabilità. Le reti di calcolatori moderne, e Internet in particolare, si basano quasi interamente sul packet switching, perché questo modello si adatta molto meglio al traffico dati, che è tipicamente discontinuo, variabile e distribuito nel tempo.

### 04.02. Routing

Il routing è il processo con cui la rete stabilisce quale percorso debba seguire un pacchetto per andare dalla sorgente alla destinazione. In pratica, i router analizzano le informazioni contenute nei datagrammi e decidono a quale nodo successivo inoltrarli, cercando di raggiungere la destinazione in modo corretto ed efficiente. Nei prossimi paragrafi analizzeremo i principali criteri e algoritmi usati per effettuare questa scelta.

##### 04.02.01. Store-and-forward, cut-through e fragment free

Questi tre termini descrivono modi diversi con cui un dispositivo di rete può gestire l'inoltro di un pacchetto, o di un frame, verso il nodo successivo.

- Store-and-forward: il dispositivo riceve l'intero pacchetto prima di inoltrarlo. Questo metodo è più sicuro, perché permette di controllare meglio eventuali errori e di prendere decisioni di inoltro con tutte le informazioni disponibili, ma introduce un ritardo maggiore.
- Cut-through: il dispositivo inizia a inoltrare il pacchetto non appena legge i primi campi utili dell'header, senza attendere la ricezione completa. In questo modo la latenza diminuisce, ma aumenta il rischio di inoltrare anche dati corrotti.
- Fragment free: rappresenta un compromesso tra i due metodi precedenti. Il dispositivo aspetta di ricevere solo la parte iniziale del pacchetto, sufficiente a ridurre il rischio di propagare collisioni, o errori tipici delle reti condivise, e poi avvia l'inoltro.

In sintesi, store-and-forward privilegia l'affidabilità, cut-through privilegia la velocità, mentre fragment free cerca un compromesso tra controllo ed efficienza.

##### 04.02.02. Percorso minimo e principio di ottimalità

Nel routing, il percorso minimo è il cammino tra un nodo sorgente e un nodo destinatario che minimizza un certo costo. Il termine minimo non significa necessariamente il minor numero di salti: il costo può infatti dipendere da diversi fattori, come ritardo, congestione, larghezza di banda, affidabilità del collegamento, oppure una combinazione di questi elementi. In pratica, un algoritmo di routing cerca spesso il percorso che risulta migliore secondo una metrica scelta.

Il principio di ottimalità afferma che se un router $J$ si trova su un percorso ottimo dal router $I$ al router $K$, allora anche il sottopercorso da $J$ a $K$ deve essere ottimo. In altre parole, un cammino ottimo è formato da sottocammini anch'essi ottimi. Questo principio è molto importante perché costituisce la base teorica di numerosi algoritmi di routing: consente infatti di costruire percorsi minimi globali a partire da decisioni corrette su tratti più piccoli della rete.

Tale principio è meglio rappresentato nella seguente figura:

<!-- to add -->
*In Figura: ecco come possiamo rappresentare il principio di ottimalità*

Da questo principio deriva l'idea che, per una certa destinazione, l'insieme dei percorsi ottimi provenienti dai vari nodi della rete tende a formare una struttura ad albero, che analizzeremo nel prossimo paragrafo con il concetto di sink tree.

##### 04.02.03. Caratteristiche di un algoritmo di routing

Un buon algoritmo di routing deve possedere alcune caratteristiche fondamentali, perché da esse dipendono l'efficienza, la stabilità e l'affidabilità dell'intera rete. In generale, un algoritmo di routing dovrebbe essere:

- corretto, cioè capace di trovare percorsi validi verso le destinazioni;
- semplice, in modo da essere implementabile e gestibile senza eccessiva complessità;
- robusto, cioè capace di continuare a funzionare anche in presenza di guasti, variazioni di topologia ed elevatto traffico nella rete (congestione);
- stabile, evitando cambiamenti continui di percorso che potrebbero peggiorare il traffico;
- efficiente, sia nell'uso della banda sia nel consumo di risorse computazionali da parte dei router, o degli host intermedi della rete;
- equo, cioè capace di distribuire le risorse senza favorire in modo eccessivo alcune comunicazioni a scapito di altre;
- convergente, cioè in grado di raggiungere rapidamente una situazione coerente dopo un cambiamento nella rete.

In pratica, progettare un algoritmo di routing significa trovare un compromesso tra qualità dei percorsi scelti, rapidità di adattamento e costo complessivo della gestione della rete. Nei prossimi paragrafi vedremo diversi algoritmi che realizzano questo compromesso in modi differenti.

##### 04.02.04. Sink tree

Un sink tree è un albero che rappresenta, per una certa destinazione della rete, l'insieme di tutti i percorsi ottimi che i vari nodi possono utilizzare per raggiungerla. Il termine sink indica proprio il nodo destinazione finale verso cui tutti i rami dell'albero convergono. In pratica, fissato un nodo di arrivo, ciascun altro nodo della rete ha un unico cammino ottimo che lo collega a quel nodo: l'unione di tutti questi cammini forma il sink tree.

Questo concetto deriva direttamente dal principio di ottimalità. Se ogni sottopercorso di un cammino ottimo è anch'esso ottimo, allora i percorsi minimi verso una stessa destinazione non si dispongono in modo casuale, ma tendono a organizzarsi in una struttura ad albero. Tale struttura è molto utile perché permette di visualizzare con chiarezza come i pacchetti provenienti da diversi punti della rete possano convergere tutti verso la stessa destinazione seguendo i cammini migliori.

Un sink tree non contiene cicli: se ci fossero cicli, un pacchetto potrebbe continuare a ruotare nella rete senza raggiungere correttamente la destinazione, oppure il percorso non sarebbe più minimo. Per questo motivo il sink tree è una struttura particolarmente adatta a descrivere l'idea dei percorsi minimi verso un singolo nodo.

La seguente figura sarebbe particolarmente utile per comprendere il concetto:

<!-- to add -->
*In Figura: un grafo di rete e, accanto, il sink tree costruito rispetto a un nodo destinazione evidenziato*

Per visualizzarlo meglio, il lettore può immaginare una rete composta da più router collegati tra loro e scegliere uno di essi come destinazione finale: tracciando da ogni altro router solo il percorso ottimo verso tale destinazione, si ottiene appunto il sink tree.

##### 04.02.05. Algoritmo shortest path e Dijkstra

L'algoritmo shortest path ha lo scopo di trovare il percorso di costo minimo tra un nodo sorgente e tutti gli altri nodi della rete. Uno degli algoritmi più noti per risolvere questo problema è l'algoritmo di Dijkstra, utilizzato quando i costi dei collegamenti sono non negativi.

L'idea di base di Dijkstra è costruire progressivamente l'insieme dei nodi per i quali il costo minimo dalla sorgente è già noto con certezza. All'inizio si conosce solo il costo del nodo sorgente, che è pari a 0, mentre per tutti gli altri nodi il costo viene inizialmente considerato infinito, o comunque sconosciuto. A ogni passo si sceglie il nodo non ancora confermato che ha il costo temporaneo minore e lo si rende definitivo. Successivamente si aggiornano i costi dei suoi vicini, verificando se passando per quel nodo si ottiene un percorso migliore rispetto a quello conosciuto fino a quel momento.

Il funzionamento può essere riassunto così:

- si sceglie un nodo sorgente;
- si assegna costo 0 alla sorgente e costo infinito a tutti gli altri nodi;
- si seleziona ogni volta il nodo non ancora confermato con costo minore;
- si aggiornano i costi dei nodi adiacenti, se il nuovo cammino risulta più conveniente;
- si ripete il procedimento finché tutti i nodi raggiungibili hanno un costo definitivo.

Il risultato finale dell'algoritmo non è soltanto il costo minimo verso ciascun nodo, ma anche l'insieme dei predecessori che permette di ricostruire i cammini minimi. In pratica, applicando Dijkstra a una rete rappresentata come grafo pesato, si ottiene un vero e proprio albero dei cammini minimi radicato nella sorgente. Ma che cosa è un grafo pesato? Si tratta di una struttura dati in cui i noi sono gli host della rete ed i collegamenti sono i mezzi trasmissivi che collegano due, o più nodi. Ciascun collegamento, detto arco, ha un peso: il peso potrebbe rappresentare una metrica fondamentale delle reti di calcolatori, oppure la QoS richiesta dall'host sorgente, o dall'host destinatario. Nel nostro caso, si sceglie sempre l'arco che ha peso minore, in quanto un peso maggiore potrebbe significare un collegamento più lento, od attualmente congestionato.

La seguente figura rappresenta come opera l'algoritmo shortest path:

<!-- to add -->
*In Figura: un grafo pesato con i costi sui collegamenti e i passaggi principali dell'algoritmo di Dijkstra fino alla costruzione dell'albero dei percorsi minimi*

L'algoritmo di Dijkstra è molto importante nello studio del routing perché mostra in modo chiaro come sia possibile passare da una descrizione completa della rete, vista come grafo, alla costruzione sistematica dei percorsi ottimi verso tutte le destinazioni.

##### 04.02.06. Algoritmo flooding

L'algoritmo flooding è uno dei metodi più semplici per inoltrare un pacchetto nella rete. L'idea di base è la seguente: quando un router riceve un pacchetto, invece di scegliere un unico collegamento in uscita, ne invia una copia su tutti i collegamenti disponibili, tranne eventualmente quello da cui il pacchetto è arrivato. In questo modo il pacchetto si diffonde rapidamente in tutta la rete.

Il vantaggio principale del flooding è la sua robustezza. Poiché il pacchetto viene replicato molte volte e percorre simultaneamente cammini differenti, è molto probabile che almeno una copia riesca a raggiungere la destinazione anche in presenza di guasti, collegamenti interrotti o informazioni di routing incomplete. Per questo motivo il flooding è utile soprattutto in contesti particolari, come la scoperta di percorsi, la diffusione di informazioni di controllo e alcune procedure di emergenza.

Tuttavia, il flooding ha anche un difetto molto grave: genera un numero enorme di copie dello stesso pacchetto, con conseguente spreco di banda e possibilità di congestionare rapidamente la rete. Inoltre, senza opportuni meccanismi di controllo, i pacchetti duplicati potrebbero continuare a circolare indefinitamente. Per limitare questo problema si introducono normalmente contromisure come:

- numero di sequenza per riconoscere e scartare i duplicati;
- contatore di vita del pacchetto, o hop count, per impedirne la circolazione infinita;
- inoltro selettivo solo su alcuni collegamenti ritenuti più promettenti.

La seguente figura mostra come avviene l'algoritmo flooding:

<!-- to add -->
*In Figura: un pacchetto ricevuto da un router e replicato su più collegamenti, con evidenza della propagazione delle copie nella rete*

In sintesi, il flooding non è un algoritmo efficiente per l'inoltro ordinario dei pacchetti, ma è molto importante dal punto di vista teorico e pratico perché mostra il modo più diretto possibile per garantire la diffusione dell'informazione nella rete.

##### 04.02.07. Algoritmo basato sui DVs (Distance Vectors)

Gli algoritmi basati sui DVs (Distance Vectors, ovvero vettori delle distanze) si fondano su un'idea semplice: ciascun router mantiene una tabella che, per ogni destinazione della rete, indica la distanza stimata da essa e il vicino a cui inoltrare i pacchetti per raggiungerla. Il termine "vector" deriva proprio dal fatto che ogni router possiede un vettore di distanze verso tutte le possibili destinazioni conosciute.

Il funzionamento è distribuito. Ogni router conosce inizialmente soltanto il costo dei collegamenti verso i propri vicini diretti. Periodicamente, oppure quando avviene un cambiamento nella rete, ciascun router invia ai router adiacenti il proprio DV. Quando un router riceve il vettore di un vicino, lo usa per aggiornare le proprie stime: se passando attraverso quel vicino il costo verso una certa destinazione risulta minore rispetto a quello noto fino a quel momento, la tabella viene modificata. Quindi, viene sempre preferito un costo minore.

In forma intuitiva, il principio è questo: se per raggiungere il router $X$ conviene andare prima al vicino $Y$, allora il costo totale sarà dato dal costo per arrivare a $Y$ più il costo che $Y$ dichiara di avere verso $X$. Questo modo di aggiornare le tabelle è alla base dell'algoritmo di Bellman-Ford, che costituisce il fondamento teorico dei DVs.

Il comportamento generale può essere riassunto così:

- ogni router conosce il costo verso i propri vicini diretti;
- ogni router mantiene una tabella delle distanze verso tutte le destinazioni note;
- periodicamente i router si scambiano le rispettive tabelle con i vicini;
- ciascun router aggiorna le proprie stime confrontando i costi ricevuti con quelli già presenti;
- il processo continua finché tutta la rete converge verso una situazione stabile.

I vantaggi principali dei DVs sono la semplicità e la natura distribuita: non è necessario che ogni router conosca l'intera topologia della rete, ma basta che scambi informazioni con i propri vicini. Tuttavia, questa semplicità ha un prezzo. Gli algoritmi basati sui DVs possono convergere lentamente e soffrono di problemi classici come il count to infinity, cioè l'aumento progressivo e scorretto della distanza stimata verso una destinazione non più raggiungibile. Per ridurre questi problemi si usano tecniche come split horizon, route poisoning e trigger update.

La seguente figura mostra il funzionamento dei DVs:

<!-- to add -->
*In Figura: tre, o più router che si scambiano i rispettivi distance vector e aggiornano progressivamente le proprie tabelle di instradamento*

In sintesi, i DVs rappresentano uno dei modelli classici del routing dinamico: sono semplici da capire e da implementare, ma meno rapidi e meno robusti rispetto ad approcci più evoluti, come quelli basati sui LSs (Link States), che analizzeremo nel prossimo paragrafo. Inoltre, tutti gli algoritmi basati sui DVs sono basati su una conoscenza locale della rete: in pratica, ciascun router mantiene le proprie distanze in locale e non necessariamente conosce la topologia globale della rete in cui sta operando. 

##### 04.02.08. Algoritmo basato sui LSs (Link States)

Gli algoritmi basati sui LSs (Link States, ovvero stati dei collegamenti) adottano un approccio differente rispetto agli algoritmi basati sui DVs (Distance Vectors). Invece di conoscere solo la distanza dalle destinazioni tramite i vicini, ciascun router cerca di costruire una visione completa della topologia della rete. Per farlo, ogni router scopre anzitutto quali sono i propri vicini diretti e il costo dei collegamenti che lo uniscono ad essi; successivamente diffonde queste informazioni a tutti gli altri router della rete mediante appositi messaggi detti LSP (Link-State Packet), o LSA (Link-State Advertisement).

In questo modo ogni router riceve informazioni sugli stati dei collegamenti di tutti gli altri router e può costruire localmente una mappa completa della rete, cioè un grafo pesato dell'intera topologia. Una volta ottenuta questa mappa, ciascun router applica un algoritmo di shortest path, tipicamente Dijkstra, per calcolare i migliori percorsi verso tutte le destinazioni.

Il funzionamento generale può essere riassunto così:

- ogni router scopre i propri vicini diretti;
- misura, o stima, il costo dei collegamenti verso tali vicini;
- genera un pacchetto LS contenente queste informazioni;
- diffonde il pacchetto LS a tutti gli altri router della rete;
- ciascun router costruisce localmente la stessa mappa della topologia;
- su tale mappa ogni router esegue Dijkstra per ottenere i percorsi minimi.

Il grande vantaggio di questo approccio è che ciascun router possiede una conoscenza globale della rete, e non solo locale. Questo permette normalmente una convergenza più rapida e decisioni di routing più accurate rispetto agli algoritmi basati sui DVs. Inoltre, i problemi classici dei DVs, come il count to infinity, risultano molto meno rilevanti in questo modello, poiché appunto si ha la conoscenza completa della topologia della rete.

Naturalmente anche gli algoritmi basati sui LSs hanno dei costi. La diffusione delle informazioni di stato richiede più memoria, più capacità di calcolo e più traffico di controllo rispetto agli algoritmi basati sui DVs. Per questo motivo sono più sofisticati, ma anche più onerosi da gestire. Un esempio molto importante di protocollo reale basato sui LSs è OSPF (Open Shortest Path First), che analizzeremo più avanti in questo stesso capitolo.

La seguente figura è utile per comprendere come funzionano gli algoritmi basati sui LSs:

<!-- to add -->
*In Figura: ogni router diffonde i propri link states, tutti costruiscono lo stesso grafo della rete e poi applicano Dijkstra localmente*

In sintesi, gli algoritmi basati sui LSs si fondano su una conoscenza globale della topologia e permettono un routing generalmente più rapido e preciso, al prezzo però di una maggiore complessità rispetto agli algoritmi basati sui Distance Vectors.

##### 04.02.09. Algoritmo basato sul routing gerarchico

Il routing gerarchico è una tecnica usata per rendere più gestibile il routing nelle reti molto grandi. L'idea di base è suddividere la rete in regioni, aree, o domini: ciascun router conosce bene la topologia della propria area, ma possiede informazioni più sintetiche sulle altre aree.

Questo approccio riduce la dimensione delle tabelle di routing e il volume degli aggiornamenti scambiati nella rete, migliorando la scalabilità complessiva. Lo svantaggio è che, semplificando la visione globale della rete, il percorso scelto potrebbe non essere sempre il migliore in assoluto, ma resta comunque un buon compromesso tra efficienza e complessità. Ricordiamoci che dobbiamo ragionare su scale geografiche molto ampie e su un'interconnessione di un grandissimo numero di host: non a caso il routing gerarchico viene usato soprattutto nelle reti WAN e GAN (l'odierna Internet). La seguente figura mostra che cosa si intende per "routing gerarchico":

<!-- to add -->
*In Figura: che cosa si intende per routing gerarchico. In figura sono rappresentati quattro domini differenti: A, B, C e D. Ciascun router conosce la topologia del proprio dominio, ma non ha idea di come sono fatti gli altri domini: gli basta semplicemente conoscere il router d'ingresso del dominip*

Il BGP (Border Gatewat Protocol) è l'esempio principale di routing gerarchico.

##### 04.02.10. Routing broadcast, multicast e anycast

Nel routing broadcast un pacchetto deve essere consegnato a tutti i nodi della rete, o di una certa sottorete. È quindi una comunicazione one-to-all (letteralmente, "uno a tutti"). Per realizzarla si possono usare tecniche come il flooding controllato, oppure alberi di distribuzione che evitano duplicazioni inutili.

Nel routing multicast, invece, il pacchetto deve raggiungere solo un gruppo specifico di destinatari interessati a riceverlo. Si tratta quindi di una comunicazione uno-a-molti selettiva: i router cercano di inoltrare i pacchetti solo lungo i rami della rete che portano a membri del gruppo multicast, riducendo lo spreco di banda rispetto al broadcast. Il multicast è un modello di comunicazione one-to-many (letteralmente, "uno a molti"), dove il lato "many" non necessariamente coinvolge tutti gli host della rete.

L'anycast, infine, è un modello one-to-one (letteralmente, "uno a uno"), fra molti possibili destinatari: più nodi condividono lo stesso indirizzo logico e la rete consegna il pacchetto a uno solo di essi, in genere quello ritenuto più vicino, o più conveniente secondo le metriche di routing. Questo approccio è molto usato per distribuire il carico tra server equivalenti e per migliorare tempi di risposta e affidabilità.

In sintesi:

- broadcast: un mittente invia a tutti gli altri host della rete;
- multicast: un mittente invia solo a un gruppo di host della rete;
- anycast: un mittente invia a un solo host della rete (anche se più host hanno lo stesso indirizzo IP logico).

La seguente figura confronta visivamente i tre casi:

<!-- to add -->
*In Figura: un nodo sorgente che invia rispettivamente a tutti i nodi, solo a un gruppo selezionato, oppure a uno solo tra più nodi equivalenti*

##### 04.02.11. Routing nelle reti mobile

Nelle reti mobile il problema del routing diventa più complesso perché l'host destinatario, o anche quello sorgente, può cambiare posizione mentre la comunicazione è ancora in corso. In questo caso non basta più conoscere un indirizzo logico fisso: la rete deve anche essere in grado di capire dove si trova in quel momento il nodo mobile e come raggiungerlo senza interrompere la connessione.

L'idea generale è distinguere tra identità del nodo e punto attuale di collegamento alla rete. Un dispositivo mobile può mantenere il proprio indirizzo logico principale, ma collegarsi di volta in volta a reti diverse. Per questo motivo servono meccanismi di aggiornamento della posizione, di inoltro dei pacchetti verso la nuova rete e di gestione del passaggio da un punto di accesso a un altro, operazione che prende il nome di handoff, o handover.

Nei sistemi ispirati a Mobile IP si introducono in genere un home network, cioè la rete originaria del nodo mobile, e una foreign network, cioè la rete in cui esso si trova temporaneamente. Quando il nodo cambia rete, la sua posizione viene registrata e i pacchetti possono essere reindirizzati verso il nuovo punto di aggancio. La difficoltà principale consiste nel farlo in modo trasparente, rapido ed efficiente, limitando ritardi, perdite di pacchetti e spreco di banda.

La seguente figura sarebbe utile per chiarire il concetto:

<!-- to add -->
*In Figura: un host mobile che si sposta dalla propria home network a una foreign network, con indicazione del reindirizzamento dei pacchetti verso la nuova posizione*

### 04.03. Protocollo IP
<!-- to do -->

##### 04.03.01. IPv4 e IPv6: quali sono le differenze?
<!-- to do -->

##### 04.03.02. Struttura degli indirizzi IPv4
<!-- to do -->

##### 04.03.03. Struttura degli indirizzi IPv6
<!-- to do -->

##### 04.03.04. Classificazione degli indirizzi IPv4
<!-- to do - classe A -->
<!-- to do - classe B -->
<!-- to do - classe C -->
<!-- to do - classe D -->
<!-- to do - classe E -->
<!-- to do - classfull vs classless -->

##### 04.03.05. Tipi di indirizzi IPv6
<!-- to do - global unicast -->
<!-- to do - link-local -->
<!-- to do - unique local unicast -->
<!-- to do - multicast -->  
<!-- to do - anycast -->

##### 04.03.06. Notazione CIDR e subnet mask per gli indirizzi IPv4
<!-- to do -->

##### 04.03.07. Notazione CIDR e subnet mask per gli indirizzi IPv6
<!-- to do -->

##### 04.03.08. Indirizzi IPv4 e IPv6 "speciali"
<!-- to do -->

##### 04.03.09. Struttura di un datagramma IPv4
<!-- to do -->

##### 04.03.10. Struttura di un datagramma IPv6
<!-- to do -->

##### 04.03.11. NAT (Network Address Translation)
<!-- to do -->

##### 04.03.12. Subnetting IPv4 e IPv6
<!-- to do -->

### 04.04. Controllo del traffico
<!-- to do -->

##### 04.04.01. Grafico del traffico e capacità della rete
<!-- to do -->

##### 04.04.02. Traffic-aware routing
<!-- to do -->

##### 04.04.03. Controllo di ammissione
<!-- to do -->

##### 04.04.04. Traffic throttling
<!-- to do -->

##### 04.04.05. Load shedding
<!-- to do -->

### 04.05. QoS (Quality of Service)
<!-- to do -->

##### 04.05.01. Caratteristiche del QoS
<!-- to do -->

##### 04.05.02. Traffic shaping
<!-- to do -->

##### 04.05.03. Scheduling dei datagrammi
<!-- to do -->

##### 04.05.04. Controllo di ammissione
<!-- to do -->

##### 04.05.05. QoS routing
<!-- to do -->

##### 04.05.06. IntServ (Integrated Services)
<!-- to do -->

##### 04.05.07. DiffServ (Differentiated Services˝)
<!-- to do -->

##### 04.05.08. Servizi class-based
<!-- to do -->

### 04.06. Il routing su Internet
<!-- to do -->

##### 04.06.01. Tecnica Tunnelig
<!-- to do -->

##### 04.06.02. MTU (Maximum Transmission Unit) e packet fragmentation
<!-- to do -->

##### 04.06.03. ICMP (Internet Control Message Protocol)
<!-- to do -->

##### 04.06.04. ARP (Address Resolution Protocol)
<!-- to do -->

##### 04.06.05. DHCP (Dynamic Host Configuration Protocol)
<!-- to do -->

##### 04.06.06. OSPF (Open Shortest Path First)
<!-- to do -->

##### 04.06.07. BGP (Border Gateway Protocol)
<!-- to do -->

##### 04.06.08. Ping
<!-- to do -->

##### 04.06.09. Traceroute
<!-- to do -->

##### 04.06.10. Mobile IP
<!-- to do -->