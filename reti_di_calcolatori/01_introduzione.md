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

Un protocollo stabilisce, in pratica, il modo in cui due, o più host della rete possono comunicare.

Uno standard è un insieme di scelte ufficiali e soprattutto effettuate da organizzazioni internazionali (che si occupano appositamente di reti e telecomunicazioni) che delinano i protocolli da utilizzare all'interno di una comunicazione.

Standard e protocolli sono in stretto rapporto tra loro ed ognuno di essi cerca di delinare tutti gli aspetti tecnici utili per raggiungere effiicenza, prestazioni, affidabilità e sicurezza maggiori. 
