# **Web service**

### **Architetture distribuite**

Un sistema distribuito consiste in un insieme di **agenti software** distinti che lavorano insieme per implementare una determinata funzionalità. 

Gli **agenti** di un sistema distribuito operano nello stesso ambiente, quindi devono comunicare tramite protocolli di rete.

La **comunicazione** via rete è poco affidabile: i disegner di sistemi distribuiti devono tener conto di elementi quali la **latenza**, **concorrenza**, **malfunzionamenti parziali e temporanei** ecc...

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
- opzionalmente, i descrittori dei servizi.

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

# **RESTful Web Services**
>**REpresentational State Transfer (REST)**: insieme di principi architetturali per la progettazione di Web Services che permettano la manipolazione di risorse.

Una **risorsa** è un oggetto o la rappresentazione di qualcosa di significativo nel dominio applicativo.  
È possibile interagire con le risorse attraverso le **API**.  
Esempio: Un Libro, un Ordine, un Post e qualsiasi altra entità che si possa astrarre da un determinato contesto.  
Il concetto di risorsa è quindi molto simile a quello di oggetto nel mondo della programmazione ad oggetti.

**REST** è uno **stile architetturale** che offre dei principi guida per la realizzazione di "un’architettura di sistema":
- non si riferisce ad un sistema concreto e ben definito, non si tratta di un protocollo, non è uno standard stabilito da un organismo di standardizzazione.
- non dipende da alcuna piattaforma o tecnologia specifica, ma è un insieme di principi architetturali da seguire per la progettazione di WS.

La sua definizione è apparsa per la prima volta nel 2000 nella tesi di Roy Fielding,“Architectural Styles and the Design of Network-based Software
Architectures", in cui si analizzavano alcuni principi alla base di diverse architetture software, tra cui appunto i principi di un’architettura software che consentisse di vedere il Web come una piattaforma per l’elaborazione distribuita.

### **Principi REST**
REST si basa sul concetto di risorsa: ogni componente del sistema è una risorsa accessibile e manipolabile tramite metodi dello standard HTTP (ma attenzione: l’uso del protocollo HTTP non è obbligatorio, si possono utilizzare altri protocolli, es. SMTP).

REST rappresenta dunque un’astrazione degli elementi di un’architettura all’interno di un sistema hypermedia distribuito.

**REST specifica i ruoli dei componenti**, i vincoli sulla loro interazione con altri componenti e la loro interpretazione.

REST definisce il Web come una **hypermedia application** le cui risorse collegate comunicano scambiandosi rappresentazioni dello stato delle risorse stesse.

>REST si fonda sul principio **ROA** (Resource Oriented Architecture): un insieme di linee guida per implementare un web service RESTful.

Mentre REST viene definito come stile architetturale
**RESTful** viene in genere utilizzato per fare riferimento a servizi Web che implementano l’architettura REST. Esempio per riferirsi alle API di un servizio REST.

L’architettura REST fornisce dei principi guida per lo sviluppo di applicazioni distribuite:
- Interazione client server
- Stateless Interactions (Comunicazione stateless
- Uniform Interface (Uso esplicito di metodi HTTP
- Resource Identification (identificazione univoca delle risorse)
- Self Descriptive Messages autodescrizione delle risorse)
- Hypermedia As The Engine Of Application State
(Collegamenti tra le risorse)
- Verranno analizzate singolarmente nelle prossime slide.

### **Interazione Client-Server**

REST applica il paradigma SoC (Separation of Concerns, separazione dei compiti) con un architettura Client-Server.  
Ciò aiuta a stabilire un’architettura distribuita, supportando in tal modo l’evoluzione indipendente della logica lato client e della logica lato server.

Il vincolo Client-Server prevede che il server offra una o più funzionalità e ascolti le richieste di possibili client.  
I client invocano il servizio messo a disposizione dal server inviando il
corrispondente messaggio di richiesta e il servizio, lato server, respinge la richiesta o esegue l’attività richiesta prima di inviare un messaggio di risposta al client.

>La gestione delle eccezioni è delegata al client.

### **Stateless Interactions**

>Si tratta del principio che stabilisce la necessità di avere una comunicazione stateless, senza stato, cioè una comunicazione tra client e server in cui ciascuna richiesta è indipendente dalle altre.

Ogni richiesta dal client al server deve contenere le informazioni necessarie per capire completamente la richiesta, indipendentemente da qualunque richiesta precedente.

**Non significa applicazioni stateless!**

L’idea del REST è quella di evitare transazioni di lunga durata nelle applicazioni.

Una comunicazione senza stato consente di ottimizzare le prestazioni del Web Service e di semplificare la progettazione e l’implementazione dei componenti lato server, perchè l’assenza della gestione dello stato rimuove la necessità
di sincronizzare dati di sessione con un’applicazione esterna: ciò significa che viene favorita la scalabilità orizzontale dell’applicazione.

**Vantaggio**: se un’applicazione si troverà a dover gestire un picco di richieste, sarà sufficiente aggiungere un nuovo server a quelli esistenti e poter rispondere alle richieste dei client senza dover gestire problematiche di sincronizzazione delle sessioni (questa possibilità può essere facilmente sfruttata in ambienti come le architetture cloud).

>Esempio: banale applicazione per la richiesta di una pagina da un insieme numerato in un sistema che richiede la gestione delle sessioni con i client.
- Stateful design
- Il server deve memorizzare l’ultima pagina richiesta dal client.
- Richiede sincronizzazione.

>Esempio: banale applicazione per la richiesta di una pagina da un insieme numerato in un sistema con **stateless interactions**.
- Stateless design
- Il server genera una risposta che collega alla pagina successiva.
- È il client a fornire nella richiesta il numero della pagina da ottenere senza richiedere al server di ricordare la pagina richiesta in precedenza.

**Server**:
- Deve generare risposte che contengono links ad altre risorse per consentire la navigazione tra le stesse.
-Genera risposte che indicano se possono essere memorizzate in una cache o meno per ridurre il numero di richieste per risorse duplicate.

**Client**:
- Invia richieste complete che possono essere gestite indipendentemente dalle altre.
- Usa le informazioni del server per determinare se
porre la risposta in una cache o meno.

### **Uniform Interface**
Unico insieme di operazioni (verbi) che si applica a tutte le azioni (es. GET, PUT, DELETE, …)
- I verbi sono universali e non sono inventati in base all’applicazione; se servono nuovi verbi a molte applicazioni, l’interfaccia può essere estesa.

- I verbi sono le azioni possibili: **metodi HTTP**  
Quando inseriamo un URI nella barra degli indirizzi di un browser stiamo in realtà chiedendo al browser di eseguire un metodo HTTP sulla risorsa individuata dall’URI.

### **Uso di HTTP**
- I servizi web RESTful fanno, uso del protocollo HTTP come mezzo di comunicazione tra client e server.
- Un client invia un messaggio in forma di una richiesta HTTP e il server risponde in forma di una risposta HTTP.

**Richiesta HTTP**:
- **Verb**--> Indica uno dei metodi HTTP come GET,
POST, DELETE, PUT ecc.
- **URI**--> Uniform Resource Identifier, per
identificare la risorsa sul server.
- **HTTP Version**--> Indica la versione HTTP, per esempio, HTTP v 1 1.
- **Request Header**--> Contiene i metadati per il
messaggio di richiesta HTTP come coppie chiave-valore. Ad esempio, tipo del client (o browser), formato supportato dal client, il formato del corpo del messaggio, ecc.
- **Request Body**--> Contenuto del messaggio
restituzione della rappresentazione delle
risorse (es. JSON di risposta).

**Risposta HTTP**
- **Status/Response Code**--> indica lo stato del
server per la risorsa richiesta.
- **HTTP Version**--> Indica la versione di HTTP.
- **Response Header**--> Contiene i metadati per il
messaggio di risposta HTTP come coppie chiave-valore; Ad esempio, la lunghezza dei contenuti, tipo di contenuto, la data della risposta, il tipo di server, ecc.
- **Response Body**--> Contenuto del messaggio di
risposta o rappresentazione della risorsa.

### **Metodi HTTP**
I metodi HTTP permettono di effettuare operazioni sulla risorsa indicata dall’URI.

Si stabilisce una **mappatura uno a uno** tra le
tipiche **operazioni CRUD** (Create, Read, Update,
Delete) che possono essere effettuate sulle
risorse e i metodi HTTP.

|**Metodo HTTP**|**Operazione CRUD**|**Descrizione**|
|--------|--------|--------|
|POST|Create|Crea una nuova risorsa|
|GET|Read|Ottiene una risorsa esistente (rappresentazione)|
|PUT/PATCH|Update|Aggiorna una risorsa o ne modifica lo stato|
|DELETE|Delete|Elimina una risorsa|

### **Metodo GET**
- Operazione di sola lettura.
- Si comporta come l’operazione di SELECT in un database.
- Applicata su URL rappresentanti risorse (es. http ://server.net/servizio/utenti/).

--> In SQL corrisponde a : SELECT * FROM utenti WHERE ID =“U01".  
--> **Input** : accept Header con i media types accettabili per la risorsa.  
--> **Output** : la rappresentazione della risorsa nel media type scelto.

- Applicata su URL rappresentanti collezioni di risorse
(es. http ://server.net/servizio/utenti?nome=pinco&cognome=pallino).  

--> In SQL corrisponde a: SELECT FROM utenti WHERE nome="pinco" AND cognome="pallino".  
--> **Input** : eventuale query string con cui filtrare la collezione e nell’ Accept header i media types accettabili per la risorsa.  
--> **Output** : lista delle url delle risorse (non le risorse stesse) nella collezione.

- Applicata su URL rappresentanti attributi di risorse
(http://server.net/servizio/utenti/U01/nome).

--> In SQL corrisponde a: SELECT nome FROM utenti WHERE ID =“U01”.  
--> **Input**: Accept Header con i media types accettabili per la risorsa.  
--> **Output**: la rappresentazione dell’attributo nel media type scelto.

**Metodo PUT**
- Si usa per aggiornare una risorsa preesistente (cambiarne lo stato).
- Equivale all’ UPDATE in un database SQL.
- Applicata su URL rappresentanti risorse (es.http://server.net/servizio/utenti/U01).

In SQL corrisponde a : UPDATE utenti SET… WHERE ID="U01".  
**Input**:  
--> Content type nell’header: media type con cui si sta trasmettendo la risorsa.  
--> Nel payload è contenuta la rappresentazione della risorsa che verrà interamente sovrascritta a quella indicata nell’URL, codificata nel modo dichiarato. È possibile trasmettere una rappresentazione completa o
parziale, per sostituire tutta la risorsa o solo gli attributi specificati.

**Output**:  
--> Return Status: 204 NO_CONTENT se la richiesta è stata servita.

- Su URL rappresentanti collezioni di risorse
(http://server.net/servizio/utenti). 

**Input**:  
--> Content-type nell’header: media type con cui si sta trasmettendo la risorsa.
--> Payload contenente una rappresentazione di una lista di risorse, codificata opportunamente. L’intero contenuto verrà cancellato e sostituito dagli item indicati.  
**Output**:  
--> Return Status: 204 NO_CONTENT se la richiesta è stata servita.

### **Metodo PATCH**
Si usa per aggiornare parti di una risorsa preesistente (partial update).
- Equivale all’ UPDATE in un database SQL.
- Applicata su URL rappresentanti risorse (es. http://server.net/servizio/utenti/U01).

In SQL corrisponde a UPDATE utenti SET nome =… WHERE ID = "U01"
**Input**:  
--> Content type nell’header : media type con cui si sta trasmettendo la risorsa.  
--> Payload contenente una rappresentazione dell’attributo o degli attributi da sovrascrivere, codificato opportunamente nel formato indicato in Content type.  
**Output**:  
-->Return Status: 204 NO_CONTENT se la richiesta è stata servita.

### **Metodo POST**
- Si usa per creare una nuova entry di risorsa nella collezione.
- Equivale all’ operazione INSERT in un database SQL.
- Su URL rappresentanti collezioni di risorse (http://server.net/servizio/utenti)

In SQL corrisponde : INSERT INTO utenti VALUES(…).  
**Input**:  
--> Content type nell’header: media type con cui si sta trasmettendo la risorsa.  
--> Payload contenente una rappresentazione della risorsa da aggiungere, codificata opportunamente.  
**Output**:  
--> URL utilizzabile per accedere alla risorsa appena inserita.  
--> Location nell’header impostato con tale URL.  
--> Return Status: 201 CREATED se la richiesta è stata servita.

### **Metodo DELETE**
- Si usa per rimuovere una risorsa da una collezione o per svuotare la collezione.
- Equivale all'operazione DELETE in un database SQL.
- Su URL rappresentanti collezioni di risorse (http://server.net/servizio/utenti)    
--> In SQL corrisponde: DELETE FROM utenti  
--> **Output**. Return Status: 204 NO_CONTENT se la richiesta è stata servita.
- Su URL rappresentanti risorse (http://server.net/servizio/utenti/U01)  
-->In SQL corrisponde : DELETE FROM utenti WHERE ID = "U01".  
--> **Output**. Return Status: 204 NO_CONTENT se la richiesta è stata servita.

### **Resource Identification**
>Le risorse sono gli elementi fondamentali su cui si basano i Web Service RESTful.

Per **risorsa** si intende un qualsiasi elemento oggetto di elaborazione che possa essere indirizzabile tramite Web, cioè accessibile e trasferibile tra client e server.

Il concetto di risorsa è molto simile al concetto di oggetto nel mondo della programmazione ad oggetti.

Una risorsa può essere rappresentata in molti modi
diversi.  
Ad esempio come HTML, XML, JSON o anche come file
JPEG. La rappresentazione più famosa utilizzata nelle
implementazioni REST è il JSON.

Ogni risorsa deve essere identificata univocamente sul
Web, il meccanismo più idoneo per individuare una
risorsa è dato dal concetto di **URI** (Universal Resource Identifier)  
- Il principale beneficio nell’adottare lo schema URI per identificare le risorse consiste nel fatto che esiste già, è ben definito e collaudato; non occorre pertanto inventar e un modo nuovo.

Formato URI:
< protocol>://< service-name>/< ResourceType>/< ResourceID>

### **Resource Identification: struttura delle URL**
>Gli **URI** per un web services devono essere intuitivi e facilmente identificabili.

Nella progettazione di un WS RESTful occorre scegliere gli URI secondo le seguenti “best practices”:
- Evitare gli spazi tra i nomi, preferendo l’uso dell’underscore (es. authorized_users).
- Usare solo le lettere in minuscolo.
- Evitare l’uso di verbi o nomi di operazioni (es. non usare get_users o /book?isbn=24&action=delete.
- Mantenere la retrocompatibilità in caso di modifica o aggiornamento degli URI per consentire ai vecchi sistemi di continuare a funzionare. Un modo semplice per ottenere questo scopo è quello di utilizzare il versioning delle API come base dell’url (es. https://api.myservice.it/v1/orders).

>**URI TEMPLATE**: Una tecnica per definire URI che includano parametri, che devono essere sostituiti prima di utilizzare l’URI.
http://example.com/prodotti/{id}

REST non specifica dettagli sugli URI.

L’URI Template non è richiesto dal REST, in senso
strettamente tecnico.
- In termini pratici l’URI Template si rivela una best practice da seguire.

>Gli URI Templates specificano come costruire ed effettuare il parsing di URI parametrici.

Sul _server_ sono spesso usati per configurare "regole di routing" necessarie per elaborare la risposta basata sui parametri forniti dal client.  
Sul _client_ sono utilizzati per istanziare URI a partire da parametri locali.

Le risorse sono organizzate spesso in una struttura
gerarchica tipo directory (che è spesso una vista
sull’effettiva organizzazione dei dati), i cui elementi sono detti **collezioni**.

- http://server.net/servizio/rest/utenti  
Indica la collezione di tutti gli utenti (tabella di un database)
- http://server.net/servizio/rest/utenti/U01  
indica l’utente con identificativo U01 nella collezione

È possibile avere URL con schema diverso da quello
"collezione-risorsa-collezione".
- http://server.net/servizio/rest/utenti/U01/nome  
Non indica la sottocollezione nome dell’utente U01, ma si considera la risorsa utente U01 come collezione di attributi e se ne estrae quello chiamato nome
- Si può usare una query string per simulare un’operazione di filtro quando la URL indica una collezione.  
Es: http://server.net/servizio/rest/utenti?n=pinco&c=pallino

### **Self Descriptive Messages**
>Ogni messaggio contiene le informazioni necessarie per la propria gestione.

Le risorse sono **entità astratte**.  
- L’identificazione delle risorse garantisce che siano chiaramente identificate.  
- L’accesso avviene attraverso un interfaccia uniforme.

L’accesso alle risorse avviene usando la loro rappresentazione.
- Ovvero lo stato attuale della risorsa.
- Viene comunicato che tipo di rappresentazione utilizzare.
- Il formato di rappresentazione è negoziabile tra pari.

La rappresentazione delle risorse può essere basata su vincoli diversi.
- XML e JSON possono rappresentare lo stesso modello.

>Rapresentation rapresents Resource, URI Identifies Resource, URI dereference Rapresentation.

### **Stato delle risorse e dell’applicazione**
L’acronimo REST sta per REpresentational State Transfer e **sottolinea la centralità della gestione dello stato in un sistema distribuito**.

Lo stato che REST prende in considerazione è quello
delle risorse e dell’intera applicazione.

A differenza di quanto avviene in buona parte delle applicazioni Web, dove lo stato dell’applicazione viene spesso mantenuto dal server insieme allo stato della comunicazione, **lo stato dell’applicazione in un’architettura RESTful è il frutto della collaborazione di client e server, ciascuno con i propri ruoli e responsabilità**.

Esempio: gestione del carrello in una applicazione di e-commerce
- Si può prevedere una risorsa carrello dedicata al mantenimento degli articoli scelti dal cliente.
- Si tratta di una risorsa come le altre che non è associata alla sessione corrente di comunicazione e quindi accssibile tramite Uri in qualunque momento.

### **HATEOAS**
Dall’acronimo REST, Representational State Transfer, notiamo che in esso viene fatto riferimento al trasferimento di stato, cioè al fatto che un’applicazione passi **da uno stato all’altro**.

Uno dei principi REST suggerisce l’uso di collegamenti tra risorse come modalità di transizione da uno stato all’altro: **Hypermedia As The Engine of Application State (HATEOAS)**.

Sono trasferite rappresentazioni delle risorse contenenti link.
- Il client può procedere al passo successivo dell’interazione scegliendo uno di questi link.

Le risorse e lo stato possono essere utilizzate navigando i link.
- I link possono interconnettere risorse navigabili.

Le applicazioni RESTful _navigano_ invece di chiamare.
- Le rappresentazioni contengono informazioni riguardo possibili attraversamenti.
- Le applicazioni navigano alla prossima risorsa sulla base dei link semantici.
- La navigazione può essere delegata, dato che tutti i link utilizzano identificatori.

Nella visione REST, l’esecuzione di un’applicazione può essere rappresentata da una rete di risorse in cui un client naviga seguendo i collegamenti ammissibili tra una risorsa e l’altra.

Sfruttando pienamente il principio HATEOAS è possibile creare servizi Web con scarso accoppiamento tra client e server.
- Se il server riorganizza le relazioni tra le risorse, il client è in grado di trovare tutto ciò che serve nelle rappresentazioni ricevute.
- Tutto quello che servirebbe ad un client è solo l’URI della risorsa iniziale.
