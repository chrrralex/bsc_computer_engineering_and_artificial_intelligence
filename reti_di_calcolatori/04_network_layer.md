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

Eccoci giunti all'argomento forse più importante e noto del livello network: IP. Il protocollo IP (Internet Protocol) è il protocollo fondamentale del livello network dello stack TCP/IP. Il suo compito principale è fornire un sistema di indirizzamento logico e permettere l'inoltro dei datagrammi da una sorgente a una destinazione anche attraverso reti diverse e numerosi router intermedi.

IP offre un servizio di tipo connectionless e best effort: non stabilisce una connessione preventiva, non garantisce la consegna, né l'ordine dei pacchetti, ma si occupa di farli avanzare nella rete nel modo più corretto ed efficiente possibile, in relazione alla QoS (la qualità del servizio) richiesta dagli host in comunicazione. Proprio per questo motivo, tutto il funzionamento di Internet dipende in larga parte da IP e dalla struttura dei suoi indirizzi.

Nei prossimi paragrafi analizzeremo le due versioni principali del protocollo, IPv4 e IPv6, la struttura degli indirizzi, i datagrammi, il NAT e le principali tecniche di suddivisione delle reti.

##### 04.03.01. IPv4 e IPv6: quali sono le differenze?

IPv4 e IPv6 sono due versioni dello stesso protocollo di rete, ma differiscono per struttura, capacità e obiettivi progettuali. IPv4 è la versione storicamente più diffusa e usa indirizzi lunghi 32 bit, mentre IPv6 è stato introdotto soprattutto per superare il limite dello spazio di indirizzamento di IPv4 e usa indirizzi lunghi 128 bit. Parliamoci chiaro: gli ingegneri di oltre trent'anni fa non si sarebbero mai immaginati una crescita così vasta di Internet e non si sarebbero mai aspettati che miliardi e miliardi di dispositivi si potessero connettere in tutto il mondo, per questo è stato inventato IPv6.

Le differenze principali possono essere riassunte così:

- IPv4 usa indirizzi più brevi, scritti di solito in notazione decimale puntata, ad esempio `192.168.1.10`;
- IPv6 usa indirizzi molto più lunghi, scritti in formato esadecimale separato da due punti, ad esempio `2001:0db8::1`;
- IPv6 offre uno spazio di indirizzamento enormemente più ampio rispetto a IPv4;
- IPv4 fa spesso uso del NAT per compensare la scarsità di indirizzi pubblici, mentre IPv6 è stato progettato per ridurre questa necessità;
- l'header di IPv6 è più semplice e regolare rispetto a quello di IPv4, così da rendere più efficiente l'inoltro nei router;
- IPv6 integra meglio funzioni moderne come l'autoconfigurazione degli indirizzi e un supporto più naturale al multicast.

In sintesi, IPv4 rappresenta la base storica di Internet, mentre IPv6 costituisce la sua evoluzione naturale, pensata per reti molto più grandi, più scalabili e più adatte alle esigenze attuali.

##### 04.03.02. Struttura degli indirizzi IPv4

Un indirizzo IPv4 è composto da 32 bit. Per renderlo più leggibile, esso viene normalmente suddiviso in 4 gruppi di 8 bit, detti ottetti, e rappresentato in notazione decimale puntata. Un esempio tipico è `192.168.1.10`.

Dal punto di vista logico, un indirizzo IPv4 contiene due parti fondamentali:

- una parte che identifica la rete;
- una parte che identifica l'host all'interno di quella rete.

La separazione tra queste due parti non è visibile direttamente guardando solo il numero scritto in forma decimale, ma dipende dalla subnet mask, o dalla notazione CIDR, che stabilisce quanti bit appartengono alla rete e quanti all'host.

Ad esempio, nell'indirizzo `192.168.1.10/24`, i primi 24 bit identificano la rete, mentre gli ultimi 8 bit identificano il singolo host. Questo meccanismo permette di organizzare gli indirizzi in modo gerarchico, facilitando il routing e la suddivisione delle reti in sottoreti.

In sintesi, la struttura di un indirizzo IPv4 è semplice solo in apparenza: dietro la notazione decimale puntata si nasconde infatti una struttura binaria precisa, fondamentale per l'indirizzamento e l'instradamento dei pacchetti.

##### 04.03.03. Struttura degli indirizzi IPv6

Un indirizzo IPv6 è composto da 128 bit, cioè quattro volte la lunghezza di un indirizzo IPv4. Per rappresentarlo in modo leggibile, esso viene suddiviso in 8 gruppi di 16 bit, scritti in esadecimale e separati da due punti. Un esempio tipico è `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.

Poiché questa scrittura sarebbe spesso troppo lunga, IPv6 permette alcune abbreviazioni:

- gli zeri iniziali di ciascun gruppo possono essere omessi;
- una sequenza continua di gruppi composti solo da zeri può essere sostituita una sola volta con `::`.

Per esempio, l'indirizzo precedente può essere scritto in forma abbreviata come `2001:db8:85a3::8a2e:370:7334`.

Dal punto di vista logico, anche un indirizzo IPv6 è organizzato in modo gerarchico. In generale contiene:

- una parte iniziale che identifica il prefisso di rete;
- una parte finale che identifica l'interfaccia, o l'host, all'interno di quella rete.

Molto spesso, nelle reti IPv6, i primi 64 bit identificano la rete e gli ultimi 64 bit identificano l'interfaccia. Questa struttura rende più semplice l'autoconfigurazione e favorisce una gestione più ordinata e scalabile dell'indirizzamento.

In sintesi, la struttura degli indirizzi IPv6 è più lunga e apparentemente più complessa di quella IPv4, ma è stata progettata per essere più flessibile, gerarchica e adatta alla crescita di Internet.

##### 04.03.04. Classificazione degli indirizzi IPv4

Storicamente, gli indirizzi IPv4 venivano classificati in classi, in base al valore dei bit iniziali del primo ottetto. Questo modello prende il nome di indirizzamento classful e serviva a stabilire automaticamente quanti bit fossero riservati alla rete e quanti all'host.

Le classi principali erano le seguenti:

- Classe A: indirizzi con primo ottetto compreso tra `1` e `126`. In questa classe il primo ottetto identifica la rete e i restanti tre identificano l'host. Era pensata per reti enormi, con un numero molto elevato di host. L'intervallo privato principale di questa classe è `10.0.0.0/8`, cioè da `10.0.0.0` a `10.255.255.255`.
- Classe B: indirizzi con primo ottetto compreso tra `128` e `191`. In questo caso i primi due ottetti identificano la rete e gli altri due l'host. Era adatta a reti di dimensione intermedia. L'intervallo privato associato è `172.16.0.0/12`, cioè da `172.16.0.0` a `172.31.255.255`.
- Classe C: indirizzi con primo ottetto compreso tra `192` e `223`. Qui i primi tre ottetti identificano la rete e l'ultimo l'host. Era pensata per reti più piccole, ma molto numerose. L'intervallo privato più noto è `192.168.0.0/16`, cioè da `192.168.0.0` a `192.168.255.255`.
- Classe D: indirizzi con primo ottetto compreso tra `224` e `239`. Non sono usati per identificare singoli host, ma per il multicast.
- Classe E: indirizzi con primo ottetto compreso tra `240` e `255`. Sono riservati a usi sperimentali, o speciali, e non vengono normalmente assegnati agli host.

Questo schema aveva il vantaggio della semplicità, ma portava a uno spreco notevole di indirizzi, perché obbligava a usare blocchi di dimensione fissa, spesso troppo grandi, o troppo piccoli rispetto alle necessità reali.

Per questo motivo il modello classful è stato progressivamente abbandonato in favore del modello classless, basato su CIDR (Classless Inter-Domain Routing). Con l'approccio classless non si ragiona più in termini rigidi di classi A, B e C, ma si specifica direttamente quanti bit appartengono al prefisso di rete, ad esempio `/24`, `/20` o `/27`. Questo rende l'assegnazione degli indirizzi molto più flessibile ed efficiente.

In sintesi, la classificazione in classi è importante soprattutto dal punto di vista storico e didattico, mentre nelle reti moderne si usa quasi sempre l'indirizzamento classless.

##### 04.03.05. Tipi di indirizzi IPv6

In IPv6 non si usa una classificazione in classi come avveniva storicamente in IPv4. Esistono invece diversi tipi di indirizzi, ciascuno pensato per uno specifico uso all'interno della rete.

- Global unicast: sono gli indirizzi pubblici instradabili su Internet. Identificano in modo univoco un'interfaccia a livello globale e costituiscono l'equivalente più vicino degli indirizzi pubblici IPv4. In genere appartengono allo spazio `2000::/3`.
- Link-local: sono indirizzi validi solo all'interno del collegamento locale, cioè della singola rete fisica, o logica, a cui un host è connesso. Non vengono instradati dai router e sono usati per funzioni fondamentali come autoconfigurazione, Neighbor Discovery e comunicazioni locali. Appartengono al prefisso `fe80::/10`.
- Unique local unicast: sono indirizzi privati IPv6, usati all'interno di reti locali, o organizzazioni, senza essere instradati pubblicamente su Internet. Sono l'equivalente concettuale degli indirizzi privati IPv4, anche se non nascono per essere usati necessariamente con NAT. Appartengono in genere al blocco `fc00::/7`.
- Multicast: identificano un gruppo di interfacce. Un pacchetto inviato a un indirizzo multicast viene consegnato a tutti i nodi che fanno parte di quel gruppo. In IPv6 il multicast sostituisce il broadcast, che infatti non esiste più come tipo di indirizzo separato. Gli indirizzi multicast appartengono al prefisso `ff00::/8`.
- Anycast: più interfacce condividono lo stesso indirizzo anycast e la rete consegna il pacchetto a una sola di esse, di solito quella ritenuta più vicina, o più conveniente. L'anycast è utile per distribuire servizi replicati e migliorare efficienza e disponibilità. Dal punto di vista sintattico, un indirizzo anycast ha la stessa forma di un indirizzo unicast: cambia il modo in cui viene assegnato e utilizzato.

In sintesi, IPv6 distingue chiaramente tra indirizzi pubblici globali, indirizzi locali, indirizzi di gruppo e indirizzi condivisi tra più nodi equivalenti, offrendo un modello più ordinato e flessibile rispetto a IPv4.

##### 04.03.06. Notazione CIDR e subnet mask per gli indirizzi IPv4

La notazione CIDR indica quanti bit iniziali di un indirizzo appartengono al prefisso di rete. Per esempio, in `192.168.1.10/24` il valore `/24` significa che i primi 24 bit identificano la rete.

Negli indirizzi IPv4 questa informazione può essere espressa anche tramite subnet mask. Nell'esempio precedente, la subnet mask corrispondente è `255.255.255.0`, cioè una maschera con 24 bit a `1` seguiti da 8 bit a `0`. In breve, CIDR e subnet mask esprimono la stessa idea: separare la parte di rete dalla parte host.

##### 04.03.07. Notazione CIDR e subnet mask per gli indirizzi IPv6

Anche in IPv6 si usa la notazione CIDR per indicare la lunghezza del prefisso di rete. Per esempio, in `2001:db8:abcd:0012::1/64`, il valore `/64` indica che i primi 64 bit rappresentano la rete e i restanti 64 l'interfaccia.

In IPv6, però, non si usa normalmente una subnet mask scritta in forma estesa come avviene in IPv4: si preferisce quasi sempre indicare direttamente la lunghezza del prefisso con la notazione CIDR. Per questo motivo, in IPv6 il concetto di subnet mask esiste ancora dal punto di vista logico, ma nella pratica viene quasi sempre espresso come prefisso.

##### 04.03.08. Indirizzi IPv4 e IPv6 "speciali"

Alcuni indirizzi IP non identificano normali host pubblici, ma hanno un significato speciale all'interno del protocollo e della rete.

Tra gli indirizzi IPv4 speciali più importanti ricordiamo:

- `0.0.0.0`, usato per indicare un indirizzo non ancora assegnato, o la rete corrente in modo generico;
- `127.0.0.1`, e più in generale il blocco `127.0.0.0/8`, usato per il loopback, cioè per comunicare con sé stessi;
- `255.255.255.255`, che rappresenta il broadcast limitato sulla rete locale;
- gli indirizzi privati `10.0.0.0/8`, `172.16.0.0/12` e `192.168.0.0/16`, non instradati pubblicamente su Internet;
- gli indirizzi APIPA `169.254.0.0/16`, assegnati automaticamente quando un host non riesce a ottenere configurazione da DHCP.

Anche IPv6 possiede indirizzi speciali, tra cui:

- `::`, che indica l'indirizzo non specificato;
- `::1`, che rappresenta il loopback IPv6;
- gli indirizzi link-local `fe80::/10`, validi solo sul collegamento locale;
- gli unique local `fc00::/7`, usati per reti private;
- gli indirizzi multicast `ff00::/8`, usati per comunicazioni verso gruppi di nodi.

In sintesi, questi indirizzi speciali non servono semplicemente a numerare host, ma svolgono funzioni precise di configurazione, diagnostica, comunicazione locale e gestione del traffico di rete.

##### 04.03.09. Struttura di un datagramma IPv4

Un datagramma IPv4 è composto da due parti: un header e un payload. L'header contiene tutte le informazioni necessarie per l'instradamento e il controllo del pacchetto, mentre il payload contiene i dati del livello superiore, ad esempio un segmento TCP, o UDP.

I campi principali dell'header IPv4 sono:

- Version, che indica la versione del protocollo IP usata;
- IHL (Internet Header Length), che specifica la lunghezza dell'header;
- Type of Service, oggi interpretato soprattutto per priorità e QoS;
- Total Length, cioè la lunghezza totale del datagramma;
- Identification, Flags e Fragment Offset, usati per la frammentazione e il riassemblaggio;
- TTL (Time To Live), che limita il numero di salti del pacchetto nella rete;
- Protocol, che indica il protocollo del livello superiore trasportato, come TCP, UDP o ICMP;
- Header Checksum, usato per controllare errori nell'header;
- Source Address e Destination Address, cioè gli indirizzi IPv4 del mittente e del destinatario.

L'header IPv4 ha una lunghezza minima di 20 byte, ma può essere più lungo se sono presenti opzioni. Dopo l'header si trova il payload vero e proprio. In sintesi, il datagramma IPv4 è una struttura compatta che combina informazioni di controllo e dati, permettendo ai router di inoltrare correttamente il pacchetto fino alla destinazione. L'header di IPv4 è un esempio di header di lunghezza variabile: a seconda delle opzioni inserite e/o utilizzate da ciascun router, l'header può avere una lunghezza superiore, o inferiore.

##### 04.03.10. Struttura di un datagramma IPv6

Anche un datagramma IPv6 è formato da un header e da un payload, ma rispetto a IPv4 la sua struttura è stata semplificata. L'header base di IPv6 ha infatti lunghezza fissa di 40 byte, scelta che rende più semplice e veloce l'elaborazione da parte dei router.

I campi principali dell'header IPv6 sono:

- Version, che indica la versione del protocollo;
- Traffic Class, usato per priorità e QoS;
- Flow Label, pensato per identificare particolari flussi di traffico dal punto di vista logico;
- Payload Length, cioè la lunghezza del contenuto trasportato dopo l'header di base;
- Next Header, che indica il protocollo del livello superiore oppure un eventuale header di estensione;
- Hop Limit, equivalente del TTL di IPv4;
- Source Address e Destination Address, cioè gli indirizzi IPv6 di sorgente e destinazione.

Dopo l'header base possono comparire uno, o più extension headers, usati per funzioni aggiuntive come frammentazione, sicurezza o instradamento speciale. Infine si trova il payload vero e proprio. In sintesi, il datagramma IPv6 mantiene la stessa logica generale di IPv4, ma con una struttura più regolare, più estendibile e più efficiente. L'heade rdi IPv6 è ancora più estendibile rispetto all'header di IPv4.

##### 04.03.11. NAT (Network Address Translation)

Il NAT (Network Address Translation) è una tecnica con cui un router, o un gateway, modifica gli indirizzi IP presenti nei pacchetti mentre essi attraversano il confine tra una rete privata e una rete pubblica. In pratica, molti host interni con indirizzi privati possono condividere uno, o pochi, indirizzi IPv4 pubblici.

Consideriamo la seguente figura, che mostra le due reti A e B: la rete A è un'area a cui si accede mediante il router R1, mentre la rete B è un'area a cui si accede mediante il router R2:

<!-- to add -->
*In Figura: un esempio di applicazione del protocollo NAT alle reti A e B*

Tutti gli host della rete A condividono lo stesso indirizzo pubblico, ovvero quello dell'interfacca del router R1 a cui è collegata l'intera rete A. Analogamente, tutti gli host della rete B condividono l'indirizzo pubblico posseduto dall'interfacca a cui la rete B è collegata del router R2. Quando l'host H4, della rete B, invia un pacchetto IP all'host H2 della rete A:

- Il router R2 sostituisce l'indirizzo IP sorgente di H4 nel proprio indirizzo IP pubblico.
- Il router R1 accetta il pacchetto IP proveniente da R2 e, grazie al livello datalink, consegnerà il pacchetto all'host H2.

Un caso molto tipico di utilizzo del protocollo NAT è il PAT (Port Address Translation), in cui non viene tradotto solo l'indirizzo IP, ma anche il numero di porta, così da distinguere più comunicazioni contemporanee provenienti da host diversi. Questo meccanismo ha avuto enorme diffusione perché ha permesso di rallentare l'esaurimento degli indirizzi IPv4 pubblici.

Il vantaggio principale del NAT è quindi il risparmio di indirizzi pubblici e una maggiore separazione tra rete interna e rete esterna. Lo svantaggio è che rompe in parte il principio end-to-end di Internet, perché i pacchetti vengono modificati lungo il percorso e alcune applicazioni, o protocolli, richiedono accorgimenti aggiuntivi per funzionare correttamente.

##### 04.03.12. Subnetting IPv4 e IPv6

Il subnetting è la tecnica con cui una rete IP viene suddivisa in sottoreti più piccole, così da organizzare meglio gli indirizzi e rendere più efficiente la gestione del traffico. In IPv4 il subnetting si realizza scegliendo quanti bit dedicare al prefisso di rete e quanti agli host, mediante subnet mask, o notazione CIDR. In IPv6 il principio è lo stesso, ma si usa quasi sempre direttamente la lunghezza del prefisso. In entrambi i casi, il subnetting serve a migliorare ordine, scalabilità e controllo dell'infrastruttura di rete. In questo breve corso introduttivo sulle reti di calcolatori non c'è sufficiente spazio per analizzare il subnetting IPv4 e IPv6, ma sappiate che si tratta di una tecnica molto utilizzata oggigiorno e che permette di risparmiare tantissiimi indirizzi IPv4, oltre che migliorare la gestione delle reti. Si tratta di una tecnica molto usata da piccole e grandi istituzioni e da piccole e grandi aziende per organizzare le proprie sedi ed i propri uffici.

### 04.04. Controllo del traffico

Il controllo del traffico comprende l'insieme delle tecniche usate per regolare il flusso dei pacchetti nella rete, evitare situazioni di congestione e sfruttare meglio le risorse disponibili. Quando troppi pacchetti attraversano contemporaneamente gli stessi collegamenti, o gli stessi router, ritardi, code e perdite possono aumentare rapidamente. Per questo motivo la rete deve essere in grado non solo di instradare i pacchetti, ma anche di gestire il carico in modo efficiente. Nei prossimi paragrafi vedremo alcuni dei principali strumenti usati per raggiungere questo obiettivo.

##### 04.04.01. Grafico del traffico e capacità della rete

Per capire il problema della congestione è utile immaginare un grafico in cui sull'asse orizzontale compare il traffico offerto alla rete, mentre su quello verticale compare il throughput effettivo, cioè la quantità di dati che la rete riesce davvero a trasportare. Finché il traffico resta inferiore alla capacità disponibile, il throughput cresce quasi proporzionalmente: la rete riesce ad assorbire il carico e i ritardi restano contenuti.

Quando però il traffico si avvicina troppo alla capacità massima, la situazione cambia rapidamente. Le code nei router aumentano, i ritardi diventano più elevati e possono comparire perdite di pacchetti. Se il carico continua a crescere oltre il limite sostenibile, la rete entra in congestione: in questo caso il throughput non aumenta più in modo utile e può perfino peggiorare, perché molte risorse vengono sprecate per gestire attese, ritrasmissioni e pacchetti scartati.

In sintesi, il grafico traffico-capacità mostra che una rete non può essere caricata indefinitamente senza conseguenze: esiste una soglia oltre la quale l'aumento del traffico porta a un degrado complessivo delle prestazioni. La seguente figura mostra questo grafico:

<!-- to add -->
*In Figura: il grafico del traffico e della capacità della rete*

##### 04.04.02. Traffic-aware routing

Si tratta di una tecnica che effettua il routing (ovvero, la scelta di un determinato percorso che deve seguire un pacchetto IP) sulla base delle condizioni di traffico attuali della rete. Facciamo un esempio, per comprendere meglio come opera il traffic-aware routing, considerando la seguente figura:

<!-- to add -->
*In Figura: il router R ha tre interfacce d'uscita per il pacchetto P, ovvero i percorsi I1, I2 e I3*

Il router effettua il routing non solo eseguendo, ad esempio, un determinato algoritmo di routing (come l'algoritmo di Dijkstra, o un algoritmo basato sui DVs, o sui LSs); bensì, il router "ascolta" una serie di metriche che provengono direttamente dalle interfacce, quali l'attuale traffico e/o congestione del canale. A seconda di quanto traffico è presente nella rete, il router intrada il pacchetto P nell'interfaccia in cui ce n'è di meno.

In pratica, il traffic-aware routing combina le classiche modalità di routing basate su uno, o più algoritmi di routing con le reali condizioni di traffico della rete percepite dal router stesso.

##### 04.04.03. Controllo di ammissione

Il controllo di ammissione è una tecnica con cui la rete decide se accettare, oppure rifiutare, una nuova comunicazione in base alle risorse disponibili in quel momento. L'idea è semplice: se un nuovo flusso rischia di peggiorare troppo il servizio già offerto agli altri flussi attivi, allora conviene non ammetterlo.

Questo meccanismo è particolarmente utile quando si vogliono garantire certe prestazioni minime, ad esempio in termini di banda disponibile, ritardo o probabilità di perdita. Prima di autorizzare un nuovo traffico, la rete verifica quindi se collegamenti, code e router siano in grado di sostenerlo senza entrare in congestione.

In sintesi, il controllo di ammissione agisce come un filtro preventivo: invece di lasciare entrare tutto il traffico e gestire i problemi solo dopo, cerca di evitare in anticipo il sovraccarico della rete.

##### 04.04.04. Traffic throttling

Il traffic throttling consiste nel ridurre in modo controllato la velocità con cui un host, un'applicazione, o un flusso di traffico può immettere pacchetti nella rete. In pratica, invece di bloccare completamente la comunicazione, si rallenta il ritmo di trasmissione per evitare che il carico cresca troppo rapidamente.

Questa tecnica viene usata quando la rete è vicina alla congestione, oppure quando si vuole impedire che alcuni flussi occupino una quantità eccessiva di banda a scapito degli altri. Limitando temporaneamente il traffico in ingresso, si cerca di mantenere più stabili code, ritardi e perdite di pacchetti.

In sintesi, il traffic throttling è una forma di regolazione del flusso: non elimina il traffico, ma lo dosa nel tempo per proteggere l'equilibrio complessivo della rete.

##### 04.04.05. Load shedding

Il load shedding è una tecnica usata nelle situazioni di congestione più gravi, quando la rete non riesce più a gestire tutto il traffico ricevuto. In questi casi alcuni pacchetti, o addirittura alcuni flussi, vengono scartati intenzionalmente per ridurre rapidamente il carico complessivo.

Si tratta quindi di una misura più drastica rispetto al traffic throttling: invece di limitare soltanto la velocità di trasmissione, si rinuncia a trasportare una parte del traffico per evitare che l'intero sistema peggiori ulteriormente. In genere si cerca di scartare prima il traffico meno importante, o meno prioritario, così da proteggere quello considerato più critico.

In sintesi, il load shedding sacrifica una parte del traffico per salvaguardare la stabilità generale della rete quando le risorse disponibili non sono più sufficienti.

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

Bene, abbiamo analizzato tutte le vari sfacetturature del livello network dello stack TCP/IP. Adesso entreremo nel dettaglio e comprendero quali sono i reali protocolli e le reali applicazioni di essi all'interno di Internet, la grande rete mondiale che intercollega la stragrande maggioranza degli host presenti nel mondo. Analizzeremo anche alcune tecniche molto utili per permettere a due, o più host di comunicare fra loro.

##### 04.06.01. Tecnica Tunnelig

La tecnica di tunneling consiste nell'incapsulare un pacchetto all'interno di un altro pacchetto, così da permettergli di attraversare una rete intermedia come se viaggiasse in un "tunnel" logico. In pratica, il contenuto originale viene trattato come payload di un nuovo pacchetto, dotato di un header adatto alla rete che deve attraversare.

Questo meccanismo è utile quando due estremi della comunicazione usano un certo protocollo, ma tra di essi esiste una porzione di rete che ne usa un altro, oppure quando si vuole creare un collegamento logico sicuro, o isolato, sopra una rete pubblica. Un caso tipico è il trasporto di pacchetti IPv6 sopra una rete IPv4, oppure il funzionamento di molte VPN. La seguente figura mostra come funziona la tecnica tunneling quando si vuole trasportare un pacchetto IPv6 all'interno di un pacchetto IPv4:

<!-- to add -->
*In Figura: tecnica tunneling per trasportare i pacchetti IPv6 all'interno di pacchetti IPv4*

In sintesi, il tunneling non modifica la comunicazione logica tra sorgente e destinazione, ma aggiunge un livello di incapsulamento temporaneo che consente ai pacchetti di superare reti intermedie differenti.

##### 04.06.02. MTU (Maximum Transmission Unit) e packet fragmentation

La MTU (Maximum Transmission Unit) è la dimensione massima di pacchetto che può essere trasportata su un certo collegamento senza dover essere suddivisa. Poiché reti differenti possono avere MTU diverse, può accadere che un datagramma IP valido in una parte del percorso risulti troppo grande per attraversare il collegamento successivo.

Quando questo accade, in IPv4 il pacchetto può essere frammentato, cioè diviso in più frammenti più piccoli, ciascuno dotato delle informazioni necessarie per essere riconosciuto e riassemblato correttamente a destinazione. La frammentazione permette quindi al pacchetto di continuare il viaggio, ma introduce anche costi aggiuntivi in termini di elaborazione, ritardo e probabilità di perdita: se anche un solo frammento va perso, infatti, l'intero datagramma originale non può essere ricostruito correttamente.

In sintesi, la MTU stabilisce il limite di dimensione dei pacchetti su un collegamento, mentre la frammentazione è il meccanismo usato per adattare i datagrammi troppo grandi ai vincoli della rete attraversata. A differenza del livello datalink dello stack TCP/IP (in cui i frame hanno tutti una lunghezza fissa), i pacchetti del livello network dello stack TCP/IP possono avere una lunghezza variabile.

##### 04.06.03. ICMP (Internet Control Message Protocol)

ICMP (Internet Control Message Protocol) è un protocollo di supporto a IP usato per trasmettere messaggi di controllo, diagnostica e segnalazione di errori. Non serve a trasportare i dati delle applicazioni, ma a informare host e router su problemi che possono verificarsi durante l'inoltro dei datagrammi.

Per esempio, ICMP viene usato per segnalare che una destinazione è irraggiungibile, che il tempo di vita di un pacchetto è scaduto, oppure che un datagramma è troppo grande per essere inoltrato senza frammentazione. Proprio grazie a questi messaggi è possibile capire meglio che cosa sta accadendo nella rete e sviluppare strumenti diagnostici molto utili.

In sintesi, ICMP accompagna il funzionamento di IP fornendo un canale di feedback essenziale per il controllo e la diagnostica della rete. È inoltre alla base di strumenti molto noti, come `ping` e `traceroute`, che analizzeremo più avanti.

Dal punto di vista della struttura, un messaggio ICMP contiene in genere alcuni campi fondamentali:

- un campo Type, che indica il tipo di messaggio;
- un campo Code, che ne specifica meglio il significato;
- un campo Checksum per il controllo degli errori;
- e un payload, che dipende dal tipo di messaggio.

In molti casi questa parte finale include informazioni utili a identificare il pacchetto che ha causato il problema, così che il mittente possa capire con maggiore precisione l'origine dell'errore.

Alcuni esempi tipici di messaggi ICMP, giusto per farsi un'idea, sono i seguenti:

- Echo Request ed Echo Reply, usati da `ping` per verificare se un host è raggiungibile;
- Destination Unreachable, usato quando una destinazione, una rete, un host, o una porta non possono essere raggiunti;
- Time Exceeded, usato quando il valore di TTL (per IPv4) e di Hop Limit (per IPv6) del pacchetto arriva a zero durante il percorso;
- Redirect, usato da un router per suggerire a un host un percorso migliore verso una certa destinazione;
- Fragmentation Needed, usato per segnalare che un pacchetto è troppo grande rispetto alla MTU del collegamento successivo.

##### 04.06.04. ARP (Address Resolution Protocol)

ARP (Address Resolution Protocol) è il protocollo usato nelle reti IPv4 per associare un indirizzo IP a un indirizzo fisico di livello datalink, cioè in pratica a un indirizzo MAC. Questo è necessario perché un host può sapere a quale indirizzo IP deve inviare un datagramma, ma per trasmettere realmente il frame sulla rete locale deve conoscere anche l'indirizzo MAC del destinatario, o del router a cui consegnarlo. Proprio per questo motivo il protocollo ARP si dice che è un protocollo intermedio tra il livello datalink ed il livello network, poiché sta tra i due ed opera sia con gli indirizzi IP, sia con gli indirizzi MAC.

Il funzionamento di ARP è abbastanza semplice: quando un host conosce l'indirizzo IP di destinazione, ma non conosce il corrispondente indirizzo MAC, invia nella rete locale una ARP Request in broadcast, chiedendo quale dispositivo possieda quell'indirizzo IP. Il nodo interessato risponde con una ARP Reply, comunicando il proprio indirizzo MAC. A questo punto il mittente può aggiornare la propria ARP cache e inviare correttamente i frame.

Dal punto di vista della struttura, un messaggio ARP contiene in genere alcuni campi fondamentali:

- il tipo di hardware e il tipo di protocollo usato;
- la lunghezza dell'indirizzo MAC e dell'indirizzo IP;
- un campo Operation, che indica se il messaggio è una ARP Request, o una ARP Reply;
- l'indirizzo MAC e l'indirizzo IP del mittente;
- l'indirizzo MAC e l'indirizzo IP del destinatario.

Alcuni esempi tipici di messaggi ARP, giusto per avere un'idea, sono i seguenti:

- ARP Request: "Chi ha l'indirizzo IP `192.168.1.20`? Risponda a `192.168.1.10`";
- ARP Reply: "L'indirizzo IP `192.168.1.20` corrisponde al MAC `AA:BB:CC:DD:EE:FF`".

In sintesi, ARP fa da collegamento tra livello network e livello datalink nelle reti IPv4 locali, permettendo di tradurre gli indirizzi IP in indirizzi fisici realmente usabili per la trasmissione dei frame.

##### 04.06.05. DHCP (Dynamic Host Configuration Protocol)

DHCP (Dynamic Host Configuration Protocol) è il protocollo usato per assegnare automaticamente ai dispositivi i parametri di configurazione necessari per comunicare in rete. Invece di configurare manualmente ogni host, un server DHCP (un host della rete predisposto per fungere da "arbitro" in questo protocollo) può fornire in modo dinamico un indirizzo IP, la subnet mask, il gateway predefinito, i server DNS e altre informazioni utili. In pratica, il protocollo DHCP rende la configurazione degli host automatica.

Il funzionamento di DHCP è spesso descritto con la sequenza DORA (Discover, Offer, Request, Acknowledge). Quando un host si collega alla rete e non possiede ancora un indirizzo IP valido, invia un messaggio DHCP Discover in broadcast per cercare un server DHCP. Il server risponde con un DHCP Offer, proponendo una configurazione. Il client invia quindi un DHCP Request per richiedere formalmente quei parametri, e infine il server conferma l'assegnazione con un DHCP Ack. In questo modo l'host ottiene automaticamente la configurazione necessaria per iniziare a comunicare. Questo tipo di comunicazione è rappresentato nella seguente figura:

<!-- to add -->
*In Figura: ecco come opera il protocollo DHCP quando un host vorrebbe una configurazione da parte del server DHCP della rete locale*

Dal punto di vista della struttura, un messaggio DHCP contiene in genere alcuni campi fondamentali:

- un campo Operation, che indica se il messaggio è una DHCP Request, o una DHCP Ack;
- identificatori del client, come ad esempio il suo indirizzo MAC;
- gli indirizzi IP coinvolti, se già noti, o proposti;
- un insieme di opzioni DHCP, usate per trasportare parametri come subnet mask, gateway, DNS e durata della lease.

Una caratteristica del protocollo DHCP che merita una parentesi è la lease, cioè il periodo di tempo stabilito per cui un server DHCP assegna un determinato indirizzo IP a un dispositivo di rete.

Alcuni esempi tipici di messaggi DHCP, giusto per avere un'idea, sono i seguenti:

- DHCP Discover: il client chiede se nella rete è presente un server DHCP;
- DHCP Offer: il server propone, per esempio, l'indirizzo IP `192.168.1.50` con una certa durata di lease;
- DHCP Request: il client dichiara di voler accettare quella configurazione proposta;
- DHCP Ack: il server conferma definitivamente l'assegnazione dei parametri di rete.

In sintesi, DHCP automatizza la configurazione degli host nelle reti IP, riduce gli errori manuali e rende molto più semplice la gestione di reti con molti dispositivi.

##### 04.06.06. OSPF (Open Shortest Path First)
<!-- to do -->

##### 04.06.07. BGP (Border Gateway Protocol)
<!-- to do -->

##### 04.06.08. Ping

`ping` è uno strumento di diagnostica di rete usato per verificare se un host remoto è raggiungibile e per misurare il tempo necessario a ricevere una risposta. Il suo funzionamento si basa su ICMP: il mittente invia uno, o più, messaggi Echo Request e attende i corrispondenti Echo Reply provenienti dall'host destinatario.

Se la risposta arriva correttamente, `ping` permette di capire che la destinazione è raggiungibile e consente anche di misurare il tempo di andata e ritorno del pacchetto, detto RTT (Round-Trip Time, lo analizzeremo meglio quando parleremo dei protocolli TCP e UDP nel prossimo livello dello stack TCP/IP). Se invece non arriva alcuna risposta, oppure arrivano messaggi ICMP di errore, ciò può indicare problemi di connettività, instradamento, filtraggio, o congestione.

In pratica, `ping` è uno strumento semplice, ma molto utile per un primo controllo dello stato della rete. Un esempio tipico di utilizzo è il seguente: il comando `ping 8.8.8.8` invia messaggi Echo Request all'host con indirizzo IP `8.8.8.8` e misura se, e in quanto tempo, arrivano gli Echo Reply. Tale esempio è mostrato nella seguente figura (dove l'indirizzo IPv4 8.8.8.8 è il server DNS primario di Google):

<!-- to add -->
*In Figura: un esempio di ping mediante l'esecuzione del comando `ping 8.8.8.8`*

In sintesi, `ping` serve a capire rapidamente se un host è raggiungibile e a ottenere una stima elementare della qualità della connessione.

##### 04.06.09. Traceroute

`traceroute` è uno strumento di diagnostica usato per scoprire quali router attraversa un pacchetto nel percorso dalla sorgente alla destinazione. A differenza di `ping`, che verifica soprattutto la raggiungibilità finale, `traceroute` cerca di ricostruire passo dopo passo il cammino seguito nella rete.

Il suo funzionamento si basa sul campo TTL in IPv4, o Hop Limit in IPv6. Il programma invia una serie di pacchetti con valori iniziali sempre più grandi: prima con valore `1`, poi con `2`, poi con `3` e così via. Quando un router riceve un pacchetto e ne decrementa il TTL fino a zero, scarta il pacchetto e restituisce un messaggio ICMP Time Exceeded. In questo modo il mittente scopre l'indirizzo del router corrispondente a quel determinato salto. Ripetendo il procedimento, `traceroute` ricostruisce progressivamente l'intero percorso fino alla destinazione finale.

In pratica, `traceroute` è utile per capire dove si trovano ritardi, interruzioni o percorsi anomali nella rete. Un esempio tipico di utilizzo è il seguente: il comando `traceroute www.google.com` mostra la sequenza dei router attraversati per raggiungere il server associato a quel nome di dominio. Questa situazione, in modo semplificato è concettualmente rappresentata nella seguente figura:

<!-- to add -->
*In Figura: un esempio di traceroute durante l'esecuzione del comando `traceroute www.google.com`*

In sintesi, `traceroute` permette di osservare il cammino seguito dai pacchetti nella rete ed è molto utile per analizzare problemi di instradamento e latenza.

##### 04.06.10. Mobile IP

Mobile IP è un insieme di tecniche e protocolli progettati per permettere a un host mobile di cambiare rete senza perdere, o dover cambiare continuamente, il proprio indirizzo IP logico principale. Il problema di fondo è questo: normalmente un indirizzo IP identifica non solo un host, ma anche la rete in cui esso si trova. Se un dispositivo si sposta da una rete a un'altra, dovrebbe quindi cambiare indirizzo IP, ma questo interromperebbe facilmente le comunicazioni già in corso. Mobile IP nasce proprio per risolvere questo problema e permettere a un host in movimento di mantenere le proprie comunicazioni anche durante il cambiamento del proprio indirizzo IP.

L'idea fondamentale è separare l'identità logica del nodo dalla sua posizione attuale nella rete. Un host mobile mantiene un indirizzo stabile, detto home address, associato alla sua rete originaria, chiamata home network. Quando però il dispositivo si trova temporaneamente in un'altra rete, detta foreign network, la rete deve comunque essere in grado di recapitargli i pacchetti. Per fare questo si introduce un indirizzo temporaneo, detto care-of address, che rappresenta il punto attuale in cui il nodo mobile è raggiungibile.

Nel modello classico di Mobile IP compaiono in genere tre elementi principali:

- il mobile node, cioè l'host che si sposta da una rete all'altra;
- l'home agent, cioè il router, o agente, presente nella home network che tiene traccia della posizione temporanea del nodo mobile;
- il foreign agent, cioè il router, o agente, della rete visitata che aiuta il nodo mobile a ricevere i pacchetti nella foreign network.

In alcune varianti moderne il nodo mobile può anche ottenere e usare direttamente un care-of address senza dipendere sempre da un foreign agent dedicato, ma il modello con home agent e foreign agent resta molto utile dal punto di vista didattico per capire il meccanismo generale.

Il funzionamento può essere descritto in modo semplificato così:

1. il nodo mobile si collega alla propria home network e comunica normalmente usando il suo home address;
2. quando si sposta in una foreign network, rileva che si trova in una rete diversa e ottiene un care-of address;
3. il nodo mobile registra il nuovo care-of address presso il proprio home agent;
4. quando un host remoto invia un pacchetto verso l'home address del nodo mobile, il pacchetto arriva alla home network;
5. l'home agent intercetta il pacchetto e lo inoltra verso il care-of address, spesso mediante tunneling;
6. il pacchetto raggiunge la foreign network e viene consegnato al nodo mobile nella sua posizione attuale.

La seguente figura mostra l'idea generale del meccanismo:

<!-- to add -->
*In Figura: un mobile node che lascia la home network, ottiene un care-of address nella foreign network e riceve i pacchetti tramite home agent e tunneling*

Il ruolo del tunneling è particolarmente importante. Quando l'home agent riceve un pacchetto destinato all'home address del nodo mobile, non può semplicemente consegnarlo localmente, perché il nodo non si trova più nella rete originaria. Per questo motivo l'home agent incapsula il datagramma originale dentro un nuovo pacchetto IP e lo invia verso il care-of address. Arrivato nella foreign network, il pacchetto viene decapsulato e consegnato al destinatario mobile. In pratica, Mobile IP sfrutta proprio la tecnica di tunneling che abbiamo già introdotto nei paragrafi precedenti.

Dal punto di vista logico, il vantaggio principale è la trasparenza verso i corrispondenti. Un host remoto, spesso chiamato correspondent node, può continuare a inviare i pacchetti verso l'home address del nodo mobile senza dover sapere in quale rete esso si trovi realmente in quel momento. Sarà poi l'infrastruttura di Mobile IP a occuparsi del reindirizzamento.

Questo meccanismo, però, introduce anche alcune inefficienze. Il caso più noto è il cosiddetto triangular routing. Supponiamo che un correspondent node voglia comunicare con un host mobile che si è spostato lontano dalla sua home network. I pacchetti inviati dal corrispondente raggiungono prima la home network, vengono intercettati dall'home agent e solo dopo sono ritrasmessi verso la foreign network. Il percorso reale del traffico può quindi risultare più lungo del necessario, formando idealmente un triangolo tra mittente, home agent e host mobile.

La seguente figura aiuta a visualizzare questo problema:

<!-- to add -->
*In Figura: esempio di triangular routing, in cui i pacchetti passano prima per la home network e solo dopo raggiungono il nodo mobile nella foreign network*

Per ridurre questo inconveniente, alcune evoluzioni del protocollo introducono meccanismi di route optimization, con cui il correspondent node può imparare il care-of address corrente del nodo mobile e inviargli più direttamente i pacchetti. Tuttavia, questa ottimizzazione rende il sistema più complesso e richiede maggiore attenzione alla sicurezza e all'aggiornamento delle informazioni di posizione.

Un altro aspetto importante è la gestione della mobilità durante una comunicazione già attiva. Quando il nodo mobile cambia nuovamente rete, deve ottenere un nuovo care-of address e registrarlo rapidamente presso il proprio home agent. Questo processo deve essere abbastanza veloce da limitare interruzioni, ritardi e perdite di pacchetti. Qui entra in gioco il concetto di handoff, o handover, cioè il passaggio da una rete, o da un punto di accesso, a un altro.

In sintesi, Mobile IP cerca di conciliare due esigenze che normalmente entrano in conflitto:

- mantenere stabile l'identità logica del nodo mobile;
- permettere al nodo di spostarsi fisicamente tra reti differenti;
- continuare a ricevere traffico anche mentre la sua posizione cambia.

Dal punto di vista storico e concettuale, Mobile IP è stato molto importante perché ha mostrato come gestire la mobilità a livello network. Nelle reti moderne molte soluzioni pratiche per la mobilità usano approcci differenti, spesso integrati con livelli superiori, reti cellulari e meccanismi applicativi, ma le idee introdotte da Mobile IP restano fondamentali per comprendere il problema del routing verso nodi in movimento.

In conclusione, Mobile IP permette a un host di conservare un'identità IP stabile pur cambiando rete, grazie a meccanismi di registrazione della posizione, care-of address, home agent e tunneling. Il prezzo da pagare è una maggiore complessità del sistema e, in alcuni casi, percorsi non ottimali dei pacchetti.