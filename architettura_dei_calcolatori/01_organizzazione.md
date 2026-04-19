# 01. Organizzazione

### 01.01. Processore

**CPU (Central Processing Unit)**: dal punto di vista logico, una CPU e' il cervello di un sistema digitale. E' l'hardware dedicato al calcolo e all'esecuzione delle istruzioni. Spesso il termine "CPU" non viene usato per indicare il chip hardware del computer, cioe' il processore o microprocessore, ma viene usato per indicare l'unita' di elaborazione del sistema dal punto di vista logico. Dal punto di vista logico, una CPU e' composta dai seguenti sottocomponenti:

- **CU (Control Unit)**: un componente interno al processore che coordina i segnali da e verso la CPU.
- **ALU (Arithmetic-Logic Unit)**: un componente interno al processore che esegue calcoli ed elabora uno, due o piu' operandi.
- **Registri**: piccole memorie installate direttamente nello stesso chip dell'ALU e della CU. L'ALU puo' accedere direttamente e rapidamente a ciascun registro. Ogni registro ha una capacita' limitata, spesso compresa tra 8 e 512 bit, cioe' tra 1 e 64 byte.

Usiamo il termine "CPU" per indicare una generica unita' di elaborazione dal punto di vista logico; puo' essere un processore, un processore single-core, un processore multi-core oppure un sistema multicomputer.

**Data Path**: l'ALU di un processore e' un componente altamente strutturato. L'ALU e' organizzata come un *data path*, cioe' un percorso seguito dai dati durante l'esecuzione di una specifica istruzione. Il data path parte dai registri, dove vengono memorizzati gli operandi e i risultati parziali, prelevati e inseriti nei bus dell'ALU. I bus dell'ALU sono tipicamente chiamati bus A e bus B e, talvolta, esiste un terzo bus chiamato bus C. L'ALU ha due o tre registri in ingresso: il bus A trasporta il primo operando, operando A, da un registro al primo ingresso dell'ALU; il bus B trasporta il secondo operando, operando B, da un registro al secondo ingresso dell'ALU. I sistemi dotati di bus C hanno un'ALU che accetta un terzo operando, operando C, e questo bus trasporta il terzo operando da un registro al terzo ingresso dell'ALU.

La figura seguente rappresenta due tipi di data path:

<!-- da aggiungere -->
*In figura - Sul lato sinistro: un data path con bus A e bus B, ALU con due operandi. Sul lato destro: un data path con bus A, bus B e bus C, ALU con tre operandi*

Dopo che l'ALU esegue l'istruzione corrente del programma, memorizzata nella memoria centrale, il risultato viene salvato nel registro di uscita dell'ALU. Per esempio, se l'istruzione corrente e' la somma tra gli operandi A, B e C, il registro di uscita dell'ALU contiene il risultato `A + B + C`. Un altro bus dell'ALU trasporta l'uscita dell'istruzione corrente verso uno specifico registro oppure in una specifica locazione della memoria centrale, a seconda dell'istruzione eseguita.

**Registri**: un registro e' una memoria piccola e veloce collocata vicino all'ALU. Le moderne ALU hanno diversi tipi di registri:

- **PC (Program Counter)**: un registro puntatore relativo che indica la prossima istruzione da prelevare ed eseguire. Ogni volta che una nuova istruzione viene prelevata per l'esecuzione, il PC viene incrementato di uno. Esistono istruzioni che permettono al programma di aggiungere al PC un offset diverso da 1, per esempio nel caso dell'istruzione di salto.
- **IR (Instruction Register)**: contiene l'istruzione corrente nella fase di esecuzione. Un'istruzione puo' avere zero, uno, due o piu' operandi.
- **ACC (ACCumulator)**: un registro contatore, oppure accumulatore, usato da una o piu' istruzioni.
- **GPRs (General Purpose Registers)**: registri di lavoro usati per memorizzare operandi e risultati parziali. I GPR seguono una nomenclatura specifica: tipicamente ogni registro e' chiamato `Rn`, dove `n` e' un numero che parte da 0 e arriva fino al numero di GPR installati nel chip meno uno. Per esempio, se la CPU ha 64 GPR, detti anche registri di lavoro, esistono registri da `R0` a `R63`.
- **Registro A**: l'operando A dell'ALU.
- **Registro B**: l'operando B dell'ALU.
- **Registro C**: l'operando C dell'ALU, per ALU che possono operare con piu' di due operandi simultaneamente.
- **Registro di stato**, oppure *flags register*: un registro in cui ogni bit indica una specifica situazione dopo l'esecuzione dell'ultima istruzione. Un registro di stato e' composto dai seguenti flag:
  - **Zero flag (Z)**: `Z = 1` se l'ultima istruzione restituisce 0, altrimenti `Z = 0`.
  - **Carry flag (C)**: `C = 1` se l'ultima istruzione restituisce un risultato con riporto, altrimenti `C = 0`.
  - **Sign flag (S)**: `S = 1` se l'ultima istruzione restituisce un numero negativo, altrimenti `S = 0`.
  - **Overflow flag (O)**: `O = 1` se l'ultima istruzione ha causato un overflow, altrimenti `O = 0`.
  - **Parity flag (P)**: `P = 1` se l'ultimo risultato e' un numero dispari, altrimenti `P = 0`.
- **MAR (Memory Address Register)**: memorizza l'indirizzo della locazione di memoria a cui la CPU vuole accedere. E' usato durante le operazioni di lettura e scrittura.
- **MDR (Memory Data Register)**, oppure **MBR (Memory Buffer Register)**: memorizza i dati trasferiti verso o dalla memoria. Anche questo registro e' usato durante le operazioni di lettura e scrittura.

**Ciclo fetch-decode-execution**: il ciclo macchina, chiamato anche ciclo fetch-decode-execution, e' un ciclo continuamente eseguito dall'hardware della CPU. Il ciclo macchina consiste nell'eseguire i seguenti passi, nell'ordine indicato:

1. **IF (Instruction Fetch)**: prelevare dalla memoria principale la prossima istruzione, indicata dal registro PC.
2. **PCI (Program Counter Increment)**: incrementare il PC, in modo che punti all'istruzione successiva.
3. **ID (Instruction Decode)**: decodificare l'istruzione considerando il suo opcode. Un opcode, *operation code*, e' un codice univoco di una particolare architettura che indica il tipo di istruzione.
4. **OPF (OPerands Fetch)**: se l'istruzione corrente richiede uno, due o piu' operandi dalla memoria principale, in questa fase la CPU preleva tutti gli operandi.
5. **EXE (EXEcute, oppure EXEcution)**: l'ALU esegue l'istruzione prelevata usando gli operandi prelevati.
6. **WB (Write Back)**: dopo il calcolo, l'ALU salva dapprima il risultato nel registro di uscita, poi un bus della CPU trasporta il risultato verso un GPR.
7. **MEM (MEMory, oppure MEMory write)**: se il risultato e' un risultato finale, viene memorizzato nella memoria principale.

In realta', il ciclo macchina non e' necessariamente eseguito continuamente dall'hardware del sistema. Per esempio, nel linguaggio Java esiste una macchina virtuale chiamata JVM, *Java Virtual Machine*, che esegue il ciclo macchina tramite software.

**Processore**: e' il chip installato nel computer. Il termine "processore" e' tipicamente usato per indicare il chip fisico del sistema. Un processore possiede pin e segnali propri, ma esistono vari standard che descrivono come il processore debba comunicare con le altre periferiche del sistema. Un processore e' chiamato anche microprocessore, noto anche come `uP`.

**Core, processore single-core, processore multi-core e multicomputer**: un core e' un'unita' di elaborazione indipendente all'interno di un processore, capace di eseguire istruzioni autonomamente. Ogni core puo' prelevare istruzioni direttamente dalla memoria centrale, eseguire calcoli, per esempio con numeri interi o in virgola mobile, eseguire programmi e gestire task del sistema operativo. Un processore con un solo core puo' eseguire un solo task alla volta; un processore con due core puo' eseguire due task in parallelo; un processore con `N` core puo' idealmente eseguire `N` task in parallelo. Piu' core permettono al computer di gestire programmi simultaneamente e in modo piu' fluido.

Un processore puo' essere:

- **Single-Core**: ha una sola unita' di esecuzione installata sul chip. Intel Pentium III e Intel Pentium 4 sono esempi di processori single-core.
- **Dual-Core**: ha due unita' di esecuzione installate sul chip. Intel Core 2 Duo e AMD Athlon 64 X2 sono esempi di processori dual-core.
- **Multi-Core**: ha piu' di due unita' di esecuzione installate sul chip. Intel Xeon Clearwater Forest, con 288 core, e AMD EPYC 9965 Zen 5 Dense Cores, con 192 core, sono due processori che supportano un elevato livello di parallelismo con alcuni dei piu' alti numeri di core oggi esistenti.

Un processore con due o piu' core e' chiamato processore multi-core. Un processore con un solo core e' chiamato processore single-core, oppure semplicemente processore. Se un sistema ha due o piu' processori, intesi come piu' chip processore collegati tra loro, allora e' chiamato multicomputer. Un multicomputer permette di ottenere un grado di parallelismo molto maggiore.

L'immagine seguente rappresenta due tipi di sistema: un processore con singolo core e un processore con piu' core.

<!-- da aggiungere -->
*In figura: un processore single-core e un processore multi-core*

**Processori fortemente accoppiati**: un sistema fortemente accoppiato consiste di due o piu' processori con memoria condivisa. Ogni processore tipicamente lavora con la stessa istruzione oppure con gli stessi dati, e cio' da' origine a diverse modalita' di esecuzione parallela nello stesso sistema:

- **SISD (Single Instruction, Single Data)**: usato fondamentalmente da un processore che esegue la propria istruzione con i propri dati.
- **SIMD (Single Instruction, Multiple Data)**: in cui piu' processori eseguono la stessa istruzione su insiemi di dati differenti. Questo modello e' tipicamente usato da GPU, *Graphic Processing Unit*, oppure da TPU, *Tensor Processing Unit*.
- **MISD (Multiple Instruction, Single Data)**: molto simile al precedente; in questo contesto piu' processori eseguono istruzioni differenti considerando lo stesso insieme di dati. E' tipico nei sistemi di simulazione oppure nell'esecuzione di grandi calcoli.
- **MIMD (Multiple Instruction, Multiple Data)**: questo e' il massimo grado di parallelismo tra due o piu' processori, in cui ogni processore esegue il proprio programma con i propri dati. I sistemi multi-core usano MIMD.

Nella figura seguente e' rappresentata la GPU Nvidia Fermi, un esempio di modello SIMD:

<!-- da aggiungere -->
*In figura: la GPU Nvidia Fermi, che segue il modello SIMD, Single Instruction Multiple Data*

**Processori debolmente accoppiati**: un sistema debolmente accoppiato consiste di processori con memorie locali separate, collegati tramite una rete di comunicazione, come mostrato nella figura seguente:

<!-- da aggiungere -->
*In figura: un esempio di processori debolmente accoppiati, cioe' un multicomputer*

In un sistema debolmente accoppiato ogni processore ha il proprio ciclo di vita e la propria memoria. Ogni processore puo' eseguire la propria istruzione e il proprio programma senza interferire con gli altri. Non esiste una memoria globale condivisa e ogni processore opera in modo indipendente. I sistemi debolmente accoppiati sono facilmente scalabili e adatti alle architetture parallele. Esempi di sistemi debolmente accoppiati sono i sistemi distribuiti, i sistemi di cloud computing e i supercomputer. Un processore debolmente accoppiato e' sostanzialmente un sistema multicomputer.

**RISC (Reduced Instruction Set Computer)**: e' un tipo di ISA, *Instruction Set Architecture*, con un numero ridotto di istruzioni. La filosofia alla base dell'approccio RISC e' molto semplice: ogni istruzione dovrebbe essere il piu' semplice possibile e dovrebbe essere eseguita il piu' velocemente possibile, con il minor numero di cicli di clock possibile. Tipicamente, in una ISA RISC, ogni istruzione ha uno o due operandi; e' difficile avere istruzioni con piu' di due operandi in un'architettura RISC. Spesso le architetture RISC hanno al massimo 128 oppure 256 istruzioni; inoltre ogni opcode e' progettato per essere il piu' semplice possibile da interpretare. Tutte le istruzioni seguono lo stesso formato e hanno la stessa lunghezza, in numero di bit o di byte, raramente superiore a 16, 32 oppure 64 bit. Compilatori e interpreti dei linguaggi di programmazione svolgono un ruolo importante nell'ottimizzazione del codice. RISC consente tipicamente una bassa complessita' hardware. Per esempio, l'immagine seguente mostra la ISA RISC ARMv7-A:

<!-- da aggiungere -->
*In figura: un esempio di ISA ARMv7-A*

**CISC (Complex Instruction Set Computer)**: e' un tipo di ISA con un numero molto alto di istruzioni. La filosofia alla base dell'approccio CISC e' questa: ogni istruzione deve essere il piu' indipendente possibile e il piu' vicina possibile al modo di pensare umano. Un'architettura CISC riduce il divario tra il livello macchina e il livello umano. Tipicamente, in una ISA CISC, ogni istruzione ha uno, due o piu' operandi; alcune istruzioni possono avere tre, quattro o piu' operandi. Le architetture CISC hanno un numero elevato di istruzioni, 512 oppure 1024 in alcune architetture. Sfortunatamente, le architetture CISC non migliorano l'ottimizzazione hardware; al contrario, spesso l'hardware della CPU e dell'ALU e' piu' complesso dell'hardware richiesto da un'architettura RISC. In un'architettura CISC esistono formati diversi e lunghezze diverse, e un'istruzione puo' facilmente raggiungere anche 64, 128 oppure 256 byte. Ogni istruzione puo' essere eseguita in un numero maggiore di cicli di clock, spesso 4, 8, 16 o piu' per le istruzioni piu' complesse. Intel 8088, come Intel Core i9, e' un esempio di architettura CISC. L'immagine seguente mostra i vari formati della ISA 8088:

<!-- da aggiungere -->
*In figura: diversi formati della ISA Intel 8088*

**HISC (Hybrid Instruction Set Computer)**: un'architettura ibrida usa sia ISA CISC sia ISA RISC per trovare un compromesso tra semplicita' e indipendenza delle istruzioni. Le architetture moderne, incluse Intel e AMD, usano un'architettura RISC per le istruzioni piu' comuni e frequentemente usate, come `ADD`, `MOV`, `SUB`, `MUL`, `DIV`, `JMP` e altre, e usano un'architettura CISC per le istruzioni piu' complesse, per esempio alcune istruzioni vettoriali o alcuni calcoli in virgola mobile. Questo compromesso si colloca a meta' tra architetture RISC pure e architetture CISC pure: HISC e' piu' veloce di CISC ma piu' lento di RISC.

**Architettura NUMA (Non-Uniform Memory Access)**: e' un'architettura usata per sistemi multiprocessore e per processori fortemente accoppiati in cui il tempo di accesso alla memoria dipende dalla sua posizione e dalla distanza dal processore che vi accede. La figura seguente mostra come e' organizzato un sistema NUMA con quattro processori:

<!-- da aggiungere -->
*In figura: un sistema NUMA con quattro processori*

NUMA e' l'evoluzione naturale dell'architettura UMA, *Uniform Memory Access*, in cui esiste un solo chip di memoria principale e il tempo di accesso e' uguale per tutti i processori installati nel sistema. La figura seguente mostra come e' organizzato un sistema UMA con quattro processori:

<!-- da aggiungere -->
*In figura: un sistema UMA con quattro processori*

Come si puo' vedere, un'architettura NUMA con `N` processori ha anche `N` chip di memoria, uno per ogni processore. Ogni processore accede alla propria memoria tramite un bus di memoria dedicato ad alta velocita' di trasferimento. Tutti i processori di un'architettura NUMA sono collegati con un bus comune e ogni processore puo' accedere a un'altra memoria tramite il bus comune, inviando un messaggio a un altro processore; in questo caso c'e' maggiore latenza. Se il lavoro tra tutti i processori e' coordinato bene da un arbitro centralizzato, l'architettura NUMA permette maggiore banda passante rispetto all'architettura UMA; inoltre NUMA e' ottimizzata per applicazioni real-time e time-critical.

**Architettura SMP (Symmetric Multi-Processor)**: e' un'architettura in cui esiste una memoria globale, memoria principale o memoria centrale, condivisa da tutti i processori: ogni processore puo' accedere alla memoria condivisa tramite un bus comune, chiamato anche bus di sistema. Esiste un arbitro centralizzato che raccoglie le richieste di accesso fatte da tutti i processori. Secondo una politica specifica, come una politica FIFO, *First In, First Out*, ogni richiesta viene accettata e soddisfatta dall'arbitro del bus. Tra il bus di sistema e il processore e' presente una cache. Ogni processore possiede la propria cache, che puo' essere unificata oppure separata in cache dati e cache istruzioni. L'architettura SMP e' un esempio di sistema multiprocessore fortemente accoppiato, perche' esiste un'unica memoria condivisa. La figura seguente rappresenta l'organizzazione di un'architettura SMP:

<!-- da aggiungere -->
*In figura: organizzazione di un'architettura SMP*

**Architettura AMP (Asymmetric Multi-Processor)**: e' un sistema multiprocessore in cui i processori non hanno ruoli uguali: un processore, chiamato master, controlla il sistema, mentre gli altri processori, chiamati slave, eseguono compiti specifici assegnati. Il processore master controlla il sistema operativo, pianifica i task, gestisce l'I/O e gestisce gli interrupt di sistema e di programma. I processori slave eseguono i calcoli assegnati e non eseguono direttamente il sistema operativo. Ogni slave puo' eseguire un programma diverso. La comunicazione avviene spesso tramite memoria condivisa oppure tramite scambio di messaggi attraverso un bus comune. I programmi tipicamente eseguiti dagli slave sono calcoli grafici, elaborazione dei segnali e applicazioni orientate all'utente. La figura seguente mostra come e' organizzata un'architettura AMP:

<!-- da aggiungere -->
*In figura: organizzazione di un'architettura AMP*

**Parallelismo reale ed emulato**: per parallelismo emulato intendiamo l'impressione che l'utente ha dell'attivita' svolta dal computer. Il processore potrebbe non supportare parallelismo a livello hardware, ma la sua velocita' di esecuzione e l'elevata frequenza di clock gli permettono di eseguire piu' programmi in tempi molto brevi, anche uno alla volta e con frequenti cambi di contesto. Per parallelismo reale intendiamo invece un sistema che puo' effettivamente gestire l'esecuzione simultanea, o concorrente, di piu' programmi in esecuzione, per esempio avendo piu' core hardware, oppure supportando thread hardware e usando tecniche come il pipelining. Esistono sostanzialmente due tipi di parallelismo reale: ILP, *Instruction-Level Parallelism*, e PLP, *Processor-Level Parallelism*:

- **ILP (Instruction-Level Parallelism)**: e' una forma di parallelismo reale che funziona eseguendo simultaneamente piu' istruzioni all'interno di un singolo processore. Tecniche utili di ILP sono pipeline, architetture superscalari, esecuzione out-of-order, *register renaming* ed esecuzione speculativa.
- **PLP (Processor-Level Parallelism)**: e' una forma di parallelismo reale che funziona eseguendo task simultaneamente su piu' processori o piu' core. Le architetture che supportano PLP sono processori multi-core, processori vettoriali e registri vettoriali, SMP, AMP, NUMA, sistemi distribuiti, cluster e cloud computing.

**Clock di sistema**: il clock di sistema e' un circuito digitale che usa un opportuno hardware, tipicamente un oscillatore ad anello oppure un oscillatore al quarzo, per generare un segnale digitale, periodico e ciclico. Il segnale digitale alterna continuamente un'alta tensione, 1.2 V, 3.3 V oppure 5 V, e una bassa tensione, `-5 V` oppure `0 V`. Il clock di sistema e' il circuito piu' importante dei sistemi digitali sincroni, come un computer, perche' definisce i vari istanti in cui ogni componente esegue il proprio compito. La figura seguente mostra come e' strutturato un clock di sistema:

<!-- da aggiungere -->
*In figura: un esempio di clock di sistema*

La frequenza e' il parametro chiave di un clock di sistema: definisce i cicli di clock in un secondo. I moderni sistemi digitali hanno clock di sistema di 4 GHz o piu', il che significa che il clock di sistema ha un periodo di `1 / 4 000 000 000` secondi, cioe' `0.25 ns`, dove `ns = 10^(-9)` secondi. Il clock di sistema e' il circuito piu' "veloce" del sistema, poiche' marca i vari istanti temporali in cui ciascuna periferica svolge il proprio compito. Ricorda che il periodo, indicato con `T` oppure `P`, e' l'inverso della frequenza, misurata in Hz, *Hertz*, e indicata con `f`:

$$
f = \frac{1}{T}
$$

$$
T = \frac{1}{f}
$$

Per esempio, il processore Intel Core i9 9900 ha una frequenza di base di 3.1 GHz, cioe' un periodo di `1 / 3 100 000 000` secondi, pari a `0.323 ns`, ma con Turbo Boost il clock di sistema puo' essere aumentato a 5 GHz, con un periodo di `1 / 5 000 000 000` secondi, cioe' `0.2 ns`.

**Gerarchia di memoria**: i moderni sistemi digitali, come computer, server e smartphone, hanno piu' memorie a cui la CPU puo' accedere per trovare dati da elaborare e istruzioni da eseguire. Fondamentalmente, esistono cinque categorie di memoria che si possono trovare in un moderno dispositivo digitale:

- **Registri**: memorie piccole e molto veloci installate direttamente nello stesso chip dell'ALU. Sono molto vicine alla CPU e fanno parte del data path. Il tempo di accesso e' quasi istantaneo: spesso l'ALU puo' accedere simultaneamente a uno o piu' registri in 1 ns. E' difficile stimare quanti registri abbia una CPU: dipende da come il chip e' stato costruito e dal tipo di architettura.
- **Memoria cache**: e' la categoria di memoria piu' piccola in termini di dimensione del chip e capacita', non piu' grande di qualche decina di MB. Una cache e' organizzata in vari livelli, alcuni dei quali sono collocati direttamente nello stesso chip della CPU o addirittura all'interno di ciascun core nei sistemi multi-core. Il tempo di accesso e' molto basso, dell'ordine di pochi ns, o al massimo 20 ns.
- **Memoria primaria**, oppure **memoria principale**: rappresenta un giusto compromesso tra dimensione del chip e capacita' fornita, normalmente tra 512 MB e 64 GB, o piu' nei server e nei cluster. Tipicamente la memoria principale piu' comune e' chiamata RAM, acronimo di *Random Access Memory*, a indicare che l'accesso ai dati e' rapido e indipendente dalla posizione. Il costo per GB e' alto, ma il tempo di accesso e' ancora basso, dell'ordine di 20 ns, o al massimo 60 ns.
- **Memoria secondaria**, oppure **memoria di memorizzazione**: queste memorie hanno una dimensione del chip maggiore e una capacita' compresa tra 128 GB e 1 TB. Due delle memorie di memorizzazione piu' comuni sono SSD, *Solid State Disk*, e HD, *Hard Disk*. Oggi gli SSD hanno ampiamente superato le prestazioni degli HDD, fornendo tempi di accesso dell'ordine di qualche centinaio di ns circa. Gli HDD, invece, offrono tempi di accesso molto piu' lenti, poiche' si basano su parti meccaniche oltre che elettriche, e possono raggiungere fino a diversi millisecondi. Il costo per GB e' medio per SSD e basso per HD. Il tempo di accesso e' alto o molto alto, dell'ordine di 100 ns per SSD o fino a 20 ms per HD.
- **Memoria terziaria**, oppure **memoria esterna**: queste memorie hanno una dimensione del chip maggiore e una capacita' compresa tra 128 GB e 1 TB, simile alla memoria secondaria. Sia SSD sia HD possono essere usati come memorie esterne e le prestazioni sono praticamente le stesse. Il costo per GB e' medio per SSD e basso per HD. Il tempo di accesso e' ancora molto alto, dell'ordine di 20 ns oppure fino a 60 ns. Possono essere usati anche altri tipi di memoria, come CD, *Compact Disk*, DVD, *Digital Versatile Disk*, Blu-Ray, chiavette USB e cosi' via.

La figura seguente mostra la gerarchia di memoria:

<!-- da aggiungere -->
*In figura: come e' organizzata la gerarchia di memoria*

Come si puo' vedere osservando la figura precedente, esistono alcuni parametri di una memoria che variano man mano che ci si sposta dal basso verso l'alto, oppure viceversa, nella gerarchia di memoria:

- **Tempo di accesso**: scendendo nella gerarchia aumenta progressivamente. Questo significa che i registri sono significativamente piu' veloci della memoria principale, che a sua volta e' molto piu' veloce delle memorie secondarie ed esterne.
- **Capacita' di memorizzazione**: scendendo nella gerarchia aumenta progressivamente. Questo significa che i registri sono significativamente piu' piccoli della memoria principale, che a sua volta e' molto piu' piccola delle memorie secondarie ed esterne.
- **Costo per bit**: scendendo nella gerarchia diminuisce progressivamente. Questo significa che le memorie principali sono significativamente piu' costose delle memorie secondarie o esterne.

### 01.02. Memoria cache

**Cache**: e' una memoria molto veloce con bassa capacita', tipicamente realizzata con tecnologia SRAM, *Static Random Access Memory*. La SRAM e' un tipo di memoria semiconduttrice volatile che memorizza dati usando circuiti bistabili flip-flop, tipicamente implementati con 6 transistor per cella, una cella per bit. La SRAM non richiede refresh periodico, il che la rende piu' veloce ma piu' costosa e meno densa. Fornisce bassa latenza di accesso e alta velocita'; per questo motivo e' comunemente usata per le cache e non per le memorie principali. Tuttavia, la SRAM consuma piu' area di silicio e ha un costo per bit piu' elevato. Una cache puo' essere unificata oppure separata. Una cache unificata contiene sia dati sia istruzioni, mentre una cache separata e' divisa in due cache: la cache istruzioni contiene le istruzioni che la CPU sta eseguendo.

**Livelli di cache**: la memoria cache e' organizzata in livelli e ogni livello fornisce una specifica capacita' e una specifica dimensione. Normalmente, un comune computer ha tre livelli di cache: L1, L2 e L3. Sistemi piu' costosi e piu' potenti possono avere fino a sette livelli di cache, da L1 a L7. I primi tre livelli di una cache sono organizzati in questo modo:

- **Cache L1**, oppure semplicemente **L1**: e' collocata nel chip di ciascun processore oppure nel chip di ciascun core. Ogni unita' di calcolo possiede la propria L1. La L1 fornisce un tempo di accesso piu' rapido, ma al prezzo di una dimensione piu' piccola, tipicamente tra 16 KB e 128 KB per core. Le L1 piu' comuni sono cache separate: esistono una L1d, per i dati, e una L1i, per le istruzioni.
- **Cache L2**, oppure semplicemente **L2**: e' collocata nel chip del processore, raramente nel chip di ciascun core, il che significa che nei sistemi multi-core puo' esistere una sola L2 condivisa da tutti i core. Ogni unita' di calcolo possiede comunque la propria L1. Le L2 piu' comuni sono cache unificate. La L2 fornisce un tempo di accesso piu' lento della L1, ma con una dimensione maggiore, tipicamente tra 256 KB e 2 MB.
- **Cache L3**, oppure semplicemente **L3**: e' collocata fuori dal chip del processore, ma molto vicina ad esso. Ogni unita' di calcolo condivide una L3. Le L3 sono tipicamente cache unificate. La L3 fornisce un tempo di accesso piu' lento della L2, ma con una dimensione maggiore, tipicamente tra 2 MB e 128 MB.

**Principi di localita' temporale e spaziale**: cache e memoria principale funzionano sulla base di due principi fondamentali:

- **Principio di localita' temporale**: se una locazione di memoria viene acceduta una volta, e' probabile che venga acceduta di nuovo nel prossimo futuro.
- **Principio di localita' spaziale**: se una locazione di memoria viene acceduta, e' probabile che locazioni vicine vengano accedute presto.

Rispettare questi due principi significa avere una maggiore coerenza tra cache e memoria principale, garantendo un accesso rapido a dati o istruzioni da parte della CPU e un uso efficiente della memoria.

**Cache hit e cache miss**: quando una CPU genera un indirizzo di memoria gia' presente in uno dei livelli di cache, L1, L2 o L3, si verifica un *cache hit*. Un cache hit si verifica quando la CPU richiede dati gia' presenti nella cache, accedendovi quindi in tempi molto brevi. Al contrario, quando la CPU richiede dati che non sono gia' presenti nella cache, la richiesta viene propagata alla memoria principale, oppure al livello successivo della cache: in questo caso si verifica un *cache miss*. Cache hit e cache miss sono molto importanti per controllare le prestazioni della cache. Da queste due situazioni derivano i seguenti parametri prestazionali delle cache:

- **Hit Ratio**: e' un numero compreso tra `0` e `1`, cioe' una percentuale, che rappresenta il rapporto tra cache hit e cache miss. Un valore vicino a `1` rappresenta un alto numero di cache hit, e conseguentemente pochi cache miss; un valore vicino a `0` rappresenta molti cache miss, e conseguentemente pochi cache hit. Indichiamo l'hit ratio con `r`. Se indichiamo il numero totale di cache hit con `h` e il numero totale di cache miss con `m`, allora l'hit ratio si calcola con la formula `r = h / (h + m)`. Normalmente, le cache moderne raggiungono valori di `r` compresi tra 95%, cioe' `0.95`, e 100%, cioe' `1.00`.
- **Miss Rate**: e' un numero compreso tra `0` e `1`, cioe' una percentuale, che rappresenta il rapporto tra cache miss e cache hit. Dal punto di vista concettuale, e' l'inverso dell'hit ratio. Un valore vicino a `1` rappresenta molti cache miss, e conseguentemente pochi cache hit; un valore vicino a `0` rappresenta molti cache hit, e conseguentemente pochi cache miss. Indichiamo il miss rate con `l`. Se indichiamo il numero totale di cache hit con `h` e il numero totale di cache miss con `m`, allora il miss rate si calcola con la formula `l = m / (m + h)`. Normalmente, le cache moderne raggiungono valori di `l` compresi tra 5%, cioe' `0.05`, e 0%, cioe' `0.00`. Un altro modo per calcolare il miss rate e' `l = 1 - r` e, in modo simile, un altro modo per calcolare l'hit ratio e' `r = 1 - l`.
- **Hit Time**: e' il tempo richiesto per accedere ai dati dalla memoria cache quando il dato richiesto e' gia' presente nella cache, cioe' in caso di cache hit. Normalmente, un cache hit si risolve in pochi nanosecondi.
- **Miss Penalty**: e' il tempo aggiuntivo richiesto per recuperare i dati dal livello successivo della gerarchia di memoria, L2, L3 oppure memoria principale, quando il dato richiesto non viene trovato nella cache, cioe' in caso di cache miss.

**AMAT (Average Memory Access Time)**: e' molto complesso da calcolare, ma possiamo provare a considerare una formula semplice. Possiamo considerare la seguente gerarchia di memoria, indicando per ciascuna memoria il tempo di accesso:

- **Cache**, con i seguenti livelli:
  - **L1**, realizzata con tecnologia SRAM. `tl1` e' il tempo di accesso, `ml1` e' il miss rate.
  - **L2**, realizzata con tecnologia SRAM. `tl2` e' il tempo di accesso, `ml2` e' il miss rate.
  - **L3**, realizzata con tecnologia SRAM. `tl3` e' il tempo di accesso, `ml3` e' il miss rate.
- **Memoria principale**, realizzata con tecnologia DRAM. `tmm` e' il tempo di accesso, `mmm` e' il miss rate.
- **Due memorie secondarie**:
  - la prima e' un SSD, realizzato con tecnologia NAND flash. `tssd` e' il tempo di accesso, `mssd` e' il miss rate;
  - la seconda e' un HD, realizzato con tecnologie sia VLSI sia meccaniche. `thd` e' il tempo di accesso.

La CPU puo' accedere alle varie memorie nel seguente ordine:

```text
CPU -> L1 -> L2 -> L3 -> Main Memory -> SSD -> HDD
```

Queste sono le formule di base dell'AMAT in funzione di dove si trova il dato richiesto:

- Dato memorizzato in L1: `tl1`
- Dato memorizzato in L2: `tl1 + (ml1 * tl2)`
- Dato memorizzato in L3: `tl1 + (ml1 * (tl2 + (ml2 * tl3)))`
- Dato memorizzato nella memoria principale: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * tmm)))))`
- Dato memorizzato nell'SSD: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * (tmm + (mmm * tssd)))))))`
- Dato memorizzato nell'HD: `tl1 + (ml1 * (tl2 + (ml2 * (tl3 + (ml3 * (tmm + (mmm * (tssd + (mssd * thd)))))))))`

Come si puo' vedere, quanto piu' complessa e' la gerarchia di memoria, tanto piu' lungo diventa il tempo medio di accesso alla memoria.

**Linee di cache**: una linea di cache e' l'unita' base di dati trasferita tra cache e memoria principale ed e' identificata usando tre campi di indirizzo: *tag*, *index* e *offset*. L'index seleziona il set di cache, oppure la linea, in cui il dato puo' trovarsi; il **tag** identifica se il blocco di memoria richiesto e' presente in quella posizione; l'offset seleziona il byte o la word specifica all'interno della linea di cache. Questi campi vengono estratti dall'indirizzo di memoria per consentire una ricerca e un accesso rapidi nella cache.

**Strategie di mapping**: le strategie di mapping della cache determinano come i blocchi di memoria vengano collocati nelle linee di cache. Nelle cache direct-mapped, ogni blocco di memoria viene mappato in una sola linea di cache, rendendo l'accesso veloce ma aumentando i conflict miss. Nelle cache set-associative, ogni blocco puo' essere collocato in una qualsiasi linea all'interno di un set selezionato, bilanciando flessibilita' e complessita' hardware. Nelle cache fully associative, un blocco di memoria puo' essere collocato in qualsiasi linea di cache, riducendo al minimo i conflict miss ma richiedendo meccanismi hardware di ricerca piu' complessi e piu' lenti.

**Strategie di sostituzione**: le strategie di sostituzione della cache determinano quale linea di cache viene rimpiazzata quando un nuovo blocco di memoria deve essere caricato e la cache, oppure il set, e' gia' pieno. La scelta della strategia influisce sulle prestazioni della cache influenzando il miss rate. Le strategie piu' comuni sono:

- **FIFO (First In, First Out)**: sostituisce la linea di cache che e' rimasta nella cache per il tempo piu' lungo. E' semplice da implementare ma non considera quanto frequentemente o recentemente i dati siano stati usati, e questo puo' diminuire l'hit ratio, oppure equivalentemente aumentare il miss rate.
- **LRU (Least Recently Used)**: sostituisce la linea di cache che non e' stata acceduta per il tempo piu' lungo. Sfrutta la localita' temporale e in generale offre prestazioni migliori di FIFO, ma richiede maggiore complessita' hardware.
- **Random Replacement**: seleziona casualmente una linea di cache da sostituire. E' semplice e veloce da implementare e puo' funzionare abbastanza bene nella pratica.
- **LFU (Least Frequently Used)**: sostituisce la linea di cache che e' stata acceduta il minor numero di volte. Tiene traccia della frequenza di utilizzo ma e' piu' complessa da implementare ed e' meno comune nelle cache hardware.
- **Pseudo LRU**: un'approssimazione di LRU usata nei processori moderni per ridurre la complessita' hardware mantenendo prestazioni vicine a LRU. E' la tecnica piu' usata nei moderni sistemi digitali.

**Strategie di scrittura**: in una politica *write-through*, ogni operazione di scrittura aggiorna simultaneamente sia la cache sia la memoria principale. Questo garantisce consistenza della memoria e semplifica la coerenza, ma aumenta il traffico di memoria e puo' ridurre le prestazioni a causa di operazioni di scrittura piu' lente. In una politica *write-back*, oppure *copy-back*, le operazioni di scrittura aggiornano inizialmente solo la cache, e i dati modificati, cioe' i blocchi dirty, vengono scritti nella memoria principale solo quando vengono sostituiti. Questo riduce il traffico di memoria e migliora le prestazioni, ma richiede hardware aggiuntivo per tracciare le linee di cache modificate. In una politica *write-allocate*, quando si verifica un write miss, il corrispondente blocco di memoria viene prima caricato nella cache e poi aggiornato. Questa strategia e' comunemente usata insieme alle cache write-back perche' e' probabile che in futuro si verifichino altre scritture sullo stesso blocco, localita' temporale. In una politica *no write-allocate*, quando si verifica un write miss, il dato viene scritto direttamente nella memoria principale senza caricare il blocco nella cache. Questo riduce l'inquinamento della cache ed e' tipicamente usato insieme alle cache write-through.

Ci sarebbe molto altro da dire sulle cache, ma purtroppo non c'e' abbastanza spazio per parlarne. Rimandiamo a testi piu' approfonditi.

### 01.03. Memoria primaria
<!-- da fare - RAM (Random Access Memory), SRAM (Static RAM) e DRAM (Dynamic RAM) -->
<!-- da fare - organizzazione delle celle di memoria: bit, nibble, byte, half-word, word -->
<!-- da fare - memoria come matrice vs memoria come array di byte -->
<!-- da fare - definizione di indirizzo di memoria -->
<!-- da fare - memoria byte-addressing e word-addressing -->
<!-- da fare - ordinamento dei byte: big endian vs little endian -->
<!-- da fare - problematiche tra sistemi big endian e little endian -->
<!-- da fare - EDC (Error Detection Codes): bit di parita' unidimensionale, bit di parita' bidimensionali, checksum, CRC (Cyclic Redundant Code) -->
<!-- da fare - ECC (Error Correction Codes): distanza di Hamming, codici di Hamming per SEC (Single Error Correction), codici di Hamming per SEC-DED, chipkill ECC, codici BCH (Bose-Chaudhuri-Hocquenghem), codici Reed-Solomon -->
<!-- da fare - package di memoria: SIMM (Single Inline Memory Module), DIMM (Dual Inline Memory Module) e SO-DIMM (Small Outline DIMM) -->

### 01.04. Memoria secondaria
<!--
da fare - memoria NAND: SSD (Solid State Disk)
    - memoria flash basata su NAND
    - memoria flash basata su NOR
    - principio del transistor a gate flottante
    - meccanismo di memorizzazione della carica
    - struttura: pagine, blocchi, piani, die e canali
    - SLC (Single-Level Cell) e MLC (Multi-Level Cell)
    - parametri prestazionali: endurance, latenza, densita' e affidabilita'
    - errori nelle memorie NAND, gestione dei bad block, wear leveling e garbage collection
-->
<!-- da fare - HD (Hard Disk)
    - principio di memorizzazione magnetica
    - concetto di memorizzazione non volatile
    - struttura fisica: piatti, spindle, testine di lettura/scrittura, braccio attuatore, tracce, settori, cilindri
    - formato dei settori, LBA (Logical Block Addressing), ZBR (Zone Bit Recording)
    - geometria logica e fisica del disco
    - parametri prestazionali: seek time, rotational latency, access time, data transfer rate, throughput
    - interfacce: IDE, SATA, SCSI e SAS
    - errori negli HD: gestione dei bad sector e sistema SMART di monitoraggio
    - caching: read caching, write caching e prefetching
-->
<!-- da fare - RAID (Redundant Array Of Independent Disks)
    - che cos'e' un RAID?
    - hardware RAID e software RAID
    - concetti di data striping e data mirroring
    - concetto di parity, parity-based redundancy e distributed parity
    - RAID livello 0
    - RAID livello 1
    - RAID livello 2
    - RAID livello 3
    - RAID livello 4
    - RAID livello 5
    - RAID livello 6
    - livelli RAID annidati: RAID 0+1, RAID 1+0, RAID 50 e RAID 60
    - parametri prestazionali: prestazioni in lettura, prestazioni in scrittura, parity update penalty, rebuild time, latenza e throughput
    - tolleranza ai guasti: MTTF (Mean Time To Failure), MTTR (Mean Time To Repair), processo di rebuild, hot spare disks
-->
<!-- da fare - CD (Compact Disk)
    - principio della memorizzazione ottica
    - struttura fisica: substrato in policarbonato, strato riflettente, strato protettivo, struttura a traccia spirale, pits e lands
    - struttura logica: frame, blocchi, indirizzamento logico e file system ISO 9660
    - parametri prestazionali: CLV (Constant Linear Velocity), access time, seek time, rotational latency, data transfer rate, capacita' standard e limiti di densita' fisica
    - errori nei CD: CIRC (Cross-Interleaved Reed-Solomon Code) e tecniche di interleaving
    - CD-ROM (CD - Read Only Memory)
    - CD-R (CD - Recordable)
    - CD-RW (CD - Re-Writable)
    - CD-DA (CD - Digital Audio)
-->
<!-- da fare - DVD (Digital Versatile Disk)
    - struttura fisica: strati di substrato in policarbonato, strato riflettente, strato protettivo, struttura dual-layer, dischi single-sided vs double-sided, struttura a traccia spirale, pits e lands
    - struttura logica: settori, blocchi, LBA (Logical Block Addressing), UDF (Universal Disk Format) e file system ISO 9660
    - formati: DVD-ROM, DVD-R, DVD+R, DVD-RW, DVD+RW, DVD-RAM, DVD-Video e DVD-Audio
    - errori nei DVD: RSPC (Reed-Solomon Product Code) e tecniche di interleaving
    - parametri prestazionali: access time, seek time, rotational latency, data transfer rate
    - SLSS (Single Layer, Single Sided)
    - DLSS (Dual Layer, Single Sided)
    - SLDS (Single Layer, Double Sided)
    - DLDS (Dual Layer, Double Sided)
-->
<!-- da fare - Blu-Ray Disk
    - concetto di memorizzazione ad alta densita'
    - struttura fisica: substrato in policarbonato, strato riflettente, rivestimento protettivo hard-coat, struttura single-layer, struttura dual-layer, dischi multi-layer, struttura a traccia spirale, pits e lands
    - struttura logica: settori, blocchi, LBA (Logical Block Addressing) e UDF (Universal Disk Format)
    - rappresentazione dei bit: codifica ottica dei bit, channel bits, lunghezza d'onda del laser, miglioramento dell'apertura numerica, spaziatura ad alta densita' delle tracce
    - formati: BD-ROM, BD-R, BD-RE, BDXL, BD-Video e BD-Audio
    - parametri prestazionali: access time, seek time, rotational latency e data transfer rate
    - single-layer, double-layer, triple-layer e quad-layer
-->

### 01.05. Dispositivi di I/O

**Tastiere**: esistono diversi tipi di tastiere:

- Le tastiere meccaniche usano uno switch individuale per ogni tasto che chiude direttamente un contatto elettrico quando viene premuto.
- Le tastiere a membrana rilevano la pressione dei tasti usando strati conduttivi flessibili premuti uno contro l'altro.
- Le tastiere a cupola di gomma usano cupole in silicone che collassano collegando le tracce del circuito.
- Le tastiere a scissor-switch usano un meccanismo a forbice di stabilizzazione sopra un livello di contatto a membrana.
- Le tastiere capacitive rilevano la pressione dei tasti misurando variazioni di capacita' invece di chiudere contatti elettrici.

**Mouse**: esistono diversi tipi di mouse:

- I mouse meccanici rilevano il movimento usando una sfera di gomma che ruota rulli interni collegati a sensori di posizione.
- I mouse optomeccanici migliorano il rilevamento meccanico usando il rilevamento ottico di ruote encoder in rotazione.
- I primi mouse ottici rilevano il movimento usando tappetini con griglie predefinite.
- I moderni mouse ottici usano un LED e un sensore d'immagine per seguire il movimento della texture della superficie.
- I mouse laser funzionano come i mouse ottici ma usano un diodo laser invece di un LED.
- I mouse wireless trasmettono i dati di movimento senza cavi usando protocolli di comunicazione a corto raggio.
- I mouse touch-based rilevano il movimento delle dita usando sensori capacitivi invece del tracciamento meccanico del movimento.

**Monitor**: esistono diversi tipi di monitor.

Un monitor **CRT** funziona lanciando fasci di elettroni dal fondo del tubo verso uno schermo rivestito di fosfori per produrre immagini. I fasci scandiscono lo schermo riga per riga per creare l'immagine. I display CRT sono ingombranti, consumano piu' energia e oggi sono in gran parte obsoleti.

Un monitor **LCD** usa cristalli liquidi posti tra strati di vetro per controllare la luce proveniente da una retroilluminazione e formare immagini sullo schermo. E' piu' sottile, piu' leggero e piu' efficiente dal punto di vista energetico rispetto ai display CRT. La tecnologia LCD e' ampiamente usata in laptop, monitor e televisori.

Un monitor **LED** e' in realta' un monitor LCD che usa diodi ad emissione luminosa come retroilluminazione al posto delle lampade fluorescenti. Questo migliora luminosita', contrasto ed efficienza energetica, permettendo anche design piu' sottili. I monitor LED sono comuni negli schermi moderni.

Un monitor **OLED** usa composti organici che emettono luce quando attraversati da corrente elettrica, quindi non e' necessaria alcuna retroilluminazione. Ogni pixel produce la propria luce, permettendo contrasti molto elevati, neri profondi e tempi di risposta rapidi. I display OLED sono usati in smartphone, TV e monitor di fascia alta.

Un **plasma display** usa piccole celle riempite di gas elettricamente carico che emettono luce ultravioletta quando vengono attivate, eccitando poi i fosfori per produrre immagini. Gli schermi al plasma offrono buona riproduzione dei colori e ampi angoli di visione, ma consumano piu' energia e sono piu' pesanti di LCD e LED. Oggi sono per lo piu' dismessi.

**Stampanti**: esistono diversi tipi di stampanti.

Una **inkjet printer** produce immagini spruzzando minuscole gocce di inchiostro liquido sulla carta attraverso ugelli microscopici. E' comunemente usata per la stampa domestica e d'ufficio perche' puo' produrre immagini a colori di alta qualita' a costi relativamente bassi. Le stampanti inkjet sono adatte per documenti e stampa fotografica.

Una **bubble-jet printer** e' un tipo di stampante inkjet che usa il calore per creare piccole bolle nell'inchiostro, forzando le gocce sulla carta. Questo metodo permette un controllo preciso del posizionamento dell'inchiostro e produce stampe nitide. E' ampiamente usata in molte stampanti inkjet consumer.

Una **laser printer** usa un raggio laser per formare un'immagine elettrostatica su un tamburo rotante, che attrae particelle di toner e le trasferisce sulla carta. Viene poi applicato calore per fissare permanentemente il toner sulla pagina. Le stampanti laser sono veloci e producono testo di alta qualita', rendendole ideali per ambienti d'ufficio.

Una **LED printer** funziona in modo simile a una stampante laser ma usa una fila di diodi ad emissione luminosa invece di un raggio laser per creare l'immagine sul tamburo. Questo progetto ha meno parti mobili e puo' migliorare l'affidabilita'. Le stampanti LED sono efficienti e comunemente usate in ambienti d'ufficio.

Una **direct thermal printer** crea immagini applicando calore direttamente su carta termica appositamente rivestita, che cambia colore quando viene riscaldata. Non richiede inchiostro ne' toner. Queste stampanti sono comunemente usate per ricevute, biglietti ed etichette.

Una **thermal transfer printer** usa il calore per trasferire inchiostro da un nastro su carta o etichette. Questo metodo produce stampe durevoli e di lunga durata che resistono allo sbiadimento. E' comunemente usata per etichette barcode, packaging e applicazioni industriali.

Una **dot-matrix printer** crea caratteri e immagini colpendo un nastro inchiostrato contro la carta usando un insieme di piccoli pin disposti a matrice. E' una stampante a impatto capace di stampare moduli multicopia usando carta copiativa. Le stampanti a matrice di punti sono usate soprattutto in ambienti come quello bancario e logistico, dove e' richiesta la stampa continua su carta.

**Altoparlante**: un altoparlante converte i dati audio digitali del computer in onde sonore analogiche udibili dall'essere umano. Il segnale segue questo percorso:

1. La CPU invia i campioni audio al controller audio, o scheda audio.
2. Il controller audio memorizza i campioni in buffer audio.
3. Un **DAC (Digital-to-Analog Converter)** converte i campioni digitali in una tensione analogica.
4. Un amplificatore aumenta la potenza del segnale.
5. Il diaframma dell'altoparlante vibra e produce onde sonore.

**Fotocamere digitali**: una fotocamera digitale funziona catturando la luce attraverso una lente e focalizzandola su un sensore di immagine, di solito un sensore CMOS oppure CCD. Il sensore converte la luce in ingresso in segnali elettrici che rappresentano la luminosita' e il colore di ciascun pixel dell'immagine. Questi segnali vengono elaborati dal processore interno della fotocamera e convertiti in un file immagine digitale. L'immagine viene poi memorizzata in memoria, come una scheda SD, in modo da poter essere visualizzata, modificata o trasferita ad altri dispositivi.

Un sensore **CMOS (Complementary Metal-Oxide-Semiconductor)** converte la luce in segnali elettrici usando amplificatori a livello di singolo pixel costruiti direttamente nel sensore. Ogni pixel elabora il proprio segnale, permettendo una cattura delle immagini piu' rapida e un consumo energetico piu' basso. I sensori CMOS sono ampiamente usati negli smartphone e nelle moderne fotocamere digitali perche' sono economici da produrre e supportano funzionamento ad alta velocita'. Consentono inoltre di integrare sullo stesso chip funzioni di elaborazione aggiuntive.

Un sensore **CCD (Charge-Coupled Device)** cattura la luce e la converte in cariche elettriche che vengono trasferite attraverso il chip e lette in un angolo del sensore. Questo metodo produce immagini di qualita' molto elevata, con basso rumore ed eccellente sensibilita' alla luce. Tuttavia, i sensori CCD consumano piu' energia e sono piu' lenti rispetto ai sensori CMOS. Erano comunemente usati nelle prime fotocamere digitali e sono ancora impiegati in applicazioni scientifiche e di imaging professionale.

### 01.06. Bus di sistema

**Bus di sistema**: il bus di sistema e' la rete di comunicazione all'interno di un sistema digitale che permette ai vari dispositivi di un computer di comunicare. Un bus di sistema e' un insieme di fili che interconnette CPU, memoria principale e dispositivi di I/O. Un bus di sistema ha diversi tipi di bus:

- **Data bus**: un insieme di linee in cui ogni segnale rappresenta un dato.
- **Address bus**: un insieme di linee in cui ogni segnale rappresenta un indirizzo.
- **Control bus**: un insieme di linee in cui ogni segnale rappresenta un segnale di controllo.

Il bus di sistema ha diversi tipi di standard e protocolli. In generale, il bus all'interno di uno specifico dispositivo di I/O o di uno specifico componente non e' soggetto a standardizzazione, mentre l'interconnessione tra due o piu' dispositivi differenti e' un bus di sistema soggetto a standardizzazione. Uno standard e' un insieme di regole, oppure un insieme di interfacce, che tutti i produttori di dispositivi di I/O, CPU e memorie principali devono rispettare per poter comunicare in modo efficiente. La comunicazione tra due o piu' componenti di un sistema digitale e' soggetta anche a un protocollo. Un protocollo e' un insieme di regole che definisce come i dispositivi comunicano e scambiano dati in un sistema digitale o in una rete.

**Width**: la larghezza di un bus di sistema definisce quante linee parallele possiede un certo tipo di bus. Oggi esistono quattro larghezze principali usate nei piu' comuni sistemi digitali:

- `x8` definisce 8 linee parallele.
- `x16` definisce 16 linee parallele.
- `x32` definisce 32 linee parallele.
- `x64` definisce 64 linee parallele.

In questo caso, "linee parallele" significa che in un singolo ciclo di clock vengono trasferiti simultaneamente 8, 16, 32 oppure 64 bit da un componente a un altro.

**Compatibilita' e problema del disallineamento**: nel tempo, la larghezza di un bus e' stata un problema importante, per esempio per l'architettura Intel x86, che ha attraversato una serie di aumenti nella larghezza del bus indirizzi a partire dal processore 8088:

- Il processore `8088` aveva un bus indirizzi a `20` bit.
- Il processore `80286` aveva un bus indirizzi a `24` bit. `4` di questi bit sono stati aggiunti insieme ad altri bit di controllo per garantire la retrocompatibilita'.
- Il processore `80386` aveva un bus indirizzi a `32` bit. Sono stati aggiunti altri `8` bit, complicando ulteriormente la complessita' della circuiteria di controllo.

La compatibilita' e' un problema concreto: un bus indirizzi multiplexato potrebbe essere una soluzione efficiente.

Una larghezza troppo elevata porta al problema del *bus misalignment*: ogni segnale in una specifica linea del bus ha il proprio ritardo di propagazione e la propria velocita', che varia leggermente. Questo fatto potrebbe portare a lievi disallineamenti del bus, soprattutto quando il ciclo di clock e' molto breve.

**Timing**: ricorda che il clock di sistema e' un segnale digitale, continuo e deterministico, che si ripete sempre e costantemente senza interruzione e che assume sempre la stessa forma d'onda a ogni periodo di clock. Un bus puo' usare il clock di sistema, oppure no.

- Un **bus sincrono** usa un segnale di clock condiviso per coordinare tutte le operazioni tra i componenti collegati, per esempio l'accesso alla memoria in lettura o scrittura. Tutti i dispositivi seguono lo stesso clock e i trasferimenti di dati avvengono a intervalli temporali fissi. Questi tipi di bus di sistema sono piu' facili da progettare e controllare, ma hanno flessibilita' limitata quando i dispositivi hanno velocita' differenti. Esempi di bus sincroni sono l'FSB, *Front-Side Bus*, e il bus delle memorie SDRAM.
- Un **bus asincrono** non usa un clock globale; invece, tutti i dispositivi coordinano i trasferimenti usando segnali di handshaking, come il full handshaking. Non e' richiesto alcun clock di sistema, e ciascun dispositivo coinvolto nella comunicazione lavora con richieste e acknowledge. Questo e' piu' flessibile con dispositivi a velocita' miste. Questo tipo di bus di sistema e' piu' flessibile e ottimizzato per dispositivi con velocita' diverse, ma e' piu' lento dei bus sincroni, a causa dell'overhead dell'handshake. Esempi di bus asincroni sono USB, *Universal Serial Bus*, e PCI, *Peripheral Component Interconnect*.

La figura seguente mostra le differenze tra una comunicazione in un bus sincrono e una in un bus asincrono:

<!-- da aggiungere -->
*In figura: una comunicazione in un bus sincrono, a sinistra, e in un bus asincrono, a destra*

**Arbitraggio**: in un sistema di calcolo, piu' dispositivi, come CPU, memoria principale e dispositivi di I/O, sono tutti collegati a un percorso di comunicazione comune noto come bus di sistema. Per trasferire dati tra questi dispositivi, essi devono ottenere accesso al bus. L'arbitraggio del bus e' il processo di risoluzione dei conflitti che si verificano quando piu' dispositivi tentano di accedere al bus nello stesso momento. Quando piu' dispositivi cercano di usare simultaneamente il bus, questo puo' portare a corruzione dei dati e instabilita' del sistema. Per prevenire questo problema, si usa un meccanismo di arbitraggio del bus per garantire che un solo dispositivo abbia accesso al bus in un dato istante.

L'arbitraggio del bus si riferisce al processo mediante il quale l'attuale *bus master* accede e poi lascia il controllo del bus, passandolo a un'altra unita' processore che lo richiede. Il controllore che ha accesso al bus in un dato istante e' noto come *bus master*. Esistono due tipi di arbitraggio del bus:

- **Arbitraggio centralizzato del bus**: un singolo arbitro del bus, tipicamente un arbitro centrale chiamato master, esegue l'arbitraggio richiesto.
- **Arbitraggio distribuito del bus**: tutti i dispositivi coinvolti nella comunicazione e collegati al bus di sistema partecipano alla selezione del successivo bus master.

Esistono diversi metodi di arbitraggio del bus:

- **Metodo del daisy chaining**: e' un metodo semplice ed economico in cui tutti i bus master usano la stessa linea per fare richieste di bus. Il segnale di grant del bus si propaga serialmente attraverso ogni master finche' incontra il primo che sta richiedendo l'accesso al bus. Questo master blocca la propagazione del segnale di grant, quindi ogni altro modulo richiedente non ricevera' il segnale di grant e non potra' accedere al bus. Ecco il metodo del daisy chaining:

<!-- da aggiungere -->
*In figura: il metodo del daisy chaining per implementare un arbitraggio del bus centralizzato*

- **Metodo di polling**, oppure **priorita' rotante**: in questo metodo il controllore e' usato per generare l'indirizzo del master, cioe' una priorita' univoca; il numero di linee di indirizzo richieste dipende dal numero di master collegati nel sistema. Il controllore genera una sequenza di indirizzi dei master. Quando il master richiedente riconosce il proprio indirizzo, attiva la linea busy e comincia a usare il bus. Ecco il metodo di polling:

<!-- da aggiungere -->
*In figura: il metodo di polling per implementare un arbitraggio del bus distribuito*

- **Metodo a priorita' fissa**, oppure **independent request method**: in questo metodo ogni master ha una coppia separata di linee di richiesta del bus e di concessione del bus, e a ciascuna coppia e' assegnata una priorita'. Il decoder di priorita' integrato nel controllore seleziona la richiesta a priorita' piu' alta e attiva il corrispondente segnale di grant. Ecco il metodo a priorita' fissa:

<!-- da aggiungere -->
*In figura: il metodo a priorita' fissa per implementare un arbitraggio del bus centralizzato*

**Architettura del bus di sistema**: il bus di sistema in un sistema digitale puo' essere organizzato in modi diversi. Esistono tre principali architetture note per il bus di sistema:

- **Architettura a bus singolo**: tutti i componenti condividono un solo bus comune di comunicazione per segnali dati, indirizzi e controllo. Tutte le comunicazioni avvengono sullo stesso e unico bus. Avviene un solo trasferimento alla volta, perche' ogni dispositivo deve usare lo stesso percorso di comunicazione. In questi sistemi e' comunemente presente un arbitro del bus.
- **Architettura a bus multipli**: usa bus separati per differenti compiti di comunicazione. Possono avvenire simultaneamente piu' trasferimenti. Questa architettura e' usata nei processori moderni e nei sistemi orientati alle prestazioni. Di solito usa sia arbitraggio centralizzato sia arbitraggio distribuito.
- **Architettura a bus gerarchico**: in cui ogni componente e' come una foglia oppure una radice di un albero. Tipicamente il componente radice e' la CPU, con una connessione diretta, tramite un bus dedicato, alla memoria principale. Questa architettura e' basata sul bus di espansione, oppure slot di espansione: ogni slot permette all'utente di collegare altri dispositivi di I/O al sistema digitale, creando un sottosistema ad albero.

L'architettura a bus gerarchico e' mostrata nella figura seguente:

<!-- da aggiungere -->
*In figura: un'architettura a bus gerarchico con la CPU come radice dell'albero*

**Parametri prestazionali del bus di sistema**: ecco i principali parametri prestazionali di un bus che determinano quanto velocemente i dati si muovono all'interno di un sistema di calcolo:

- **Width**: la larghezza del bus e' il numero di bit, uno per ogni linea, che possono essere trasferiti simultaneamente sul bus.
- **Latency**: e' il ritardo temporale tra l'invio di una richiesta e la ricezione della risposta.
- **Frequency**: la frequenza del bus e' il numero di cicli di trasferimento al secondo sul bus.
- **Throughput**: e' la quantita' di dati trasferita per secondo sul bus.

**Chipset, northbridge e southbridge**: il chipset e' un insieme di componenti della scheda madre che gestiscono il flusso di dati tra CPU, memoria e dispositivi. Tradizionalmente consiste di due parti: il northbridge, che gestisce la comunicazione ad alta velocita' con CPU, RAM e grafica, e il southbridge, che gestisce funzioni di I/O piu' lente come USB, SATA e audio. La figura seguente mostra la struttura di base del chipset:

<!-- da aggiungere -->
*In figura: northbridge e southbridge*

Il **northbridge** e' uno dei due chip collocati nella direzione Nord sulla scheda madre. La funzione principale del northbridge e' gestire le comunicazioni tra la CPU e parti della scheda madre. Il northbridge e' collegato direttamente verso l'FSB, *Front-Side Bus*. Altri nomi del northbridge sono *host bridge* e **MCH (Memory Controller Hub)**.

Il **southbridge** e' l'altro chip dell'architettura logica del chipset. E' collocato a Sud del bus PCI, *Peripheral Component Interconnect*, sulla scheda madre. La funzione principale del southbridge e' controllare il funzionamento dell'I/O. Il northbridge e' l'elemento che collega southbridge e CPU. **ICH (I/O Controller Hub)** e' un altro nome dato al southbridge per la sua funzionalita'.

**FSB (Front-Side Bus)**: e' il principale percorso di comunicazione tra CPU e memoria principale, SRAM per la cache e DRAM per la memoria centrale. Storicamente, questo bus e' chiamato "northbridge", dal chipset proposto da Intel. E' stato ampiamente usato nelle architetture di calcolo piu' vecchie prima che nuove tecnologie di interconnessione lo sostituissero. Agisce come un'autostrada dei dati, trasportando istruzioni, indirizzi e segnali di controllo tra processore e memoria. Qui e' rappresentato l'FSB:

<!-- da aggiungere -->
*In figura: come l'FSB e' collocato in un moderno sistema digitale*

**BSB (Back-Side Bus)**: il BSB, noto anche come *Back-Side Bus*, e' un bus dedicato, ad alta velocita' e interno che collega la CPU alla propria memoria cache, tipicamente la cache L2. A differenza dell'FSB, che collega la CPU alla memoria principale e al chipset, il BSB collega solo il processore e la cache. Qui e' rappresentato il BSB:

<!-- da aggiungere -->
*In figura: come il BSB e' collocato in un moderno sistema digitale*

**ISA (Industry Standard Architecture)**: e' un bus di sistema a 16 bit introdotto e usato per la prima volta nell'IBM PC/AT e successivamente nel processore Intel 80286. Intel ha sempre pensato alla compatibilita', quindi il bus di sistema ISA usato nel 80286 e' compatibile con il bus di sistema interno a 8 bit del processore Intel 8088, usato nell'IBM PC. L'evoluzione naturale del bus di sistema ISA e' l'EISA, *Extended Industry Standard Architecture*, un bus di sistema a 32 bit usato per architetture x32.

Il bus di sistema ISA ha le seguenti caratteristiche:

- supporta trasferimenti dati a 8 bit e successivamente a 16 bit;
- velocita' di clock tipica di circa 8 MHz, cioe' 8 milioni di Hz;
- massimo transfer rate fino a circa 16 MB/s;
- usa un progetto hardware semplice ed economico;
- non supporta configurazione automatica, sono richieste impostazioni manuali con jumper;
- oggi e' obsoleto nei moderni sistemi di calcolo.

Nel frattempo, EISA ha le seguenti caratteristiche:

- supporta trasferimenti dati a 32 bit;
- maggiore transfer rate fino a circa 33 MB/s;
- retrocompatibile con le schede di espansione ISA;
- supporta il bus mastering per migliorare le prestazioni;
- fornisce configurazione automatica dei dispositivi, basata su software;
- e' stato usato principalmente in PC e server di fascia alta prima di essere sostituito dai bus PCI.

<!-- da fare - PCI (Peripheral Components Interconnect) -->
<!-- da fare - PCIe (PCI Express) -->
<!-- da fare - interfaccia PIO -->
