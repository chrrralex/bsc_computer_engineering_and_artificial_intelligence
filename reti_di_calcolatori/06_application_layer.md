# 06. Application Layer

### 06.01. Introduzione

L'application layer è il livello più vicino all'utente nello stack TCP/IP. È il livello in cui operano i protocolli e i servizi che permettono alle applicazioni di rete di comunicare tra loro, come la navigazione Web, la posta elettronica, il trasferimento di file, la risoluzione dei nomi e lo streaming multimediale. In altre parole, mentre i livelli sottostanti si occupano del trasporto dei dati, dell'instradamento e della trasmissione fisica, il livello application si occupa del significato e dell'organizzazione logica delle comunicazioni viste dalle applicazioni.

Dal punto di vista pratico, quando un utente apre un browser, invia una email, scarica un file, oppure guarda un video in streaming, sta usando servizi che appartengono all'application layer. Questo livello non lavora isolatamente: si appoggia ai livelli inferiori, in particolare al transport layer, per ottenere canali di comunicazione affidabili, o veloci, a seconda delle necessità del protocollo utilizzato. Per esempio, HTTP e SMTP si appoggiano tipicamente a TCP, mentre altre applicazioni real-time possono preferire UDP per ridurre la latenza.

Le responsabilità principali dell'application layer possono essere riassunte così:

- definire i protocolli con cui le applicazioni si scambiano informazioni;
- stabilire il formato logico dei messaggi applicativi;
- fornire servizi di naming e risoluzione, come avviene con DNS;
- permettere l'accesso a servizi remoti come web server, mail server e file server;
- gestire aspetti applicativi come autenticazione, sessioni, comandi, richieste e risposte;
- offrire interfacce di comunicazione comprensibili ai programmi e, indirettamente, agli utenti.

È importante osservare che, nel modello TCP/IP, l'application layer ingloba in modo piuttosto ampio funzioni che in altri modelli, come il modello OSI, sarebbero distribuite tra application layer, presentation layer e session layer. Per questo motivo nel livello application dello stack TCP/IP rientrano non solo i protocolli applicativi in senso stretto, ma anche aspetti legati alla rappresentazione dei dati, alla gestione del dialogo tra processi e all'organizzazione delle sessioni di comunicazione.

In sintesi, l'application layer è il livello in cui la rete diventa davvero utile per gli utenti e per i programmi: qui si trovano i protocolli che realizzano concretamente i servizi Internet più noti, trasformando la semplice trasmissione di dati in comunicazioni con significato applicativo ben preciso.

### 06.02. Nomi e DNS (Domain Name System)

Quando navighiamo in Internet, quasi nessuno digita direttamente indirizzi IP. Scriviamo invece nomi come `www.google.com`, `it.wikipedia.org`, oppure `unica.it`. Questi nomi sono molto più facili da ricordare e da gestire, ma non sono ciò che i router e gli host usano davvero per comunicare a livello network: a basso livello la rete continua a lavorare con indirizzi IP. Serve quindi un sistema che traduca i nomi simbolici in indirizzi IP. Questo sistema è il DNS (Domain Name System), uno dei servizi più importanti dell'intero stack TCP/IP, anche se molto spesso passa inosservato all'utente.

##### 06.02.01. Obiettivi e servizi forniti dal DNS

DNS è un servizio distribuito del livello application il cui obiettivo principale è risolvere nomi simbolici in indirizzi IP, e in alcuni casi compiere anche l'operazione inversa. In pratica, quando un'applicazione vuole contattare `www.example.com`, prima di poter aprire una connessione deve sapere a quale indirizzo IP corrisponde quel nome. DNS è proprio il sistema che fornisce questa informazione ed opera su un vasto ecosistema di server (detti server DNS) distribuiti.

I servizi principali offerti da DNS possono essere riassunti così:

- traduzione di un nome di dominio in uno, o più, indirizzi IP (IPv4 e IPv6);
- traduzione inversa, cioè da indirizzo IP a nome (reverse DNS);
- gestione di informazioni associate ai domini, come server di posta, alias, record di servizio e altre informazioni amministrative;
- supporto a tecniche di bilanciamento del carico e ridondanza, perché lo stesso nome può puntare a più indirizzi IP. Posso esistere, quindi, delle associazioni multiple, o uno-a-molti tra nome simbolico e più indirizzi IP.

Senza DNS, gli utenti dovrebbero ricordare a memoria gli indirizzi IP di tutti i servizi che vogliono raggiungere e, soprattutto, le applicazioni non potrebbero contare su nomi stabili: cambiando l'indirizzo IP di un server, ogni client dovrebbe essere riconfigurato. DNS introduce quindi un livello di astrazione fondamentale tra nomi logici e indirizzi fisici di rete.

##### 06.02.02. Nomi e indirizzi IP

Per capire bene il ruolo di DNS è utile distinguere chiaramente due concetti: i nomi e gli indirizzi IP. Un indirizzo IP è un identificatore numerico usato dal livello network per individuare un'interfaccia di rete, mentre un nome è un identificatore simbolico pensato per gli esseri umani e per le applicazioni.

Le differenze più importanti sono:

- gli indirizzi IP sono legati alla posizione di rete dell'host, mentre i nomi sono legati al servizio, o all'organizzazione;
- gli indirizzi IP possono cambiare nel tempo, mentre i nomi tendono a restare stabili;
- uno stesso nome può essere associato a più indirizzi IP, e uno stesso indirizzo IP può ospitare più nomi;
- gli indirizzi IP sono usati direttamente dai protocolli di rete, mentre i nomi vengono usati soprattutto a livello applicativo.

In pratica, nomi e indirizzi IP risolvono due problemi differenti: i primi servono a identificare in modo comodo e stabile servizi e host, i secondi servono a instradare concretamente i pacchetti nella rete. DNS è il ponte tra questi due mondi. Il protocollo DNS su basa su un presupposto molto semplice: gli utenti di Internet faticano a ricordare indirizzi come `8.8.8.8`, preferendo indirizzi simbolici e più mnemonici come `www.google.com`. 

##### 06.02.03. Relazione tra dominio e indirizzo IP

Un dominio non corrisponde necessariamente a un singolo indirizzo IP. Un nome di dominio può essere associato:

- a un solo indirizzo IPv4, o IPv6, nel caso più semplice;
- a più indirizzi IP, per distribuire il carico tra server diversi;
- a indirizzi IP differenti a seconda della posizione geografica del client, come accade nelle CDN;
- a nessun indirizzo IP diretto, se il nome è un alias di un altro nome.

Allo stesso modo, un indirizzo IP può ospitare più domini diversi, come avviene tipicamente negli hosting condivisi, dove un solo server Web risponde per molti siti differenti. DNS rende possibile questa flessibilità, perché disaccoppia il nome dal singolo indirizzo IP sottostante.

##### 06.02.04. Differenza tra URL, URI, hostname e dominio

Nel contesto del Web e delle reti si usano spesso termini come URL, URI, hostname e dominio, che pur essendo collegati hanno significati distinti.

- URI (Uniform Resource Identifier): è il termine più generale; identifica una risorsa, senza specificare necessariamente come raggiungerla. Ricordiamoci che una qualsiasi risorsa, su Internet, ha un indirizzo proprio e ben preciso.
- URL (Uniform Resource Locator): è un tipo particolare di URI che indica non solo la risorsa, ma anche come e dove raggiungerla, ad esempio `https://www.example.com/pagina.html`. Questo è un indirizzo simbolico che è composto da un base URL (URL di base, detto anche host), ovvero `www.example.com` e dal percorso all'interno del server, indicato dal base URL, nel quale trovare la risorsa, che nel nostro caso è `/pagina`. In realtà, se si tratta di un documento HTML (come vedremo meglio in seguito), è plausibile che di default il server web cerchi un file denominato `index.html`, oppure `index.htm` sotto la cartella `/pagina` del server web. L'URL specifica anche il protocollo di rete utilizzato, ovvero `https://` nel nostro caso, dove HTTPS è la versione sicura e affidabile del protocollo HTTP.
- Hostname: è il nome di un host specifico in rete, ad esempio `www.example.com`. Spesso coincide con la parte di un URL che identifica il server.
- Dominio: è una porzione dello spazio dei nomi DNS, ad esempio `example.com`. Un dominio può ospitare molti hostname, come `www.example.com`, `mail.example.com` e così via.

In sintesi, ogni URL è un URI, ma non viceversa; ogni hostname appartiene a un dominio, ma un dominio può contenere molti hostname. DNS lavora soprattutto sui nomi di dominio e sugli hostname, traducendoli in indirizzi IP.

##### 06.02.05. Struttura di un nome di dominio: TLD, second-level domain e subdomain

Un nome di dominio è organizzato in modo gerarchico ed è composto da più etichette separate da punti. Leggendo il nome da destra verso sinistra si passa dalla parte più generale a quella più specifica.

Consideriamo per esempio il nome `mail.unica.it`:

- `it` è il TLD (Top-Level Domain), cioè il dominio di primo livello;
- `unica` è il second-level domain, cioè il dominio di secondo livello, registrato sotto il TLD, ovvero un dominio di secondo, terzo, quarto livello, o di livello più basso;
- `mail` è un subdomain, cioè un sottodominio definito all'interno di `unica.it`.

I TLD si dividono tradizionalmente in due grandi gruppi:

- ccTLD (country-code TLD), come `.it`, `.fr`, `.de`, `.uk`, associati a paesi, o nazioni;
- gTLD (generic TLD), come `.com`, `.org`, `.net`, `.edu`, associati a categorie generiche di organizzazioni, o servizi. Per esempio, il gTLD `.com` è normalmente rappresentativo di un'azienda, o un privato, mentre il gTLD `.org` è tipicamente associato a un'organizzazione.

Sotto un dominio di secondo livello, come `example.com`, possono essere creati molti sottodomini diversi, come `www.example.com`, `mail.example.com`, `dev.example.com`, ciascuno con le proprie informazioni DNS.

##### 06.02.06. FQDN (Fully Qualified Domain Name)

Un FQDN (Fully Qualified Domain Name) è un nome di dominio completo, che indica in modo univoco la posizione di un host nello spazio dei nomi DNS. Un FQDN comprende tutte le etichette necessarie per identificare il nome a partire dalla radice dell'albero DNS.

Formalmente un FQDN termina con un punto finale, che rappresenta la radice del namespace DNS. Per esempio, `www.example.com.` è la forma pienamente qualificata di `www.example.com`. Nella pratica quotidiana il punto finale viene quasi sempre omesso, ma è importante sapere che esiste e che chiarisce a livello logico la struttura completa del nome.

Un FQDN si distingue quindi da nomi parziali, o relativi, che sarebbero ambigui senza ulteriori informazioni di contesto. In pratica, quando un'applicazione vuole risolvere un nome con DNS, lavora sempre con un nome che, esplicitamente o implicitamente, viene trattato come un FQDN.

##### 06.02.07. Namespace gerarchico

Lo spazio dei nomi DNS è organizzato come un grande albero, detto namespace gerarchico. La radice di questo albero è un nodo speciale, spesso rappresentato come stringa vuota, oppure come un singolo punto. Sotto la radice si trovano i TLD, sotto di essi i domini di secondo livello, e così via fino ai singoli hostname.

Questa organizzazione ad albero ha due vantaggi importanti:

- distribuisce la responsabilità della gestione dei nomi tra molte organizzazioni diverse, evitando un controllo centralizzato unico;
- rende il sistema molto scalabile, perché ogni nodo dell'albero può essere gestito in modo relativamente indipendente.

La seguente figura aiuta a visualizzare la struttura ad albero del namespace DNS:

<!-- to add -->
*In Figura: l'albero del namespace DNS con la radice, i TLD (`.it`, `.com`, `.org`, ...) e alcuni domini di secondo livello e sottodomini*

In sintesi, il namespace gerarchico permette di organizzare miliardi di nomi diversi in modo ordinato e di assegnare la responsabilità di ciascuna parte dell'albero a chi davvero la gestisce.

##### 06.02.08. Struttura gerarchica dei server DNS

L'organizzazione gerarchica dei nomi si riflette direttamente nella struttura dei server DNS. Non esiste un unico server DNS che conosce tutto Internet: esiste invece una grande rete distribuita di server, ciascuno responsabile di una parte del namespace.

In modo molto semplificato, i server DNS si dividono in tre categorie principali:

- root servers, che stanno alla radice dell'albero;
- TLD servers, responsabili dei domini di primo livello;
- authoritative servers, responsabili dei singoli domini di secondo livello e dei loro sottodomini.

A questi si aggiungono i resolver, in genere offerti da provider, sistemi operativi, o servizi pubblici, che si occupano materialmente di interrogare i server DNS per conto dei client e di mettere in cache le risposte.

La seguente figura mostra in modo schematico la gerarchia dei server DNS:

<!-- to add -->
*In Figura: la gerarchia dei server DNS, dai root servers ai TLD servers, fino agli authoritative servers di dominio*

##### 06.02.09. Root servers

I root servers sono i server DNS che si trovano al vertice della gerarchia, immediatamente sotto la radice del namespace. Il loro compito principale non è risolvere direttamente i nomi, ma indicare quali sono i server responsabili dei vari TLD.

Quando un resolver non sa proprio nulla di un nome richiesto, può partire da un root server per chiedere, in pratica, "chi si occupa di `.com`?", oppure "chi si occupa di `.it`?". Il root server risponde indicando i TLD servers competenti.

I root servers sono pochi dal punto di vista logico, ma sono replicati fisicamente in moltissime istanze sparse nel mondo grazie all'uso dell'anycast: in questo modo le richieste vengono naturalmente smistate verso l'istanza più vicina, migliorando prestazioni e affidabilità.

##### 06.02.10. TLD servers

I TLD servers sono i server DNS responsabili dei domini di primo livello, come `.com`, `.org`, `.it`, `.fr` e così via. Ciascun TLD ha i propri server, gestiti dalle organizzazioni che amministrano quel particolare top-level domain.

Il compito principale dei TLD servers non è conoscere ogni dettaglio dei singoli siti, ma sapere quali sono i server authoritative per ciascun dominio di secondo livello registrato sotto quel TLD. Per esempio, i TLD servers di `.it` sanno quali sono i server authoritative per `unica.it`, `repubblica.it` e così via.

In sintesi, i TLD servers indirizzano i resolver verso il livello successivo della gerarchia, cioè verso i server che davvero conoscono le informazioni dei singoli domini.

##### 06.02.11. Authoritative servers

I server authoritative sono i server DNS che contengono le informazioni ufficiali, e quindi vincolanti, su uno, o più domini. Per ogni dominio esiste almeno un server authoritative, di solito affiancato da uno, o più server secondari per ridondanza.

Quando un resolver vuole sapere a quale indirizzo IP corrisponde, per esempio, `www.example.com`, la risposta finale e affidabile arriva proprio dall'authoritative server del dominio `example.com`. Questo server contiene la zona DNS del dominio, cioè l'insieme dei record che descrivono i nomi gestiti al suo interno.

È importante distinguere gli authoritative servers dai resolver in cache: i primi sono la fonte ufficiale dell'informazione, mentre i secondi forniscono semplicemente una copia temporanea per migliorare le prestazioni.

##### 06.02.12. DNS zones

Una zona DNS è una porzione del namespace DNS gestita come un'unità amministrativa coerente. In altre parole, una zona raggruppa tutti i nomi di cui un certo authoritative server è direttamente responsabile.

Per esempio, un'organizzazione che gestisce il dominio `example.com` può avere una zona che contiene i record per `example.com`, `www.example.com`, `mail.example.com` e altri sottodomini. Se però una parte del dominio viene delegata a un altro soggetto, ad esempio `dev.example.com`, quella sottoparte può diventare una zona separata, gestita da un proprio authoritative server.

La suddivisione in zone è molto importante perché:

- permette di distribuire la responsabilità della gestione dei nomi tra più soggetti;
- consente di organizzare meglio i grandi domini, suddividendoli in parti più piccole e più facili da amministrare;
- riflette concretamente, sui server, la struttura logica del namespace gerarchico.

##### 06.02.13. Glue records

I glue records sono particolari record DNS usati per evitare situazioni di dipendenza circolare durante la risoluzione dei nomi. Il problema si presenta quando un authoritative server per una certa zona ha un nome che appartiene proprio a quella stessa zona.

Consideriamo per esempio il dominio `example.com`, i cui server authoritative sono `ns1.example.com` e `ns2.example.com`. Per risolvere `www.example.com` il resolver dovrebbe contattare `ns1.example.com`, ma per contattarlo gli serve l'indirizzo IP di `ns1.example.com`, che si trova proprio nella zona `example.com`. Senza ulteriori informazioni, si formerebbe un loop.

Per risolvere questo problema, il TLD server (in questo caso quello di `.com`) fornisce direttamente gli indirizzi IP dei name server della zona delegata, sotto forma di glue records. In questo modo il resolver dispone subito dell'indirizzo IP necessario per contattare il server authoritative, senza dover prima risolvere ulteriormente il nome stesso.

In sintesi, i glue records sono uno strumento tecnico per garantire che la delega di zona funzioni correttamente, anche quando i name server di una zona hanno nomi appartenenti alla zona stessa.

### 06.03. Posta elettronica e SMTP (Simple Mail Transfer Protocol)
<!-- to do - obiettivi e servizi forniti da SMTP -->
<!-- to do - differenze tra SMTP, POP3 e IMAP -->
<!-- to do - architettura client/server nella posta elettronica -->
<!-- to do - flusso base di invio email -->
<!-- to do - MUA (Mail User Agent) -->
<!-- to do - MTA (Mail Transfer Agent) -->
<!-- to do - MDA (Mail Delivery Agent) -->
<!-- to do - differenze tra le porte 25, 465 e 587 -->
<!-- to do - modello request/response di SMTP -->
<!-- to do - comandi principali di SMTP -->
<!-- to do - codici di risposta SMTP -->
<!-- to do - sequenza di una sessione SMTP -->
<!-- to do - struttura degli header SMTP -->
<!-- to do - persistenza della connessione SMTP -->
<!-- to do - relay SMTP -->
<!-- to do - spam e abuso del protocollo SMTP -->
<!-- to do - SMTP store-and-forward -->
<!-- to do - SMTP routing -->
<!-- to do - generalità sulL'ESMTP (Extended SMTP) -->

### 06.04. Trasferimento file e FTP (File Transfer Protocol)
<!-- to do - obiettivi e servizi forniti da FTP -->
<!-- to do - architettura client/server di FTP -->
<!-- to do - connessione di controllo e connessione dati -->
<!-- to do - porte utilizzate da FTP -->
<!-- to do - modalità active e passive -->
<!-- to do - autenticazione FTP -->
<!-- to do - trasferimento file ASCII vs binary -->
<!-- to do - comandi principali di FTP -->
<!-- to do - codici di risposta FTP -->
<!-- to do - sessione tipica FTP -->
<!-- to do - directory remote e file system remoto -->
<!-- to do - problemi di sicurezza di FTP -->
<!-- to do - FTPS (FTP Secure) -->
<!-- to do - SFTP (SSH File Transfer Protocol) -->
<!-- to do - confronto tra FTP, FTPS e SFTP -->
<!-- to do - applicazioni pratiche del trasferimento file -->

### 06.05. World Wide Web e HTTP (HyperText Transfer Protocol)

Il WWW (World Wide Web), comunemente chiamato Web, è probabilmente l'applicazione di rete più conosciuta e usata di Internet. È nato all'inizio degli anni Novanta come sistema per condividere documenti tra ricercatori, ma si è poi evoluto in una piattaforma globale di servizi, contenuti e applicazioni. Il protocollo che ne ha reso possibile la diffusione è HTTP (HyperText Transfer Protocol), un protocollo del livello application che permette ai client (in primis i browser) di richiedere risorse a un server e di riceverne le relative risposte.

##### 06.05.01. Obiettivi e servizi forniti da HTTP

HTTP è il protocollo standard usato per scambiare risorse Web tra un client e un server. Il suo obiettivo principale è semplice: permettere a un client di chiedere una determinata risorsa, identificata da un URL, e ottenere in risposta il contenuto di tale risorsa, insieme a informazioni di servizio che ne descrivono il tipo, le dimensioni, lo stato, e così via.

I servizi principali offerti da HTTP possono essere riassunti così:

- recupero di risorse da un server Web, come pagine HTML, immagini, file CSS e script;
- invio di dati dal client al server, ad esempio nei form, nelle API e nei caricamenti di file;
- aggiornamento, sostituzione e cancellazione di risorse, soprattutto nelle API moderne;
- trasporto di informazioni di sessione, autenticazione e configurazione attraverso gli header;
- supporto a caching, proxy e meccanismi di sicurezza tramite HTTPS.

HTTP è quindi molto più di un semplice "scaricatore di pagine": è il fondamento su cui si appoggiano siti Web, applicazioni Web, servizi REST e moltissime API moderne.

##### 06.05.02. Architettura client/server del Web

Il Web segue un'architettura client/server. Da un lato c'è il client, tipicamente un browser, che chiede risorse; dall'altro lato c'è il server Web, che le rende disponibili. La comunicazione avviene sempre su iniziativa del client: il server non contatta mai spontaneamente un browser, ma si limita a rispondere alle richieste che gli arrivano.

Questa architettura è semplice ma molto efficace, perché:

- separa chiaramente i ruoli tra chi consuma e chi fornisce le risorse;
- permette a un singolo server di servire moltissimi client diversi;
- consente di costruire infrastrutture scalabili, in cui molti server cooperano per soddisfare una grande quantità di richieste.

La seguente figura mostra l'idea generale dell'architettura client/server del Web:

<!-- to add -->
*In Figura: un browser (client) che invia richieste HTTP a un web server e ne riceve le risposte*

##### 06.05.03. Browser e web server

Il browser è il programma client che l'utente usa direttamente. Si occupa di costruire le richieste HTTP, inviarle al server, ricevere le risposte e interpretarle in modo da mostrare le pagine all'utente. I browser più diffusi sono Firefox, Chrome, Safari, Edge e simili. Oltre a HTTP, un browser interpreta tipicamente HTML, CSS, JavaScript, immagini e molti altri tipi di risorse.

Il web server è il programma server che ascolta le richieste in arrivo, le elabora e produce le risposte. Esempi noti di web server sono Apache, Nginx, IIS e molti server applicativi più moderni. Un web server può:

- restituire file statici, come HTML, immagini e fogli di stile;
- eseguire codice dinamico per generare contenuti su misura;
- inoltrare le richieste a servizi applicativi, database, o backend.

In sintesi, il browser è il "consumatore" lato utente, mentre il web server è il "produttore" lato infrastruttura: entrambi comunicano tramite HTTP, parlando una lingua comune.

##### 06.05.04. Risorse Web e URL

Tutto ciò che è accessibile sul Web viene chiamato risorsa: una pagina HTML, un'immagine, un file PDF, un video, un'API, una specifica funzione di un servizio. Ogni risorsa è identificata da un URL, cioè da un indirizzo simbolico che il client usa per chiederla al server.

Il punto fondamentale è che HTTP non si occupa di sapere come la risorsa viene realmente prodotta, o memorizzata sul server: il client si limita a chiederla tramite il suo URL e il server decide come servirla. Questa astrazione è ciò che rende il Web così flessibile, perché dietro lo stesso URL può esserci un file statico, oppure un'elaborazione molto complessa.

##### 06.05.05. Struttura di un URL

Un URL HTTP, o HTTPS, è composto da diverse parti, ciascuna con un significato preciso. Consideriamo per esempio l'URL `https://www.example.com:443/percorso/pagina.html?lang=it#sezione`:

- `https` è lo schema, cioè il protocollo usato per accedere alla risorsa;
- `www.example.com` è l'host, cioè il nome del server da contattare;
- `443` è la porta, che spesso viene omessa perché ha un valore di default (80 per HTTP, 443 per HTTPS);
- `/percorso/pagina.html` è il path, cioè il percorso della risorsa sul server;
- `?lang=it` è la query string, usata per passare parametri al server;
- `#sezione` è il fragment, cioè un riferimento a una specifica porzione della risorsa, interpretato lato client.

Non tutte queste parti sono sempre presenti: in molti URL ne compaiono solo alcune, ma la struttura generale è comunque sempre questa. È importante osservare che HTTP, in quanto protocollo, lavora soprattutto su host, porta, path ed eventuale query string; il fragment, invece, è gestito direttamente dal browser.

##### 06.05.06. Funzionamento generale del World Wide Web

Quando un utente digita un URL nel browser, oppure clicca su un link, si svolge in modo automatico una sequenza di passi piuttosto standard:

1. il browser estrae dall'URL il nome dell'host e, se necessario, lo risolve in indirizzo IP tramite DNS;
2. apre una connessione di rete (di solito TCP) verso il server, sulla porta indicata, o sulla porta di default (che nel caso di HTTP è la porta 80);
3. costruisce una richiesta HTTP coerente con l'URL e la invia al server;
4. il server riceve la richiesta, la elabora e produce una risposta HTTP, contenente uno stato e, di solito, dei dati;
5. il browser riceve la risposta, la interpreta e, se è una pagina HTML, può accorgersi che servono ulteriori risorse (immagini, fogli di stile, script) e ripetere il procedimento per ciascuna di esse.

In sintesi, anche se all'utente sembra di "aprire una pagina" in modo unitario, dietro le quinte il browser sta effettuando molte richieste HTTP coordinate, spesso verso server diversi.

##### 06.05.07. Connessione TCP utilizzata da HTTP

HTTP è un protocollo di livello application che, nella sua forma classica, si appoggia a TCP come protocollo di trasporto. Questa scelta è dovuta al fatto che il Web ha bisogno di una consegna affidabile e ordinata: una pagina HTML, un'immagine, o un file scaricato non hanno senso se mancano dei byte, oppure se arrivano fuori ordine.

Il funzionamento è il seguente: prima di poter scambiare messaggi HTTP, client e server devono aprire una connessione TCP, tipicamente sulla porta 80 per HTTP e sulla porta 443 per HTTPS. Sopra questa connessione viaggiano poi le richieste e le risposte HTTP.

Quando una pagina richiede molte risorse, l'efficienza con cui vengono gestite queste connessioni TCP diventa molto importante, come vedremo parlando di connessioni persistenti.

##### 06.05.08. Modello request/response di HTTP

HTTP è un protocollo di tipo request/response. Questo significa che la comunicazione è organizzata in modo molto regolare:

- il client invia una richiesta al server;
- il server invia una risposta al client.

Per ogni richiesta corrisponde sempre una risposta, e mai il contrario: il server non può inviare messaggi al client se questo non li ha richiesti. Questa caratteristica rende HTTP semplice da capire, da implementare e da analizzare, ma introduce anche alcuni limiti che le versioni più recenti del protocollo cercano di superare.

Inoltre, nella sua forma classica HTTP è stateless: il server non mantiene di per sé memoria delle richieste precedenti dello stesso client. Lo stato delle conversazioni, quando serve, viene ricostruito con meccanismi aggiuntivi come i cookie.

##### 06.05.09. Struttura di una richiesta HTTP

Una richiesta HTTP è un messaggio testuale composto da tre parti principali:

- una riga iniziale, detta request line, che indica il metodo, l'URL relativo della risorsa e la versione di HTTP;
- una serie di header, formati da coppie "nome: valore", che descrivono ulteriori informazioni;
- un corpo facoltativo, che contiene dati inviati al server (per esempio in un POST, oppure in un PUT).

Un esempio molto schematico è il seguente:

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 ...
Accept: text/html
```

In questo esempio il client chiede la risorsa `/index.html` al server `www.example.com`, usando il metodo `GET` e la versione 1.1 di HTTP.

##### 06.05.10. Struttura di una risposta HTTP

Anche la risposta HTTP è un messaggio testuale composto da tre parti principali:

- una riga iniziale, detta status line, che indica la versione di HTTP, il codice di stato numerico e una breve descrizione testuale;
- una serie di header, che descrivono la risposta e la risorsa restituita;
- un corpo, che contiene i dati veri e propri, come HTML, JSON, immagini e così via.

Un esempio molto schematico è il seguente:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<!doctype html>
<html>
  ...
</html>
```

In questo esempio il server risponde con lo stato `200 OK`, dichiara che il contenuto è HTML lungo 1234 byte, e nel corpo restituisce la pagina richiesta.

##### 06.05.11. Metodi HTTP principali: GET, POST, PUT, DELETE, HEAD

I metodi HTTP indicano l'operazione che il client vuole eseguire sulla risorsa. I principali sono:

- GET: chiede una risorsa al server, senza modificarla. È il metodo più usato per leggere pagine, immagini e dati.
- POST: invia dei dati al server per creare, o elaborare una risorsa. È molto usato per i form e per le API.
- PUT: chiede al server di sostituire (o, in alcuni casi, creare) una certa risorsa con i dati forniti.
- DELETE: chiede al server di eliminare una certa risorsa.
- HEAD: come GET, ma chiede solo gli header della risposta, senza il corpo. È utile per controllare lo stato di una risorsa senza scaricarla.

Esistono anche altri metodi, come OPTIONS, PATCH e TRACE, ma i cinque elencati sono quelli concettualmente più importanti. Da un punto di vista logico, GET e HEAD sono considerati metodi "sicuri" e "idempotenti", PUT e DELETE sono idempotenti ma modificano lo stato, mentre POST può avere effetti non idempotenti.

##### 06.05.12. Codici di stato HTTP

Ogni risposta HTTP contiene un codice di stato numerico a tre cifre che riassume l'esito della richiesta. I codici sono raggruppati in classi:

- 1xx: informativi (utilizzati raramente nelle applicazioni comuni);
- 2xx: successo, ad esempio `200 OK`, `201 Created`, `204 No Content`;
- 3xx: redirezione, ad esempio `301 Moved Permanently`, `302 Found`, `304 Not Modified`;
- 4xx: errore lato client, ad esempio `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`;
- 5xx: errore lato server, ad esempio `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`.

In sintesi, i codici di stato permettono al client di capire rapidamente se la richiesta è andata a buon fine, se serve essere reindirizzati, oppure se si è verificato un errore e di quale tipo.

##### 06.05.13. Header HTTP

Gli header HTTP sono coppie "nome: valore" presenti sia nelle richieste sia nelle risposte e portano informazioni aggiuntive rispetto al corpo del messaggio. Possiamo distinguere alcune categorie tipiche:

- header di richiesta: descrivono il client, le sue preferenze e il contesto, come `Host`, `User-Agent`, `Accept`, `Accept-Language`;
- header di risposta: descrivono il server, o la risorsa restituita, come `Server`, `Date`, `Location`;
- header di entità: descrivono il contenuto trasportato, come `Content-Type`, `Content-Length`, `Content-Encoding`;
- header di controllo: gestiscono caching, connessione e sicurezza, come `Cache-Control`, `Connection`, `Set-Cookie`, `Authorization`.

Non è necessario memorizzare tutti gli header esistenti, ma è importante capire che gran parte della flessibilità di HTTP nasce proprio da questo sistema di metadati ricco ed estendibile.

##### 06.05.14. Connessioni persistenti e non persistenti

Nelle prime versioni di HTTP, ogni richiesta richiedeva l'apertura di una nuova connessione TCP, che veniva chiusa subito dopo la risposta. Questo approccio è detto connessione non persistente. Funziona, ma è poco efficiente, perché caricare una pagina con molte risorse richiede di aprire e chiudere molte connessioni TCP.

Per migliorare le prestazioni è stato introdotto il concetto di connessione persistente: una stessa connessione TCP viene riutilizzata per più richieste e risposte consecutive. In questo modo:

- si riduce il numero di handshake TCP eseguiti;
- si abbassa la latenza percepita dall'utente;
- si sfrutta meglio la banda disponibile.

Le connessioni persistenti sono il comportamento di default a partire da HTTP/1.1 e restano un pilastro anche nelle versioni successive del protocollo.

##### 06.05.15. Cookie e gestione delle sessioni

Come abbiamo detto, HTTP è di per sé stateless. Tuttavia, moltissime applicazioni Web hanno bisogno di mantenere uno stato tra una richiesta e l'altra, ad esempio per ricordare l'utente che si è autenticato, oppure il contenuto di un carrello. Per questo motivo è stato introdotto il meccanismo dei cookie.

Un cookie è una piccola informazione che il server invia al client tramite l'header `Set-Cookie`. Il browser memorizza il cookie e lo rimanda al server, nell'header `Cookie`, in tutte le richieste successive verso lo stesso dominio. In questo modo il server può:

- riconoscere lo stesso utente in richieste diverse;
- mantenere una sessione applicativa;
- offrire funzionalità personalizzate.

Naturalmente i cookie sollevano anche questioni di privacy e sicurezza, soprattutto quando vengono usati per il tracciamento degli utenti tra siti diversi.

##### 06.05.16. Autenticazione HTTP

HTTP supporta anche meccanismi di autenticazione, con cui il server può richiedere al client di dimostrare la propria identità prima di accedere a certe risorse. In modo molto semplificato:

- il client invia una richiesta a una risorsa protetta;
- il server risponde con il codice `401 Unauthorized` e indica nello header `WWW-Authenticate` lo schema di autenticazione richiesto;
- il client invia una nuova richiesta includendo le credenziali nell'header `Authorization`;
- se le credenziali sono valide, il server fornisce la risorsa.

Tra gli schemi più noti ricordiamo Basic, Digest e Bearer (usato soprattutto con token come quelli OAuth, o JWT). Spesso, però, nelle applicazioni Web moderne l'autenticazione viene gestita anche tramite form, cookie di sessione e meccanismi misti, che vanno oltre i semplici schemi nativi di HTTP.

##### 06.05.17. Proxy e caching HTTP

Tra un browser e un server Web possono trovarsi diversi intermediari, in particolare i proxy e le cache. Un proxy HTTP è un componente che si pone in mezzo nella comunicazione, ricevendo le richieste dal client e inoltrandole al server, e ricevendo le risposte dal server e restituendole al client. I proxy possono svolgere ruoli diversi:

- filtraggio e controllo del traffico;
- anonimizzazione del client;
- caching delle risorse, per servire più rapidamente le richieste successive.

Il caching HTTP è particolarmente importante per le prestazioni del Web. Le risorse possono essere memorizzate in cache:

- dal browser (cache locale);
- da proxy intermedi;
- da reti di distribuzione, come le CDN.

Header come `Cache-Control`, `Expires`, `ETag` e `Last-Modified` permettono di controllare in modo fine quando una risorsa è considerata ancora valida e quando, invece, deve essere richiesta nuovamente al server di origine.

##### 06.05.18. HTTPS e TLS

HTTPS (HTTP Secure) non è un protocollo separato, ma è semplicemente HTTP trasportato sopra un canale sicuro fornito da TLS (Transport Layer Security). In pratica, prima di scambiare i messaggi HTTP, client e server stabiliscono una sessione TLS, all'interno della quale i messaggi vengono cifrati e autenticati.

I vantaggi principali di HTTPS sono:

- riservatezza, perché il contenuto delle comunicazioni non è leggibile da intermediari;
- integrità, perché eventuali manomissioni dei messaggi possono essere rilevate;
- autenticazione del server, grazie ai certificati X.509 verificati da autorità di certificazione.

Oggi HTTPS è di fatto lo standard del Web: la stragrande maggioranza dei siti moderni lo usa per impostazione predefinita e i browser segnalano come non sicuri i siti che usano ancora solo HTTP.

##### 06.05.19. Differenze tra HTTP/1.0, HTTP/1.1, HTTP/2 e HTTP/3

Nel tempo HTTP è stato aggiornato più volte per migliorarne prestazioni e funzionalità. In modo molto schematico:

- HTTP/1.0: versione storica, basata su connessioni non persistenti e funzionalità di base;
- HTTP/1.1: introduce connessioni persistenti, pipelining (poco usato in pratica), gestione più ricca degli header, virtual hosting tramite l'header `Host` e migliori meccanismi di caching;
- HTTP/2: mantiene la stessa semantica di HTTP/1.1 (stessi metodi, stessi codici di stato, stessi header), ma cambia profondamente il formato dei messaggi, introducendo multiplexing di più richieste su una sola connessione TCP, compressione degli header e gestione più efficiente delle dipendenze tra risorse;
- HTTP/3: mantiene ancora la stessa semantica, ma cambia il livello di trasporto, abbandonando TCP a favore di QUIC, un protocollo costruito sopra UDP che integra cifratura e multiplexing in modo nativo.

L'evoluzione mostra una tendenza chiara: aumentare le prestazioni e ridurre la latenza, mantenendo per quanto possibile la stessa semantica applicativa, così che le applicazioni esistenti non debbano essere riscritte.

##### 06.05.20. Concetti base di REST

REST (REpresentational State Transfer) è uno stile architetturale che descrive come si possono progettare servizi Web in modo coerente con i principi del Web e di HTTP. Pur non essendo un protocollo, REST influenza molto fortemente il modo in cui oggi si progettano le API Web.

I principi fondamentali di REST possono essere riassunti così:

- ogni elemento manipolato è una risorsa, identificata in modo univoco da un URL;
- le operazioni sulle risorse vengono espresse tramite i metodi HTTP standard (GET, POST, PUT, DELETE, ...);
- le comunicazioni sono stateless: ogni richiesta contiene tutte le informazioni necessarie alla sua elaborazione;
- le risposte possono essere rappresentate in formati diversi, come JSON, XML, oppure HTML;
- l'architettura è client/server, layered e cache-friendly.

In sintesi, REST cerca di sfruttare al meglio HTTP non come semplice canale di trasporto, ma come vero linguaggio per descrivere operazioni su risorse.

##### 06.05.21. API Web e servizi RESTful

Una API (Application Programming Interface) Web è un insieme di endpoint, accessibili tramite HTTP, che permettono ad applicazioni diverse di interagire tra loro in modo programmato. Quando un'API segue i principi di REST viene detta API RESTful.

Un'API RESTful è organizzata tipicamente intorno al concetto di risorsa: per esempio, in un'applicazione di gestione utenti potrebbero esistere endpoint come:

- `GET /utenti` per ottenere la lista degli utenti;
- `GET /utenti/42` per ottenere i dettagli dell'utente con ID 42;
- `POST /utenti` per creare un nuovo utente;
- `PUT /utenti/42` per aggiornare l'utente 42;
- `DELETE /utenti/42` per eliminarlo.

I dati viaggiano spesso in formato JSON, sia nelle richieste sia nelle risposte. Questo modello è oggi alla base di moltissimi servizi Web, applicazioni mobile e piattaforme cloud, ed è probabilmente il principale motivo per cui HTTP è andato ben oltre il suo ruolo originario di protocollo per la sola navigazione di pagine.

In conclusione, HTTP non è soltanto il protocollo del Web "delle pagine", ma è anche il protocollo che, di fatto, sta alla base di gran parte delle comunicazioni applicative su Internet, dai siti tradizionali alle moderne API REST.

### 06.06. Streaming audio e video e RTP (Real Time Protocol)

Le applicazioni multimediali, come audio e video, hanno caratteristiche molto diverse rispetto al trasferimento di file, o alla navigazione Web: producono e consumano flussi continui di dati, con un volume elevato e, soprattutto, con vincoli temporali. In pratica, ciò che conta non è solo che i dati arrivino correttamente, ma che arrivino in tempo utile per essere riprodotti.

Lo streaming audio/video consiste proprio nel trasmettere e riprodurre questi contenuti man mano che vengono ricevuti, senza dover aspettare il download completo del file. Si distingue tipicamente tra streaming live, in cui il contenuto viene generato e trasmesso in tempo reale (per esempio una diretta sportiva, o una videoconferenza), e streaming on-demand, in cui il contenuto è già registrato e l'utente può iniziare a guardarlo, o ascoltarlo in qualunque momento (per esempio video su piattaforme di intrattenimento).

Le applicazioni real-time hanno requisiti temporali stringenti: ogni pacchetto deve arrivare entro una finestra di tempo precisa, altrimenti diventa inutile. I parametri critici sono la latenza, cioè il ritardo end-to-end tra invio e riproduzione; il jitter, cioè la variazione del ritardo tra pacchetti successivi; e la perdita di pacchetti, che si traduce in glitch audio, oppure in artefatti visivi. Una perdita moderata può essere tollerata, ma jitter e ritardi eccessivi compromettono la fruizione.

Per mascherare jitter e piccoli ritardi si usa il buffering: il ricevitore accumula una piccola quantità di dati prima di iniziare la riproduzione, in modo da avere una scorta che assorbe le oscillazioni della rete. Più grande è il buffer, più la riproduzione risulta stabile, ma aumenta anche la latenza percepita; per questo lo streaming live usa buffer piccoli, mentre lo streaming on-demand può permettersene di più grandi.

Lo streaming può appoggiarsi a protocolli diversi a seconda del contesto. Per il Web e per molte piattaforme on-demand si usano spesso protocolli basati su HTTP (e quindi su TCP), come HLS e MPEG-DASH, che trasportano video segmentato. Per le comunicazioni real-time e bidirezionali, invece, si usa tipicamente RTP sopra UDP, perché TCP introdurrebbe ritardi inaccettabili a causa delle ritrasmissioni.

RTP (Real-time Transport Protocol) è il protocollo standard del livello application per il trasporto di flussi audio e video in tempo reale. RTP non garantisce di per sé consegna affidabile, ordine, né tempi: fornisce però le informazioni necessarie a un ricevitore per ricostruire correttamente il flusso, gestendo ordine temporale, sincronizzazione e identificazione del tipo di contenuto.

Un pacchetto RTP è formato da un header e da un payload. L'header contiene campi come la versione, il payload type (che indica il tipo di codec usato), un sequence number, un timestamp, un SSRC (Synchronization Source) che identifica univocamente la sorgente del flusso, ed eventuali CSRC per flussi mixati. Il payload contiene i dati multimediali veri e propri, codificati secondo il codec dichiarato.

Il sequence number serve al ricevitore per accorgersi di pacchetti mancanti, o fuori ordine. Il timestamp, invece, indica il momento di campionamento del payload nel flusso: insieme al sequence number permette al ricevitore di riordinare i pacchetti e di riprodurli al ritmo corretto, indipendentemente dalle variazioni di rete.

La sincronizzazione audio/video viene gestita confrontando i timestamp di flussi diversi (per esempio un flusso audio e un flusso video associati alla stessa scena). RTP usa lo stesso meccanismo di timestamp e l'identificatore SSRC per riconoscere le sorgenti e per mantenere il labiale e il sonoro allineati durante la riproduzione.

Accanto a RTP lavora RTCP (RTP Control Protocol), un protocollo di controllo che scambia periodicamente informazioni sullo stato della trasmissione: statistiche sul numero di pacchetti inviati e ricevuti, perdite, jitter osservato, identificazione delle sorgenti. RTCP non trasporta i dati multimediali, ma permette a mittente e ricevitore di adattare il comportamento (per esempio il bitrate del codec) in base alla qualità reale del canale.

Il vincolo temporale dello streaming si lega direttamente al concetto di QoS (Quality of Service): lo streaming funziona bene quando la rete è in grado di garantire banda sufficiente, ritardo contenuto, jitter basso e perdita ridotta. Per questo nelle reti gestite si usano spesso meccanismi di prioritizzazione del traffico real-time, come DiffServ e classi di servizio dedicate.

I dati audio e video, prima di essere trasmessi, vengono compressi tramite codec. I codec audio (Opus, AAC, MP3, G.711) e i codec video (H.264, H.265, VP9, AV1) riducono drasticamente il bitrate necessario, sfruttando la ridondanza temporale e percettiva dei segnali. Il payload type di RTP indica al ricevitore quale codec deve usare per decodificare correttamente il payload.

Un'applicazione classica di RTP è il VoIP (Voice over IP), cioè la trasmissione della voce su rete IP. In una telefonata VoIP, il flusso audio viene codificato, pacchettizzato in RTP, trasportato sopra UDP e ricostruito al ricevitore con l'aiuto di un piccolo buffer di jitter; RTCP fornisce statistiche di qualità, mentre protocolli di segnalazione come SIP (o H.323) si occupano di stabilire, modificare e terminare la chiamata.

Lo streaming adattivo, usato soprattutto in HLS e MPEG-DASH, divide il video in piccoli segmenti disponibili a più qualità (bitrate, risoluzione) diverse. Il client misura le condizioni della rete e sceglie dinamicamente il segmento più adatto, alzando, o abbassando la qualità durante la riproduzione per evitare interruzioni. È un meccanismo molto efficace per ambienti eterogenei come Internet.

WebRTC (Web Real-Time Communication) è un insieme di tecnologie e API che porta lo streaming real-time direttamente nei browser, senza bisogno di plugin esterni. Si basa su RTP/RTCP per il trasporto dei media, usa codec moderni e include meccanismi per superare NAT e firewall (ICE, STUN, TURN). È alla base di applicazioni di videoconferenza e di comunicazione peer-to-peer nel browser.

Nella pratica, RTP è usato in moltissime applicazioni reali: telefonia IP, videoconferenze, dirette in streaming, sistemi di videosorveglianza IP, comunicazioni interattive su WebRTC e numerose piattaforme di collaborazione. Pur non essendo visibile all'utente, RTP è di fatto il protocollo che rende possibile il trasporto efficiente dei media in tempo reale su Internet.

### 06.07. Server farm e CDN (Content Delivery Network)

Quando un servizio Internet deve servire molti utenti, distribuiti geograficamente, un solo server non basta. Per questo si usano infrastrutture composte da molti server e da reti di distribuzione dei contenuti.

##### 06.07.01. Necessità di scalabilità nei servizi Internet

I servizi Internet moderni devono gestire un numero molto grande di utenti contemporanei, con picchi di traffico imprevedibili. Un singolo server non è sufficiente: serve un'infrastruttura scalabile, in grado di crescere all'aumentare della domanda e di restare disponibile anche in caso di guasti.

##### 06.07.02. Concetto di server farm

Una server farm è un insieme di server connessi tra loro che cooperano per fornire lo stesso servizio. All'esterno il sistema appare come un'unica entità, ma internamente il carico viene distribuito tra molte macchine.

##### 06.07.03. Data center e infrastrutture server

Le server farm sono ospitate in data center, cioè edifici specializzati che forniscono alimentazione ridondata, raffreddamento, connettività di rete e sicurezza fisica. Un data center può contenere migliaia di server organizzati in rack.

##### 06.07.04. Bilanciamento del carico (load balancing)

Il load balancing distribuisce le richieste in arrivo tra i server di una farm, evitando che alcuni siano sovraccarichi mentre altri restano inutilizzati. Criteri tipici: round robin, server meno carico, vicinanza geografica, sessione utente.

##### 06.07.05. Load balancer hardware e software

Il load balancer è il componente che applica la politica di distribuzione. Può essere un dispositivo dedicato (hardware), oppure un componente software in esecuzione su server generici. Spesso opera a livello applicativo (es. HTTP) o a livello di trasporto.

##### 06.07.06. Alta disponibilità e fault tolerance

L'alta disponibilità è la capacità del servizio di restare operativo nel tempo; la fault tolerance è la capacità di continuare a funzionare anche in presenza di guasti. Si ottengono con ridondanza di server, link di rete, alimentazione e dati.

##### 06.07.07. Clustering di server

Un cluster è un insieme di server che lavorano in modo coordinato per condividere carico, o stato. Se un nodo cade, gli altri continuano a servire le richieste, garantendo continuità del servizio.

##### 06.07.08. Replica dei contenuti

La replica consiste nel mantenere copie identiche dei contenuti su più server. Permette load balancing, ridondanza e accesso più rapido. Richiede meccanismi per mantenere le copie coerenti.

##### 06.07.09. Problemi di latenza geografica

Anche con server potenti, la distanza fisica tra utente e server introduce latenza non trascurabile. Un utente in Europa che accede a un server negli USA paga sempre un costo minimo dovuto alla velocità di propagazione del segnale.

##### 06.07.10. Concetto di CDN (Content Delivery Network)

Una CDN è una rete di server distribuiti geograficamente che replica e serve contenuti il più vicino possibile all'utente finale. Riduce la latenza, alleggerisce il server di origine e migliora prestazioni e affidabilità.

##### 06.07.11. Edge server

Gli edge server sono i server della CDN posti ai bordi della rete, vicini agli utenti. Servono direttamente le richieste, attingendo ai propri contenuti in cache e contattando il server di origine solo quando necessario.

La seguente figura mostra l'idea generale di una CDN:

<!-- to add -->
*In Figura: un server di origine e una rete di edge server distribuiti geograficamente che servono gli utenti finali*

##### 06.07.12. Distribuzione geografica dei contenuti

I contenuti vengono replicati su più edge server sparsi nel mondo. Ogni utente viene servito dall'edge più vicino, riducendo distanza, latenza e carico sul backbone.

##### 06.07.13. Caching nelle CDN

Gli edge server mantengono in cache i contenuti richiesti più di frequente. La prima richiesta provoca un fetch dal server di origine, mentre le successive vengono servite localmente. La validità è gestita con TTL e header HTTP di caching.

##### 06.07.14. CDN statiche e dinamiche

Le CDN statiche servono contenuti che cambiano raramente (immagini, video, file CSS, JS), facilmente replicabili. Le CDN dinamiche gestiscono anche contenuti personalizzati per utente, usando tecniche di accelerazione, pre-fetch e route optimization verso l'origine.

##### 06.07.15. DNS-based redirection

Una tecnica diffusa per indirizzare l'utente all'edge migliore è basata sul DNS: la risoluzione del nome restituisce un IP diverso a seconda della posizione del client, dirigendolo all'edge server più conveniente.

##### 06.07.16. Anycast routing

Con l'anycast, lo stesso indirizzo IP è annunciato da più edge server in luoghi diversi. La rete instrada il pacchetto verso l'istanza più vicina secondo le metriche di routing, ottenendo selezione automatica dell'edge a livello network.

##### 06.07.17. Ottimizzazione delle prestazioni Web

Le CDN migliorano le prestazioni Web non solo via caching, ma anche con compressione, ottimizzazione delle immagini, HTTP/2 e HTTP/3, riuso di connessioni TLS e tecniche di pre-fetch verso l'origine.

##### 06.07.18. CDN e streaming multimediale

Lo streaming audio/video, soprattutto su larga scala, è uno degli usi principali delle CDN. La replica geografica e il caching degli edge sono essenziali per servire contemporaneamente molti utenti con bassa latenza.

##### 06.07.19. Sicurezza nelle CDN

Le CDN offrono anche funzioni di sicurezza: terminazione TLS, protezione da attacchi DDoS, filtraggio del traffico, web application firewall e mitigazione di attacchi a livello applicativo, sfruttando la capacità distribuita della rete.

##### 06.07.20. Esempi di CDN commerciali

Esempi noti di CDN commerciali sono Cloudflare, Akamai, Amazon CloudFront, Fastly e Google Cloud CDN. Sono ampiamente usate da siti, applicazioni mobile e piattaforme di streaming per scalabilità globale.

### 06.08. Altri protocolli del livello application

Oltre ai protocolli principali visti finora, il livello application include molti altri protocolli che, pur essendo meno noti all'utente comune, svolgono ruoli essenziali nel funzionamento quotidiano di Internet e dei sistemi distribuiti.

IMAP (Internet Message Access Protocol) è un protocollo per l'accesso alla posta elettronica memorizzata su un mail server remoto. A differenza di altri approcci, IMAP non scarica i messaggi sul client per poi rimuoverli dal server, ma li mantiene sul server e permette al client di consultarli, organizzarli in cartelle, marcarli come letti, o cercarli, mantenendo lo stato sincronizzato tra più dispositivi. Si appoggia a TCP, usa la porta 143 in chiaro e la porta 993 sopra TLS (IMAPS) e supporta operazioni online, offline e disconnesse.

POP3 (Post Office Protocol version 3) è un protocollo più semplice e storicamente più datato per la consultazione della posta. Il modello tipico è scarica e (di default) cancella: il client si connette al server, scarica i messaggi nuovi sulla macchina locale e di solito li rimuove dal server. POP3 si appoggia a TCP, usa la porta 110 in chiaro e la porta 995 sopra TLS (POP3S); è ancora supportato per compatibilità, ma è oggi largamente superato da IMAP, perché meno adatto all'uso da più dispositivi e alla gestione lato server della posta.

SSL/TLS (Secure Socket Layer / Transport Layer Security) è il principale protocollo di sicurezza usato sopra il livello di trasporto per cifrare, autenticare e proteggere le comunicazioni tra client e server. SSL è il nome storico (oggi deprecato per gravi vulnerabilità), mentre TLS è il nome moderno, con versioni che vanno fino a TLS 1.3. TLS fornisce riservatezza tramite cifratura simmetrica, integrità tramite codici MAC, o AEAD, e autenticazione tramite certificati X.509 e una PKI basata su autorità di certificazione. Viene usato per HTTPS, SMTP/IMAP/POP3 sicuri, FTPS, VPN e molti altri protocolli, ed è di fatto il pilastro della sicurezza applicativa su Internet.

NFS (Network File System) è un protocollo che permette a un host di accedere a file remoti come se fossero locali, montando un file system esportato da un server. Sviluppato originariamente da Sun Microsystems e ampiamente diffuso in ambiente Unix/Linux, NFS realizza un file system distribuito trasparente per le applicazioni: operazioni come read, write, open, stat vengono trasmesse al server tramite RPC (Remote Procedure Call). Le versioni moderne (NFSv4 e successive) integrano funzionalità di sicurezza, gestione dello stato e supporto a meccanismi di autenticazione e cifratura come Kerberos.

NTP (Network Time Protocol) è il protocollo standard per la sincronizzazione degli orologi tra host in rete. Si basa su un'architettura gerarchica a strati (stratum): allo stratum 0 ci sono sorgenti di tempo molto precise (orologi atomici, ricevitori GPS), allo stratum 1 i server direttamente collegati a queste sorgenti, e a strati successivi server che si sincronizzano dai livelli superiori. NTP usa UDP sulla porta 123 e impiega un algoritmo che stima ritardo e offset tra client e server per correggere l'orologio locale con precisione tipicamente nell'ordine dei millisecondi sulla rete pubblica. Una sincronizzazione affidabile del tempo è fondamentale per autenticazione, certificati, logging coerente, sistemi distribuiti e protocolli di sicurezza.

IRC (Internet Relay Chat) è uno dei più antichi protocolli di messaggistica testuale in tempo reale su Internet. È basato su un modello client/server in cui gli utenti si connettono a un server IRC e partecipano a canali, identificati dal carattere `#`, all'interno dei quali si scambiano messaggi pubblici, oppure aprono conversazioni private. IRC si appoggia a TCP, tradizionalmente sulla porta 6667 (e su porte sicure come 6697 sopra TLS), supporta operatori di canale, comandi di amministrazione e meccanismi di federazione tra server. Pur essendo stato in larga parte sostituito da piattaforme di chat moderne, IRC è ancora attivamente usato in molte comunità tecniche e open source.