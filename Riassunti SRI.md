# **Integrità e autenticazione del messaggio**
>Non è possibile per due persone comunicare in modo sicuro su un canale sicuro utilizzando la crittografia.

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