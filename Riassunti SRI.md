# **Integrità e autenticazione del messaggio**
>Non è possibile per due persone comunicare in modo sicuro su un canale insicuro utilizzando la crittografia.

Non viene garantità ne l'integrità (messaggio intercettato da terzi e riutilizzato da quest'ultimi) ne l'autenticazione (no vi è sicureza sull'identità del mittente).

Problemi:
- I contenuti dei file sono poco legati fra loro.
- Uso di block chipers

Si ricorre a una one-way function, detta anche **hash function**, **checksum** o **message digest**; i dati in input di lunghezza arbitraria vengono trasformati output di lunghezza costante.  
h: {0, 1}*--> {0, 1}^n  
One-way = irreversibile  
- Dato x è facile calcolare h(x)
- Dato y è difficile trovare x t.c. y = h(x) [Preimage resistence]
- Dato m è difficile trovare m' t.c. h(m)=h(m') [Second preimage resistence]

Collision-resitance: difficile trovare m, m' distinti t.c. h(m)=h(m')  
Una piccola modifica di m altera tutto h(m)----> Effetto valanga

### **Il paradosso del compleanno**
In crittografia usato per il **dimensionamento del blocco da cifrare** e **provare le proprietà di resistenza alle collisioni**.  
Utilizza codici hash di 64 bit (collisione fra m e m' con circa 2^32 tentativi).  
Di solito la dimensione dei codici hash è di 160 bit (SHA 1), il tempo di collisione è di 2^80 tentativi.  

Viene utilizzato il termine paradosso perchè la verità matematica contraddice l'intuizione naturale.

Che probabilità c'è che due persone nella stessa stanza compiano gli anni lol stesso giorno?
- In un gruppo di 23 persone 51%
- Da 30 più del 70%
- Da 50 il 97%

### **Algoritmi crittografici di hashing**
Un buon algoritmo di **message digest** deve essere veloce da calcolare per non sovraccaricare troppo i sistemi su cui viene utilizzato e, soprattutto, deve essere difficile da invertire, ossia deve essere praticamente impossibile, partendo dal digest ,
ricostruire il messaggio originale.  
Molto spesso gli algoritmi di digest vengono utilizzati non soltanto per proteggere i dati, ma anche in unione con algoritmi a chiave pubblica, perché, visto che questi algoritmi sono lenti, facendoli operare non sui dati originali ma sul loro «riassunto», questi algoritmi diventano più veloci.  
Gli algoritmi più usati sono:
- **MD5** che opera su blocchi dati da 512 bit e genera un hash da 128 bit.
- **SHA 1** opera su blocchi dati da 512 bit e genera un hash da 160 bit
### **Requisiti di una funzione di hash**
- È facile calcolare l’hash di un messaggio.
- È difficile trovare il messaggio che ha generato un dato hash (non invertibilità delle funzioni di hash), **si dice che la
funzione è one-way hash**.  
- È difficile modificare un messaggio senza modificare il relativo hash (resistenza debole alle collisioni).  
- È difficile trovare due messaggi che abbiano lo stesso hash
(resistenza forte alle collisioni).

### **Utilizzi di una funzione di hash**
- **Controllo degli errori**: in questo caso la funzione di hash viene utilizzata come un checksum, per identificare eventuali errori di trasmissione dei dati.
- **Integrità dei dati**: utilizzato ad esempio negli IDS (intrusion detection systems) per controllare l’integrità dei file critici di un sistema operativo.
- **Memorizzazione di password e autenticazione**: nella maggior parte dei casi, quando un sistema informatico deve memorizzare una password, questa non viene salvata in chiaro per motivi
di sicurezza, né viene cifrata per evitare che sia possibile risalire alla password originale. Si memorizza in questi casi l’ hash della password con l’aggiunta di un valore detto salt e di un eventuale ulteriore valore detto pepper.
- **Firme digitali**: firmare solo un hash del documento secondo il noto paradigma hash then sign : ossia si calcola prima hash di un documento e poi si applica la firma digitale non a tutto il documento ma solo all’ hash dello stesso.

### **Algoritmo MD5**
- Digest da 128 bit 16 bytes.
- Creato da Ronald Rivest nel 1991.
>È diffuso anche come supporto per l'autenticazione degli utenti
attraverso i linguaggi di scripting Web server side (il linguaggio
PHP implementa nativamente la funzione MD5).
- È stato ampiamente usato fino a quando sono state dimostrate
alcune sue debolezze crittografiche per le quali non è più
considerato sicuro in applicazioni critiche
Funzionamento:
- Il messaggio viene diviso in blocchi da 512 bit.
- Ogni blocco viene elaborato in 4 “round” successivi.
- In ogni round la funzione di compressione (suo uso concatenato ha il compito di “comprimere” l’informazione di un messaggio in un
numero minore di bit), viene applicata 16 volte.
- La funzione F dipende dal round
- Mi (secondo sotto blocco dell'imagine delle slide) è un sottoblocco di 32 bit.
- Ki è una costante che cambia a seconda del round.
### **Algoritmo SHA (Secure Hash Algorithm)**
Famiglia di funzioni crittografiche di hash sviluppate dalla National Security Agency (e pubblicate come standard federale dal governo degli USA).  
Usato dal governo USA all'interno del suo sistema di firma digitale.
>Gli algoritmi della famiglia sono denominati SHA 1 , SHA 224 , SHA
256 , SHA 384 e SHA 512 : le ultime 4 varianti sono spesso indicate
genericamente come SHA 2 , per distinguerle dal primo.  
Il primo produce un **digest del messaggio** di soli 160 bit, mentre gli altri producono digest di lunghezza in bit pari al numero indicato nella loro sigla.  

- L'SHA 1 è il più diffuso algoritmo della famiglia SHA ed è utilizzato in numerose applicazioni e protocolli.
- SHA 3 (Secure Hash Algorithm 3) è l'ultimo membro della famiglia di standard Secure Hash Algorithm, rilasciato dal NIST il 5 agosto 2015.
- L’abbassamento dei costi accompagnato da maggiori potenze di calcolo ha reso l’SHA 1 veramente pericoloso per la sicurezza dei sistemi. I ricercatori raccomandano per questo che ci sia quanto prima una migrazione verso SHA 2 o SHA 3, i principali browser hanno programmato di smettere di accettare le firme basate su SHA 1 a partire da gennaio del 2017.
Funzionamento:
- Il messaggio viene elaborato in blocchi di 512 bit (16 word da 32 bit)  
Vi sono 4 fasi da 20 passi:
- le 16 word sono espanse a 80 word tramite operazioni di miscelazione e duplicazione.
- L’output è sommato all’input per ottenere il nuovo valore
dei buffer.
> **Il codice hash è il valore finale del buffer**
### **Crittografia e autenticazione**
Le funzioni hash non garantiscono l'autenticazione.

One-way function 2 famiglie:
- Non-keyed (senza chiave)  
h: {0,1}*--->{0,1}^n (e. g. n = 160);  
h(m) è ilmessage digest di m;  
Usato per Integrety, firme digitali...  
Esempi: MD4, MD5 (Message digest. 128 bit digest), SHA/SHS (Secure Hash Algorithm or Standard, 160 bit digest)
- Keyed (con chiave)  
**h**k(k piccola):{0,1}*--->{0,1}^n (e. g. n = 96);  
Usato per message integrity e authentication
### **MAC Message Authentication Code**
Si tratta di una **One-way keyed function**, richiede una chiave segreta condivisa.
Utilizzo:
- Il mittente spedisce il messaggio m e M1=MAC(m)
-Il destinatario riceve entrambe le parti
- Il destinatario calcola M2=MAC(m)  
Se M2 == M1 il messaggio è valido  
Se M2 != M1 il messaggio è corrotto

Il MAC viene utilizzato per l'integrità, non per la segretezza.

Nel file system:
|............FILE............|hpwd(pwd in piccolo)(file)|
- Il MAC viene verificato quando si vuole accedere al file
-La pwd è la password necessaria per modificare il file

Il MAC è sostanzialmente un checksum crittografico: condensa un messaggio di lunghezza variabile, utilizza una data chiave segreta K e il MAC ha lunghezza fissa.
>Il MAC in cui si utilizza anche una funziona di Hash viene più
propriamente denominato HMAC (Hash based MAC).
# **Firma digitale**
La **firma digitale**, equivalente elettronico della firma autografa su carta, è associata stabilmente al documento elettronico sulla quale è apposta e ne attesta con certezza l’integrità, autenticità e la non ripudiabilità. Crittografia assimetrica e ottiene solo **autenticazione** e **integrità**.

La firma digitale viene utilizzata per garantire l’ autenticità
di un messaggio (provenienza dall’utente dichiarato), senza
ricorrere alla crittazione dell’intero messaggio, utilizzando la
chiave privata del mittente e permettendo al destinatario di
verificare tale autenticità.

Per generare una firma digitale è necessario un **kit** (dispositivo + software).
Il file firmato digitalmente **deve** essere **certificato** dall’ente certificatore prima dell’invio.
Con il certificato il destinatario ottiene la **chiave pubblica** sicura per verificare identità del mittente e integrità del documento.
L’algoritmo di apposizione della firma digitale prevede la creazione di un’impronta (message digest) attraverso la funzione di hash.
Per verificare una firma digitale occorre essere in possesso della
chiave pubblica del mittente:
- le chiavi pubbliche dovrebbero essere accessibili in una sorta di “registro”.  

Si può verificare che una chiave pubblica sia autentica
- Una chiave pubblica falsa fa cadere tutto lo schema.
- Se non c’è la certezza che una chiave pubblica PU appartenga proprio all’utente U, si apre la strada all’attacco dell’ “uomo in mezzo” (MAN IN THE MIDDLE), che potrebbe riuscire ad illudere entrambi le parti.

**Soluzione**: autorità di certificazione (Certification Authority (CA)) e il sistema dei certificati.

La firma digitale di un documento ha dimensione limitata (es:
128 bit) indipendentemente dalla dimensione del documento.  
Tra gli algoritmi più noti per la firma digitale ci sono una con schema basato su RSA (attaccabile sfruttando la proprietà di omomorfismo, la sicurezza dello schema dipende dalle proprietà di sicurezza della funzione hash utilizzata per applicare il paradigma hash then sign ) e Digital Signature Algorithm (DSA) che è uno standard FIPS per la firma digitale proposto dal National Institute of Standards and Technology (NIST) impiegato nel Digital Signature Standard (DSS).

Funzioni:
- Per firmare: Sign(key^-1, m)
- Per verificare: Verify(Key, x, m) ----> OK se x = Sign(key^-1, m)

Resistente alla contraffazione:
-Non si riesce a calcolare Sign(key^-1, m) da m e key
- Resiste all'attacco a forza brutta

### **Creazione della firma**
1. Calcolare il messagge digest del testo
2. Codificare il digest con la chiave privata del mittente (firma digitale)
3. Creare copia (testo + firma) e spedirla
### **Verifica della firma**
1. Separare il testo dall firma
2. Decodificare la firma con la chiave pubblica del mittente
3. Calcolare il digest del testo
4. Verificare che i due digest coincidano
### **Hashing vs MAC vs Firme digitali**
- Hashing: checksum privata... produce il footprint di un messaggio e deve venire memorizzata separatamente dal messaggio.
- MAC: checksum cifrata... il footprint viene protetto da un a chiave condivisa e segreta e può essere trasmesso lungo un canale pubblico.
- Firma digitale: non-repudiaton... il footprint viene protetto da una chiave privata e non ci sono dati segreti con chi verifica la firma.
# **Certificati digitali**
Una terza parte fidata, l’autorità di certificazione (**CA**), certifica/attesta il legame utente/chiave pubblica mediante apposito certificato digitale, e garantisce che la chiave pubblica di qualcuno, ottenuta da un registro pubblico, sia stata rilasciata proprio da quella persona.

Certificato reale è cartaceo, emesso da un'entità conosciuta e **associa l’identità** di una persona **al** suo **aspetto fisico**.  
Certificato digitale è elettronico, **associa l’identità** di una persona **ad una chiave pubblica**, emesso da CA riconosciuta, firmato con la chiave privata della CA. Formato tipico X.509 (raccomandato dall’ITU International Telecommunication Union).

Un certificato digitale è quindi un file contenente una serie di informazioni tra cui:
- Una chiave pubblica
- Informazioni sull'utente
- Una o più firme digitali
- Un periodo di validità

Sono liberamente distribuibili ed esistono strumenti software per la loro gestione.

Il certificato garantisce l'autenticità di una chiave pubblica, mentre **l'autenticità del certificato è garantita dalla CA che ha emesso il certificato**

Una Certification Authority è un ente che emette certificati e garantisce la loro autenticità tramite una catena di emittenti verificabile a partire da poche CA di primo livello (Root CA) di cui tutti si fidano.
La CA riceve delle richieste di emissione di certificato (CSR
Certificate Signing Request) che contengono informazioni sul
richiedente e una chiave pubblica che lo stesso ha generato. Il
richiedente non comunica alla CA la chiave privata che esso stesso ha generato congiuntamente alla chiave pubblica. La CA
effettua le opportune verifiche (in base alla legislazione in vigore nello stato in cui risiede e a standard internazionali) sull’identità del richiedente e quindi emette il certificato richiesto, firmandolo con la propria firma digitale (chiave privata).
- La CA dispone di un certificato con il quale sono firmati tutti i certificati emessi agli utenti, memorizzato su una macchina
sicura.
- Tali certificati hanno una durata temporale definita e possono
essere in qualsiasi momento revocati se non permangono le
condizioni che ne hanno consentito il rilascio.

I certificati revocati e sospesi sono inseriti in due liste:
- **CRL**: Certificate Revocation List
- **CSL**: Certificate Suspension List

Ciascun certificato è firmato digitalmente dalla CA che l’ha rilasciato, ad eccezione di una **ROOT CA** che firma da sola il
proprio certificato. Siccome la firma digitale è apposta utilizzando la chiave privata, è necessario reperire la corrispondente chiave pubblica per verificare tale firma.

Le **Root CA** sono gli unici enti che possiedono un certificato
autogenerato (self-signed) riconosciuto valido. Tale certificato è
installato nativamente nei comuni browsers.  
Chiunque può creare un certificato, ma i browsers concedono
fiducia solo ai certificati provenienti da un’organizzazione che
appartiene ad un elenco di CA di fiducia. I browsers vengono
rilasciati con un elenco di CA di fiducia preinstallato, noto come
**Trusted Root CA store**.

I 10 compiti di una CA:

- Identificare con certezza la persona che fa richiesta della certificazione della chiave pubblica.
- Rilasciare e rendere pubblico il certificato.
- Garantire l’accesso telematico al registro delle chiavi pubbliche.
- Informare i richiedenti sulla procedura di certificazione e sulle tecniche per accedervi.
- Dichiarare la propria politica di sicurezza.
- Attenersi alle norme sul trattamento di dati personali.
- Non rendersi depositario delle chiavi private.
- Procedere alla revoca o alla sospensione dei certificati in caso di richiesta dell’interessato o venendo a conoscenza di abusi o falsificazioni.
- Rendere pubblica la revoca o la sospensione delle chiavi.
- Assicurare la corretta manutenzione del sistema di certificazione.

### **Ottenere un certificato digitale**
Entità:
- Il richiedente, il soggetto richiede l’emissione di un certificato digitale a proprio nome.
- La “ Registration Authority” (RA), l’ente preposto all’identificazione del soggetto che richiede il certificato (una
sorta di intermediario tra la CA ed il soggetto richiedente).
- La “ Certification Authority” (CA) la società che rilascia i
certificati.  

Alice genera una coppia di chiavi pubblica/privata (k, k^-1) e vuole rendere k pubblica
1. Alice spedisce k a CA (Certification Authority)
2. CA verifica che Alice conosco k^-1
3. CA genera Ck e lo spedisce a Alice; Alice spedisce Ck quando usa k

Con Bob:
1. Bob richiede alla RA l’emissione di un certificato digitale relativo alla chiave pubblica della sua copia di chiavi asimmetriche.  
2. La Registration Authority esegue una “procedura di identificazione", identifica Bob come il proprietario di una coppia
di chiavi asimmetriche ne verifica la corrispondenza.
3. A questo punto la RA chiede alla CA di generare un certificato
digitale per Bob e la sua chiave pubblica. 
4. Il certificato dell’utente Bob viene firmato dalla CA con un suo certificato digitale chiamato “ Root CA” che è auto-certificato self-signed.
5. La CA pubblica su un specifico server pubblico detto “Certificate Server” liberamente accessibile, la lista dei certificati in corso di validità o con l’indicazione se questi certificati sono revocati o sospesi.
6. Bob riceve dalla CA il proprio certificato digitale firmato + il
certificato digitale “ Root ” della CA.
7. La registrazione sbagliata dell’utente è critico. Eventuali
errori nella fase di identificazione dell’utente determinano il
crollo della catena “ trusted ” e vanificano il processo di firma.
8. Il momento della identificazione deve pertanto essere fatto per
iscritto e attraverso una verifica fisica oltre che documentale del
soggetto.
9. Bob invia a Alice la sua chiave pubblica ed il suo certificato
digitale.
10. Alice per verificare quanto ottenuto si collega con il Certificate Server della CA che ha rilasciato il certificato di Bob, e lo verifica con quello memorizzato.
11. Il processo è reciproco. Una volta che entrambi (Bob e Alice) sono reciprocamente identificati e verificati lo scambio di messaggi può avere luogo nelle diverse modalità descritte
precedentemente.

L’utente genera sul PC una coppia di chiavi
- I browser comuni offrono il servizio
- La chiave privata è memorizzata localmente in un file nascosto
- Maggiore sicurezza: generare la coppia di chiavi tramite SmartCard collegata al PC - la chiave privata non esce mai dalla SmartCard

L’utente invia alla CA una richiesta di certificato, insieme alla chiave pubblica generata (a meno che non sia la CA a generare la coppia di chiavi per l’utente).
 Il certificato del server può essere certificato dai clienti che conoscono la chiave Kca della CA.  
### **Formato dei certificati**
Ck = (A, k, texp, priv, …, sig CA)  
texp = expiration date  
priv = privileges  
… = altre informazioni  

Tutti conoscono la chiave di verifica (chiave pubblica) di CA.
Problemi:
- Singolo punto di fallimento
- Vulnerabilità all’aumentare del numero di partecipanti
 ### **Public-Key Infrastructure (PKI)**
>L’insieme di tutte le parti, utenti e Authority, nonché delle
tecnologie da queste usate, dai servizi offerti e dalle politiche di gestione è detta **PKI (Public Key Infrastructure)**  

Public Key Infrastructure (PKI) è un'insieme hardware, software, persone, politiche e procedure necessarie per la creazione, la gestione, la distribuzione, l'uso, la memorizzazione e la revoca dei certificati.  
La PKI è anche ciò che lega le chiavi con le identità degli utenti per mezzo di un'Autorità di Certificazione (CA). La PKI utilizza un sistema di crittografia ibrido e trae vantaggio dall'utilizzo di entrambi i tipi di crittografia.

In particolare i certificatori (in Italia) sono soggetti con particolari requisiti di onorabilità, accreditati presso il CNIPA (Centro Nazionale per l’Informatica nella Pubblica Amministrazione). le norme vigenti in materia richiedono che il soggetto certificatore sia in possesso di particolari requisiti tecnici, organizzativi e societari.

Trusted root authority (VeriSign, IBM, United Nations)
- Tutti devono conoscere la chiave di verifica della root authority.

Le root authority può firmare i certificati.  
I certificati identificano altri utenti, incluse altre autorità.  
La gerarchia tra autorità genera **certificate chains**.
### **PKI a Struttura gerarchica**
Catene di certificati
- Contiene i certificati di tutti i nodi fino alla
radice.
- Durante la verifica i certificati vengono scambiati solo per i nodi fino al primo antenato comune.

La root signature è fidata e riconoscibile, la ridondanza riduce la vulnerabilità.  
Utilizzata in SET:  
- Sviluppato da Vista/Mastercard
- La root key viene distribuita tra 4 siti

### **PKCS**
PKCS è un gruppo di crittografia standard a chiave pubblica ideato e pubblicato da RSA Security Inc, a partire dai primi anni Novanta.  
PKCS#12 è un formato di archivio che contiene materiale
crittografico, ovvero più oggetti crittografici memorizzati in un
unico file. Viene comunemente utilizzato per memorizzare un
certificato a chiave pubblica X.509 con la corrispondente chiave
privata, o un elenco di certificati che formano una catena di
fiducia (chain trust).  
Un file PKCS #12 può essere criptato e firmato. Anche i contenitori interni, chiamati " SafeBag "s , possono essere crittografati e firmati. Alcuni SafeBag sono predefiniti per memorizzare certificati, chiavi private e CRL.  
PKCS #12 è una delle famiglie di standard chiamati Public Key Cryptography Standards (PKCS) pubblicati da RSA Laboratories.  
L'estensione dei file di PKCS #12 sono ".p12" o ". pfx".
 ### **Revoca del certificato**
Ragioni:
- Cambio dei dati personali
- Licenziamento, dimissioni
- Compromissione della chiave privata
- La richiesta di revoca può arrivare dall’utente o dall’emettitore.  

La revoca avviene mediante il CRL (Certificate Revocation List).  
**Certificate Revocation List**: lista di certificati revocati prima della loro naturale scadenza temporale.  
Firmata digitalmente dalla stessa CA che ha emesso il certificato che è stato revocato. Il provvedimento non è retroattivo.
### **Sospensione del certificato**
Il certificatore sospende la validità del certificato per un
determinato periodo di tempo.
### **KDC vs PKI**
**KDC (Chiave Segreta)**:
- Deve essere on-line in quanto usato ad ogni sessione.
- Conosce la chiave segreta.
- Viene compromesso, vengono esposti i messaggi passati e futuri.
- Veloce.  
**PKI (Chiave Pubblica)**:
- Può essere off-line tranne in fase di generazione delle chiavi.
- Conosce solo le chiavi pubbliche.
- Viene compromessa, vengono esposti solo i messaggi futuri.
- Lento.

La crittografia viene usata per risolvere alcuni problemi di sicurezza.  
Viene creato un **protocollo di sicurezza**, un preciso schema di eventi che possibilmente fanno uso della crittografia.
### **Catena di certificazione**

Un'autorità di certificazione potrebbe funzionare in modo
autonomo, oppure potrebbe appartenere a una struttura più o
meno articolata. Infatti, **ci potrebbe essere la necessità di
suddividere il carico di lavoro in più organizzazioni**.

Struttura gerarchica ad albero, dove si parte da un'autorità principale, che si autocertifica, che demanda e organizza il compito di certificazione a strutture inferiori, firmando il loro certificato (con la propria chiave privata).  
Queste autorità inferiori possono avere a loro volta la responsabilità sulla certificazione di altre autorità di livello
inferiore, ecc.

> La presenza di una scomposizione gerarchica tra le autorità di
certificazione, più o meno articolata, genera una catena di
certificati , ovvero un «percorso di fiducia» (trust path).

In questi casi è bene che il tipo di certificato elettronico che si utilizza permetta di annotare questa catena, in maniera tale che sia possibile il recupero dei certificati
mancanti. 

||Chi ottiene il certificato di Tizio, firmato
dall'autorità Bianco, per verificare l'autenticità del certificato di deve disporre della chiave pubblica di quell'autorità, deve avere cioé il certificato dell'autorità stessa (che contiene anche la sua chiave pubblica). Senza questa informazione non potrebbe verificare la firma di
questa autorità.  
Se nel certificato di Tizio è annotato che l'autorità Beta
è garante per l'autorità Bianco e inoltre è annotato in che modo
procurarsi il certificato di Bianco rilasciato da Beta, se si dispone già del certificato dell'autorità Beta, dopo che è stato prelevato il certificato di Bianco, questo lo si può controllare attraverso quello di Beta.  
1. Tizio si presenta con il proprio certificato, contenente la firma di garanzia dell'autorità Bianco;
2. l'autorità Bianco è sconosciuta, di conseguenza non si dispone
del suo stesso certificato, dal quale sarebbe necessario estrarre la chiave pubblica per verificarne la firma sul certificato di Tizio;
3. nel certificato di Tizio c'è scritto in che modo ottenere il
certificato dell'autorità Bianco, che così viene prelevato
attraverso la rete;
4. nel certificato di Tizio c'è scritto che l'autorità Bianco è garantita dall'autorità Beta, della quale, per fortuna, si dispone del certificato;
5. con la chiave pubblica di Beta si verifica la firma nel certificato di Bianco;
6. disponendo del certificato di Bianco e avendo verificato la sua
autenticità, si può verificare l'autenticità del certificato di Tizio.
> Se non si disponesse del certificato di Beta occorrerebbe ripetere la ricerca per l'autorità garante superiore, nel modo già visto.
||
### **Tipi di Certificato Digitale**
- Self-signed certificate: utilizzato soltanto per prove o emesso da una CA locale di un ambiente chiuso all’interno del quale tutti si fidano della CA locale.
- Domain Validated certificate: emesso da una CA in base solo alla verifica del proprietario di un dominio registrato.
- Fully authenticated SSL certificate: certificato standard emesso da una CA.
- Code signing certificates: certificato avente lo scopo specifico di garantire l’autenticità di un codice software.
- Extended Validation (EV) SSL certificate: i certificati di convalida estesa fanno diventare verde la barra degli indirizzi e contengono una convalida più attendibile dell'identità del sito
Web.
### **Standard X.509**
X.509 è uno standard per le infrastrutture a chiave pubblica
(PKI). Definisce formati standard per i certificati a chiave
pubblica, ed un certification path validation algorithm.  
Appartiene alla serie di documenti X.500 dell'ITU-T (International Telecommunications Union).  
E’ stato emesso nel 1988 (X.509v2 nel 1993, X.509v3 nel 1995)  
Nello standard X.509, una CA rilascia un certificato che accoppia
una chiave pubblica ad un Nome Distintivo (Distinguished
Name), oppure ad un Nome Alternativo (Alternative Name) che
potrebbe essere un indirizzo e mail o un record DNS.  
Perciò anche ad un sito web può essere assegnato un certificato
digitale; basta che sia registrato nei DNS pubblici in Internet.
>Anche i comuni browsers fanno parte della PKI, dato che possiedono
uno store di certificati delle Root CA e implementano dei protocolli per la comunicazione sicura e il software necessario per controllare la validità dei certificati utilizzati da tali protocolli.
Struttura:
- **Version**: Indica la Versione dello standard applicata al
certificato.
- **Serial Number**: Numero univoco assegnato dall’autorità di certificazione che lo ha emesso. Tale attributo, unito al nome
dell’autorità che lo ha emesso, identifica univocamente un certificato.
- **Signature Algorithm Identifier**: Identifica l’algoritmo di firma digitale utilizzato dalla CA per firmare i certificati pubblici.
- **Issuer**: Nome della CA che emette i certificati.
- **Validity Period**: Data e ora d’inizio e fine validità del certificato. La data di scadenza si riferisce
all’utilizzo della chiave privata e non di quella
pubblica. Infatti questa può essere utilizzata anche successivamente alla scadenza per verificare la veridicità di quei file immagazzinati prima della scadenza.
- **Subject**: Nome del soggetto a cui è rilasciato il certificato.
- **Subject public key information**: identifica sia la chiave pubblica dell’intestatario del certificato che l’identificativo
dell’algoritmo di hashing e di crittografia pubblica con cui la chiave può essere utilizzata.
- **Issuer unique identifier**: Una stringa di bit opzionale per identificare univocamente una CA nel caso che lo stesso nome sia
stato assegnato ad un’altra entità.
- **Subject unique identifier**: Una stringa di bit opzionale per identificare univocamente il soggetto, Subject , nel caso che lo stesso nome sia stato assegnato ad un’altra entità.

Estensioni:
- .pem
- .cer , .crt , .der
- .p7b, .p7c
- .p12
- .pfx

### **Protocolli che supportano i certificati X.509**
- TLS/SSL 
- S/MIME (Secure Multipurpose Internet Mail Extensions)
- IPsec
- SSH
- Smart card
- HTTPS
- LDAP
- WS Security
- XMPP
- Altri...

# **Firewall**
Un **firewall** (letteralmente porta tagliafuoco) è un dispositivo di rete che **filtra tutto il traffico** che lo attraversa in base a una specifica politica d’accesso (**policy**). Si trova al confine fra due reti e tutto il traffico in transito tra le due reti deve passare attraverso di esso.  
- Protegge gli host di una rete fidata dal traffico ostile proveniente da una rete esterna o pubblica.
- Affinché possa svolgere in modo corretto il proprio compito deve essere collocato al confine delle due reti e rappresentare l’unico punto di accesso alla rete da proteggere : non deve essere possibile scavalcare il firewall tramite altri punti d’accesso (es. rete).

>Attenzione: **il compito** dei firewall **è stabilire quale traffico deve essere autorizzato non controllare che il traffico permesso non sia dannoso** : a questo scopo sono dedicati altri dispositivi.

I firewall possono essere realizzati in diversi modi:
1. apparato di rete specifico.
2. implementazione all’interno di un router.
3. implementato in un computer dedicato connesso con due schede di rete.
4. i "personal firewall": applicazioni software installate sugli host o sui server, spesso integrate nel sistema operativo, che hanno il compito di filtrare il
traffico in ingresso e in uscita dal sistema specifico.

I firewall possono essere di tipo diverso:
- Packet filtering firewall (stateless filtering)
- Stateful packet inspection firewall (Forwarding gateway(?))
- Application level firewall (Proxy(?))

>Il firewall realizza una separazione in zone con diverso grado di sicurezza all’interno di una rete

I firewall hanno una diversa complessità (e costo ) a seconda del tipo di servizio implementato e del livello a cui lavorano nello stack di rete.  
I firewall più semplici di tipo packet filter lavorano a livello di rete oppure a livello di rete/ trasporto.  
I firewall di livello applicativo lavorano a livello applicativo.  
Quindi:  
- a livello applicativo (application gateway, proxy)
- a livello di trasporto (circuit gateway)
- a livello rete (packet lter)
>Esistono anche ibridi: dynamic packet filter agiscono a livello rete e trasporto (e talvolta anche applicativo).
Possono essere realizzati via software o hardware (più veloci,
ma più costosi e meno flessibili nelle congurazioni).

|Rete Esterna|router|gatekeeper|gate|mailgate|Rete Interna|
- **Gatekeeper proxy applicativo**: raccoglie le richieste
applicative (Telnet, FTP, SMTP, ...) dall'interno e le manda verso l'esterno.
- **Gate**: filtra il traffico.

Grazie al firewall:
- In tutte le sottoreti si possono definire politiche di accesso.
- Solo i componenti esterni al firewall sono direttamente accessibili.
- Possibile regolare la direzionalità delle connessioni.
- Realizza una separazione in zone

### **Packet filtering firewall**
>Questo tipo di firewall applica un filtro basato sui parametri contenuti negli header di livello rete e/o di livello trasporto, ogni pacchetto viene valutato in modo indipendente senza tener conto di quelli che lo hanno preceduto.

A livello rete : vengono controllati soltanto gli indirizzi IP mittente e destinatario.

A livello di trasporto : il controllo viene effettuato sui parametri dell’ header di livello trasporto (es. flag SYN, flag ACK, source port , destination port).

Sono firewall efficienti in termini di performance, spesso questa funzionalità viene svolta dal border router.

### **Stateful Packet inspection firewall**
>Si tiene traccia dello stato del sistema e il filtraggio avviene considerando il traffico precedente con informazioni contenute in una **tabella** fidata delle connessioni, avviene
quindi sulla storia dei pacchetti o delle richieste.

Si può autorizzare, per esempio, il traffico in ingresso correlato a una precedente apertura di connessione in uscita.

Se un host della rete ha aperto una connessione in uscita verranno autorizzati i pacchetti in entrata riferiti a quella connessione il cui stato sarà **ESTABLISHED**.

Questa tecnica è più onerosa ma flessibile.

Operano un filtraggio applicativo analizzando il contenuto dei pacchetti e vengono talvolta detti **deep packet filters**.
- Analisi del traffico applicativo, la cui liceità va valutata
caso per caso
- Generalmente basati su pattern matching di stringhe
### **Application level firewall**
>I firewall di questa categoria operano un filtraggio di livello applicativo (detti anche deep packet inspection o proxy firewall).

Si comportano da **proxy applicativi**: intercettano la connessione, estraggono la parte dati del pacchetto, la esaminano e in caso di traffico autorizzato la inviano al destinatario.

Solitamente con metodi basati su pattern matching di stringhe o anomaly detection (analisi statistica per rilevare anomalie nel traffico).

Sono firewall meno efficienti in termini di performance: per ottenere buone prestazioni (elevata larghezza di banda).
### **Scrrened subnet**
Si usano due firewall per creare una zona di interdizione.

### **Zone di sicurezza: DMZ**
I firewall consentono di definire delle politiche di accesso realizzando una separazione in zone aventi diverso grado di sicurezza nell'architettura di rete.
>**DMZ** (DeMilitarized Zone o screened subnet): area della rete accessibile dall’esterno della rete il cui traffico viene controllato da un firewall e in cui vengono posti i server che offrono servizi agli utenti esterni (es. Web server, application server, SMTP server, …)

La DMZ ha un grado di sicurezza diverso dalla rete interna che deve essere protetta da accessi indesiderati.  
**I server contenenti dati privati devono essere posizionati sulla rete interna**.

Dalla DMZ viene bloccato ogni tentativo di accedere alla rete interna.  
Si possono realizzare più zone DMZ con diversi requisiti di sicurezza oppure si può connettere allo switch ciascuna macchina in DMZ su una VLAN differente per evitare che la compromissione di
una macchina porti alla compromissione delle altre (aumenta la complessità di gestione).

La realizzazione della DMZ con due firewall (zona cuscinetto) rende la DMZ accessibile sia dalla rete interna sia dalla rete esterna.

### **Zone di sicurezza: bastion host**
>Alcune architetture prevedono la presenza di un **Bastion host**: un nodo particolarmente protetto e capace di difesa prolungata che può essere lasciato al nemico senza danni per la rete interna.

Il Bastion host ospita generalmente un **proxy server** e viene **privato** di tutti **i servizi** non essenziali (come applicazioni, demoni ed utenti) per ridurre al minimo la minaccia di infezione del sistema stesso attraverso falle del software stesso.

Due principali architetture:
- **Single homed bastion host** = il firewall fa passare i pacchetti provenienti dall’esterno e diretti al bastion host, i pacchetti provenienti dall’esterno e diretti ad un server che non ha un livello di sicurezza elavato e i pacchetti provenienti dal bastion host e diretti verso l’esterno.  
Il traffico viene analizzato due volte, ma se il packet filter viene compromesso, il traffico esterno può raggiungere la rete interna.
- **Double homed bastion host** = previene i problemi causati dalla compromissione del packet filter perché un pacchetto deve “fisicamente” attraversare il bastion host.

### **Proxy**
>Un proxy è un componente che media le comunicazioni tra due altri componenti.  
Disaccoppia la comunicazione rendendola indiretta.  
Agisce sia da client (rispetto al server originale) che da server (rispetto al client originale).

Esistono diverse tipologie di proxy:
- **Web proxy**: caching di pagine web con memorizzazione delle pagine richieste dagli utenti della rete interna.
- **Anonymizing proxy**: servizi di anonimia del traffico web.
- **Reverse proxy**: mediano l’accesso di utenti esterni a risorse interne.
- **Proxy firewall**: mediano connessioni applicative, gestiscono aspetti di sicurezza dei protocolli e scartano traffico sulla base del contenuto applicativo.

### **Reverse proxy**
1. Connessione da utente esterno verso il Web Server.
2. Redirezione della connessione verso il Reverse Proxy.
3. Autenticazione, verifica, filtraggio, …
4. Inoltro verso il web server.

# **Access Control List (ACL)**
>**ACL** (Access Control List): fissa una politica di accesso, è una lista di istruzioni che devono essere considerate per stabilire se i pacchetti devono essere ammessi o scartati.

Nell’applicazione delle regole l’approccio è di tipo TOP-DOWN: la prima regola verificata interrompe il processo e porta alla decisione (normalmente l’ultima regola è la regola di default)

Per il **filtraggio** di tipo **stateless**: ogni pacchetto viene quindi esaminato singolarmente, indipendentemente dai pacchetti precedentemente ricevuti e da quelli successivi

Le ACL possono essere realizzate utilizzando due strategie:
- **Default Deny**: tutto il traffico non autorizzato esplicitamente viene scartato.
- **Default Permit**: tutto il traffico non esplicitamente scartato (presenza di una specifica regola di diniego) viene autorizzato.

**Principio del minimo privilegio**: ogni attore dispone del minimo dei privilegi necessari per raggiungere gli obiettivi assegnatigli dalle specifiche del sistema.

**Preferire** l’approccio **default deny** con una configurazione del firewall più stringente possibile ma che permetta l’erogazione dei servizi richiesti.
|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|...|...|...|...|...|...|...|...|

- **Varibili**: è molto diffuso l’uso delle variabili nelle ACL per indicare indirizzi IP (singoli o intere sottoreti); questo consente la modifica dei valori senza dover modificare la politica (es. INTERNA:= 192.168.0.0/24). Possono essere
istanziate sulla specica topologia di rete.
- **Verso**: IN / OUT oppure l’indicazione delle zone sorgente e destinazione precedentemente definite in variabili.
- **IP Sorgente/IP Destinazione**: IP da analizzare (livello rete) o variabili precedentemente definite.
- **Protocollo**: TCP, UDP, ICMP, IP.
- **Porta sorgente/porta destinazione**: porte da analizzare (livello transporto).
- **Ack**: 0 (aperture di connessione, SYN=1, ACK=0), 1 (no pacchetti di apertura connessione) o 0/1 (tutto il traffico).
- **Azione**: Deny/Permit

### **Protocolli firewall-friendly**
Protocolli come Telnet, SSH, rlogin, etc. sono semplici da gestire:
- Per loro natura implicano ruoli ben definiti del client e
server.
- Il pattern di scambio di messaggi è un semplice request/reply.
In generale invece esistono protocolli molto più elaborati che
richiedono politiche assai più sofisticate per applicare il LPP.
### **Esempio TELNET**
Vogliamo definire una ACL autorizzare solo connessioni Telnet dall’interno della rete aziendale verso uno specifico server telnet e bloccare il resto del traffico

Definire le variabili: INTERNA = 172.16.0.0/12, ESTERNA = not (INTERNA), ANY = Qualsiasi e TELNET_SERVER = 154.45.3.11  
Telnet è un protocollo di livello applicativo che utilizza una sola connessione TCP su porta 23 lato server, e porta alta (>1023)lato client.

|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|OUT|INTERNA|TELNET_SERVER|TCP|>1023|23|1/0|Permit|
|IN|TELNET_SERVER|INTERNA|TCP|23|>1023|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|ANY|DENY|

Se il protocollo di livello trasporto considerato è TCP, definire il valore del flag ACK nelle ACL è importante per ottenere politiche restrittive.
### **SSH con stateless filtering**
La politica da implementare autorizza solo connessioni SSH dall'interno della rete aziendale verso l'esterno.

Identichiamo SSH con i pacchetti TCP con porta destinazione 22 (si noti che talvolta si cambia la porta proprio per ragioni di sicurezza!)
sshSrvs := 159.149.70.13 and 159.149.70.42
|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|OUT|INTERNA|sshSrvs|TCP|>1023|22|1/0|Permit|
|IN|sshSrvs|INTERNA|TCP|22|>1023|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|*|DENY|
Si nota che i pacchetti provenienti dall'esterno della rete dovrebbero essere solo risposte del server: quindi ACK deve essere settato.  
Inoltre solo alcuni server ssh potrebbero essere autorizzati.
>Molto difficile da applicare: c'è una costante tensione fra essibilità e sicurezza.

### **SMTP**
Nella rete aziendale un solo server SMTP è autorizzato a gestire la posta elettronica con l'esterno.
> **SMTP** è un protocollo firewall-friendly.  
Client interni alla rete non passano per il firewall.
Si vuole:
- Scambiare posta elettronica: un Mail Server riceve e invia posta da e verso altri Mail Server.
- Ricevere posta elettronica: altri Mail Server si connettono al Mail Server aziendale agendo da client.
- Inviare posta elettronica: il Mail Server aziendale si connette ad altri Mail Server agendo da client.

smtpSrv := 159.149.70.23  
External := not(159.149.70.0/24)

|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|IN|External|smtpSrv|TCP|>1023|25|1/0|Permit|
|OUT|smtpSrv|External|TCP|25|>1023|1|Permit|
|OUT|smtpSrv|External|TCP|>1023|25|1|Permit|
|IN|External|smtpSrv|TCP|25|>1023|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|*|DENY|

### **FTP Attivo**
Non è un protocollo firewall-frindly
- Primo scambio di messagi su porta 21 provenienti da una porta alta.
- Poi dalla 20 verso una porta alta.
|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|OUT|Internal|External|TCP|>1023|21|1/0|Permit|
|IN|External|Internal|TCP|21|>1023|1|Permit|
|IN|External|Internal|TCP|20|>1023|1/0|Permit|
|OUT|Internal|External|TCP|>1023|20|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|*|DENY|

### **FTP Passivo**
- Primo scambio di messagi su porta 21 provenienti da una porta alta.
- Viene comunicata dal server la porta alta su cui inviare i messaggi.

|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|OUT|Internal|External|TCP|>1023|21|1/0|Permit|
|IN|External|Internal|TCP|21|>1023|1|Permit|
|OUT|Internal|External|TCP|>1023|>1023|1/0|Permit|
|IN|External|Internal|TCP|>1023|>1023|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|*|DENY|

### **RPC**
Il server RPC (attraverso il servizio Portmapper, nel caso UNIX), determina dinamicamente la porta (> 1023) da assegnare al servizio RPC e quindi non si conosce a priori la porta che il server RPC assegnerà al servizio.

|**Verso**|**IP Sorgente**|**IP Destinazione**|**Protocollo**|**Porta Sorgente**|**Porta Destinazione**|**Flag ACK**|**Azione**|
|--------|--------|--------|--------|--------|--------|--------|--------|
|IN|External|rpcSrv|TCP|>1023|111|1/0|Permit|
|OUT|rpcSrv|External|TCP|111|>1023|1|Permit|
|IN|External|rpcSrv|TCP|>1023|ANY|1/0|Permit|
|OUT|rpcSrv|External|TCP|ANY|>1023|1|Permit|
|ANY|ANY|ANY|ANY|ANY|ANY|*|DENY|
