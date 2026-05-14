# 03. Datalink Layer

### 03.01. Introduzione
<!-- to do -->

##### 03.01.01. Panoramica del datalink layer dello stack TCP/IP
<!-- to do -->

##### 03.01.02. Responsabilità e servizi forniti dal datalink layer
<!-- to do -->

##### 03.01.03. Tipi di collegamenti: end-to-end e broadcast
<!-- to do -->

##### 03.01.04. Architettura IEEE 802
<!-- to do -->

##### 03.01.05. Introduzione ai sottolivelli LLC (Logic-Link Control) e MAC (Media Access Control)
<!-- to do -->

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