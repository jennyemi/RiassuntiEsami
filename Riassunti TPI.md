# **Web service**

### **Architetture distribuite**

Un sistema distribuito consiste in un insieme di **agenti software** distinti che lavorano insieme per implementare una determinata funzionalità. 

Gli **agenti** di un sistema distribuito operano nello stesso ambiente, quindi devono comunicare tramite protocoli di rete.

La **comunicazione** via rete è poco affidabile:i disegner di sistemi distribuiti devono tener conto di elementi quali la **latenza**, **concorrenza**, **malfunzionamenti parziali e temporanei** ecc...

### **Service Oriented Architecture**
>La **service oriented architecture** è un tipo di sistema distribuito in cui gli agenti sono servizi.  
>Un **servizio** è un agente che esegue un'operazione ben definita ("fornisce un servizio") e pùò venire invocato dall'esterno del suo contesto, che può essere anche un'applicazione di grandi dimensioni.

Anche se un servizio è implementato espandendo una particolare funzionalità di un'applicazione  complessa, i suoi utenti devono considerare solo l'interfaccia, non il contesto.  
Nella definizione di SOA si sottolinea inoltre il fatto che i servizi hanno interfacce verso la rete e comunicano usando formati e protocolli standard.

### **Elementi di una SOA**
La SOA introduce, rispetto ai più generali sistemi distribuiti, il vincolo delle **connessioni stateless**,in cui tutti i dati relatvi a una richiesta devono essere contenuti nella richiesta stessa, non si possono inviare dati correlati in richieste successive.

La descrizione di un servizio in una SOA è essenzialmente la descrizione dei messaggi scambiati.  
Se la SOA è "pubblicata", anche i descrittori pubblici dei servizi e dei messaggi diventano una sua parte integrante. Questi decrittori sono di solito in un formato comprensibile dal software, e costituiscono essi stessi dei messaggi (usati nella comunicazione con i sistemi di **service discovery**).

I componenti chiave di una SOA sono quindi:
- gli agenti che forniscono e usano servizi.
- i messaggi scambiati dai servizi.
- i meccanismi di comunicazione che permettono lo scambio dei messaggi.
- opzionalmente, i descrittori dei servizi

Per ciascuno di questi elementi esistono vari standard di implementazione/realizzazione, pubblici o proprietari. Ovviamente l'enfasi attuale è sugli standard pubblici e aperti.

### **Il WWW come una SOA**
Il World Wide Web è una SOA che opera come un sistema informativo di rete. Rispetto alla SOA generica, il WWW impone altri vincoli:
- Gli agenti e le risorse, cioé gli oggetti gestiti dagli agenti, sono identificati **Uniform Resource Identifiers** (URI).
- Gli agenti manipolano o forniscono una rappresentazione delle risorse ottenuta tramite formati dati comuni (XML, HTML, CSS, JPEG, PNG).
- Gli agenti trasmettono le rappresentazioni delle risorse attraverso protocolli che ussano gli URI per indirizzare altri agenti o risorse (HTTP).

### **La Web Service Architecture**
I servizi web svolgono due principali funzioni:
- **Manipolazione di risorse**: si tratta di servizi che permettono di manipolare (ricevere/trasmettere) direttamente delle risorse.
- **Gestione di oggetti distribuiti (operazioni via web)**: sono servizi che effettuano operazioni (anche molto complesse) su risorse che non sono sul web (es. database). In questo caso i messaggi XML contengono i dati necessari a invocare queste operazioni e comunicare gli eventuali risultati.

Nel primo caso, i servizi sono solitamente implementati direttamente dai web server.  
Nel secondo caso, quello che ci interessa maggiormente, i servizi sono costituiti da software esterno che viene attivato dai web server in risposta a particolari messaggi.

### **Definizione di Servizio Web**
un servizio web è un sistema software progettato per supportare **l'interazione interoperabile da macchina a macchina** su una rete. Ha un'interfaccia descritta in un formato elaborabile dalla macchina (WSDL). Altri sistemi interagiscono con il servizio Web nel modo prescritto dalla sua descrizione usando messaggi SOAP, tipicamente trasmessi usando HTTP con una serializzazione XML in combinazione con altri standard relativi al Web.

### **Intrazione interoperabilità Machine-to-Machine**
Lo scopo primario di un servizio web è fornire una via estremamente semplice e versatile per far comunicare componenti software attraverso la rete.

L'interoperabilità è la vera chiave:
- I servizi web sono descritti astrattamente.
- Non sono dipendenti da architetture software/hardware particolari.
- Possono essere implementati praticamente con qualsiasi linguaggio.
- Il client e il server di un servizio web possono addirittura essere basati su linguaggi e tecnologie diverse, a patto che rispettino "all'interfaccia" il semplice contratto di comunicazione definito dal servizio.

### **Web Service**
- I servizi web sono un **modo standardizzato** per un'applicazione di invocare un metodo di un'altra applicazione.  
Queste applicazioni possono risiedere su diversi computer collegati da una rete locale o da Internet.
- Due attori, un **client** e un **server**. Il server mette a disposizione una serie di metodi che, quando vengono chiamati, eseguono una certa azione e/o restituiscono alcuni dati.
- **Il client invoca uno dei metodi del server**.
- Come i metodi in una libreria di classi, i metodi di un servizio Web possono accettare un numero arbitrario di **parametri** di input e possono opzionalmente restituire un risultato.
- Lo standard dei servizi Web indica in modo molto dettagliato come un client può invocare un metodo di servizio Web da un server.
- Lo standard detta come i parametri di input e il ritorno i valori vengono passati da un computer all'altro, come i difetti vengono gestiti, e una miriade di altre complicazioni.

Nasce tutto dal concetto di **delegare** a qualcuno l'esecuzione di un compito. Nei linguaggi di prgrammazione l'applicazione di tale concetto si ha con la definizione e chiamata a sottoprogramma (procedure call).

### **Distributed Computer Environment**
Successivamente tale concetto è stato esteso con l’utilizzo di **RPC** (**Remote Procedure Call**), secondo diverse modalità e standard proprietari (es: MicrosoftRPC, CORBA, e altri).

Problemi:
- I dati vengono passati tra client che richiede l’esecuzione di un compito e server che lo effettua utilizzando formati non standard, dipendenti dalle piattaforme e dai protocolli di rete.
- La sessione di comunicazione viene ostacolata dalla tecnologia NAT spesso utilizzata quando client e/o server si trovano in una rete LAN privata.

Soluzioni:
- Utilizziamo **modalità e protocolli standard** per il trasferimento di messaggi tra client e server.  
I dati vengono scambiati in modalità testuale
(formati XML).  
Facciamo in modo che si possa utilizzare un **servizio** senza conoscere la piattaforma e le modalità di implementazione.

### **Perchè usare Web Service**
- I Web service permettono l’interoperabilità tra diverse applicazioni software e su diverse piattaforme hardware/software.
- Utilizzano un formato dei dati di tipo testuale, quindi più comprensibile e più facile da utilizzare per gli sviluppatori (esclusi ovviamente i trasferimenti di dati di tipo binario).
- Normalmente, essendo basati sul protocollo HTTP, non richiedono modifiche alle regole di sicurezza utilizzate come filtro dai firewall.
- Sono semplici da utilizzare e possono essere combinati l’uno con l’altro (indipendentemente da chi li fornisce e da dove vengono resi disponibili) per formare servizi “integrati” e complessi.
- Permettono di riutilizzare applicazioni già sviluppate.
- Fintanto che l’interfaccia rimane costante, le modifiche effettuate ai servizi rimangono trasparenti.
- I **servizi web** sono in grado di pubblicare le loro funzioni e di scambiare dati con il resto del mondo.
- Tutte le informazioni vengono scambiate attraverso protocolli “aperti”.

### **Svantaggi e problematiche**
- **Le performance**. I Web service presentano performance drasticamente inferiori rispetto ad altri metodi di comunicazione utilizzabili in rete. Questo svantaggio è legato alla natura stessa dei servizi web. Essendo basati su XML ogni trasferimento di dati richiede l’inserimento di un notevole numero di dati supplementari (i tag XML) indispensabili per la descrizione dell’operazione. 
Inoltre tutti i dati inviati richiedono di essere prima codificati e poi decodificati ai capi della connessione. Queste due caratteristiche dei Web service li rendono poco adatti a flussi di dati intensi o dove la velocità dell’applicazione rappresenti un fattore critico.
- **Il protocollo base, HTTP**. Quando si sviluppa un Web service è necessario tener conto del protocollo di base. È quindi indispensabile disporre di un’applicazione terza che gestisca le
richieste HTTP oppure è necessario includerla direttamente nel codice del nostro programma qualora si desideri la sua totale indipendenza. Va detto comunque che generalmente il codice che implementa un Web service viene fatto eseguire da un Web server (es. Apache) tramite CGI (per es. con Python) o tramite appositi moduli (vedi PHP). Eseguendo il codice del Web service attraverso un server web la gestione di HTTP è immediatamente assicurata.

### **Tipi di Web Service**
Esistono due principali architetture per i WS:
- **SOA**: architettura complessa, più completa, strutturata, basata su un insieme di protocolli tra cui SOAP, WSDL, UDDI; è usata per lo scambio di messaggi per l’invocazione di servizi remoti e si prefigge di riprodurre in ambito Web un approccio a chiamate remote
- **REST** (Web API): più semplice e leggera, si concentra sulla descrizione di risorse, sul modo di individuarle nel Web e sul modo di trasferirle da una macchina all’altra.

