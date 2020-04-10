# **Firma digitale**
La **firma digitale**, equivalente elettronico della firma autografa su carta, è associata stabilmente al documento elettronico sulla quale è apposta e ne attesta con certezza l’integrità, autenticità e la non ripudiabilità.

Per generare una firma digitale è necessario un **kit** (dispositivo + software).
Il file firmato digitalmente **deve** essere **certificato** dall’ente certificatore prima dell’invio.
Con il certificato il destinatario ottiene la **chiave pubblica** sicura per verificare identità del mittente e integrità del documento.
L’algoritmo di apposizione della firma digitale prevede la creazione di un’impronta (message digest) attraverso la funzione di hash.

# **Certificati digitali**
Una terza parte fidata, l’autorità di certificazione (**CA**), certifica il legame utente/chiave pubblica mediante apposito certificato digitale, e garantisce che la chiave pubblica di qualcuno. che otteniamo da un registro pubblico sia stata rilasciata proprio da quella persona.

Certificato reale è cartaceo, emesso da un'entità conosciuta e **associa l’identità** di una persona **al** suo **aspetto fisico**.  
Certificato digitale è elettronico, **associa l’identità** di una persona **ad una chiave pubblica**, emesso da CA riconosciuta, firmato con la chiave privata della CA. Formato tipico X.509 (raccomandato dall’ITU International Telecommunication Union).

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
Alice genera una coppia di chiavi pubblica/privata (k, k^-1) e vuole rendere k pubblica
1. Alice spedisce k a CA (Certification Authority)
2. CA verifica che Alice conosco k^-1
3. CA genera Ck e lo spedisce a Alice; Alice spedisce Ck quando usa k

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
 ### **Revoca del certificato**
Ragioni:
- Cambio dei dati personali
- Licenziamento, dimissioni
- Compromissione della chiave privata
- La richiesta di revoca può arrivare dall’utente o dall’emettitore.  

La revoca avviene mediante il CRL (Certificate Revocation List).  
**Certificate Revocation List**: lista di certificati revocati prima della loro naturale scadenza temporale.  
Firmata digitalmente dalla stessa CA che ha emesso il certificato che è stato revocato.
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
