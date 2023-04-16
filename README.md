# Filius-Router
Impostazione di due LAN comunicanti tramite un router.

La relazione dettagliata della prova si trova nel pdf allegato.

Domande a cui rispondere:
1) A cosa serve il server DHCP
2) Perchè inizialmente i PC delle due reti non si raggiungevano con ping
3) Quale protocollo viene utilizzato dal comando ping

Risposte:
1) DHCP (da relazione): è un servizio che si utilizza per assegnare indirizzi IP a dei dispositivi in modo automatico. E’ possibile impostare su di esso il range di indirizzi IP che possono essere forniti, specificando un valore minimo e uno massimo.
Si può impostare inoltre l’indirizzo IP del gateway (che nel caso della prova coincideva con il router) ed il DNS Server della rete. Su filius dopo aver configurato il DHCP Server è necessario abilitare il servizio su ogni dispositivo che ne necessita.

2) I pc delle due reti non comunicavano tramite ping per i seguenti motivi:
  - il DHCP server della prima rete non era impostato in modo da definire il gateway dei dispositivi collegati ad esso: di conseguenza questi ultimi non disponevano di una via di uscita dalla rete.
  - sul pc della seconda rete non era impostata l'opzione che specifica l'utilizzo del DHCP come metodo di configurazione, il pc disponeva perciò di una configurazione statica ed errata.

3) Il comando PING utilizza il protocollo ARP:
  - PING (da relazione): è un comando eseguibile dal prompt dei comandi, viene utilizzato per effettuare controllo sulla diagnostica di una rete in quanto è possibile contattare un dispositivo tramite il proprio indirizzo ip ed ottenere una risposta (pong) che comunica se il dispositivo è presente sulla rete (fornendo il tempo impiegato a rispondere) o meno.
Se il dispositivo non è presente sulla rete o il ping non è in grado di arrivare ad esso (ad esempio potrebbe essersi compromesso un collegamento), il risultato del ping sarà un Timeout, il quale indica che non è stata ricevuta alcuna risposta.
Nel caso in cui il dispositivo sia presente e fornisca una risposta, è possibile visualizzare a schermo la latenza del ping stesso, cioè il tempo durante il quale il pacchetto naviga sulla rete prima che ritorni una risposta accettabile. La latenza viene misurata in millisecondi.
Questo comando utilizza il protocollo ARP come spiegato successivamente.
  - Protocollo ARP (Address Resolution Protoco l - da relazione): opera al livello di accesso alla rete, è necessario per definire le relazioni tra indirizzi IP e MAC.
Questo servizio può essere utilizzato, ad esempio, quando si vuole comunicare ad un dispositivo di una sottorete diversa da quella in cui ci si trova per conoscere l’indirizzo IP del gateway. 
In questa prova è stato utilizzato questo protocollo per far popolare la MAC table allo switch di una rete, in quanto è stato fornito solamente l’indirizzo IP tramite un ping (che utilizza infatti questo protocollo).
Il primo ARP che viene trasmesso sulla rete è inviato tramite broadcast (quindi il MAC address sarà uguale a FF:FF:FF:FF:FF:FF), il destinatario che riconosce di avere indirizzo IP uguale a quello contenuto nell’ARP lo completa con il proprio MAC address per poi reinviarlo al mittente. Se il messaggio iniziale deve uscire da una LAN (come nel caso della prova), inizialmente esso dovrà arrivare al router per poi essere indirizzato dal gateway (del quale MAC address sarà riconosciuto da un’ARP locale). Tendenzialmente il router indirizzerà il messaggio tramite il percorso migliore rilevato dalla routing table.

# RELAZIONE DELLA PROVA (allegata in pdf)

**Data in cui si è svolta la prova:** 3 Febbraio 2023

**Obiettivo:** impostare due reti LAN comunicanti che contengano 1 Notebook collegato ad uno switch che comunica a sua volta con quello della rete opposta tramite un router, e verificare che esse siano effettivamente in grado di comunicare effettuando un ping rivolto a un dispositivo dell’altra rete.
Ogni rete deve disporre di un server con servizio DHCP ed uno con servizio DNS.
L’intera prova è stata eseguita utilizzando Filius.

**Dispositivi coinvolti:**
● 2 Notebook (PC1 e PC2)
● 2 Computer con funzione di server DHCP (Server DHCP e Server DHCP 2)
● 2 Computer con funzione di server DNS
● Router
● Cavi

**Riferimenti teorici:**
● *Ping*: è un comando eseguibile dal prompt dei comandi, viene utilizzato per
effettuare controllo sulla diagnostica di una rete in quanto è possibile
contattare un dispositivo tramite il proprio indirizzo ip ed ottenere una risposta
(pong) che comunica se il dispositivo è presente sulla rete (fornendo il tempo
impiegato a rispondere) o meno.
Se il dispositivo non è presente sulla rete o il ping non è in grado di arrivare
ad esso (ad esempio potrebbe essersi compromesso un collegamento), il
risultato del ping sarà un Timeout, il quale indica che non è stata ricevuta
alcuna risposta.
Nel caso in cui il dispositivo sia presente e fornisca una risposta, è possibile
visualizzare a schermo la latenza del ping stesso, cioè il tempo durante il
quale il pacchetto naviga sulla rete prima che ritorni una risposta accettabile.
La latenza viene misurata in millisecondi.
Questo comando utilizza il protocollo ARP come spiegato successivamente.
● Protocollo ARP (Address Resolution Protocol): opera al livello di accesso alla
rete, è necessario per definire le relazioni tra indirizzi IP e MAC.
Questo servizio può essere utilizzato, ad esempio, quando si vuole
comunicare ad un dispositivo di una sottorete diversa da quella in cui ci si
trova per conoscere l’indirizzo IP del gateway.
In questa prova è stato utilizzato questo protocollo per far popolare la MAC
table allo switch di una rete, in quanto è stato fornito solamente l’indirizzo IP
tramite un ping (che utilizza infatti questo protocollo).
Il primo ARP che viene trasmesso sulla rete è inviato tramite broadcast
(quindi il MAC address sarà uguale a FF:FF:FF:FF:FF:FF), il destinatario che
riconosce di avere indirizzo IP uguale a quello contenuto nell’ARP lo completa
con il proprio MAC address per poi reinviarlo al mittente. Se il messaggio
iniziale deve uscire da una LAN (come nel caso della prova), inizialmente
esso dovrà arrivare al router per poi essere indirizzato dal gateway (del quale
MAC address sarà riconosciuto da un’ARP locale). Tendenzialmente il router
indirizzerà il messaggio tramite il percorso migliore rilevato dalla routing table.
● *DHCP*: è un servizio che si utilizza per assegnare indirizzi IP a dei dispositivi
in modo automatico. E’ possibile impostare su di esso il range di indirizzi IP
che possono essere forniti, specificando un valore minimo e uno massimo.
Si può impostare inoltre l’indirizzo IP del gateway (che nel caso della prova
coincideva con il router) ed il DNS Server della rete. Su filius dopo aver
configurato il DHCP Server è necessario abilitare il servizio su ogni dispositivo
che ne necessita.
● *DNS*: è un servizio che ha lo scopo di assegnare dei nomi a degli indirizzi IP,
è utilizzato ad esempio per pagine web in quanto sarebbe scomodo e
soprattutto inefficiente dover scrivere ogni volta l’intero indirizzo IP relativo
alla pagina che si vuole visitare: come soluzione si sceglie abitualmente
questo servizio.

**Svolgimento:**
1) *Impostazione DHCP server setup:*
Selezionando il Computer scelto come Server DHCP è possibile configurare
quest’ultimo tramite il tasto sotto riportato, che compare all’interno della
finestra in basso alla schermata.

<img src="images\tastoDHCP.png" width="350" title="tastoDHCP">

<img src="images\impostazioneDHCP.png" width="350" title="impostazioneDHCP">

Per quanto riguarda gli altri dispositivi, essi andranno collegati al server DHCP tramite uno switch ed in seguito andrà spuntata l’opzione che permette l’uso di tale servizio dal dispositivo.

<img src="images\attivazioneDHCP.png" width="350" title="attivazioneDHCP">

2) *Simulazione*
Sistema risultante:

<img src="images\rete.png" width="350" title="rete">

Dopo aver impostato correttamente gli indirizzi IP relativi ai vari dispositivi (ad
esempio come in figura), è possibile avviare la simulazione.
Se i collegamenti sono stati effettuati in modo corretto e sono stati impostati indirizzi
IP validi, a simulazione appena avviata si possono vedere i cavi colorarsi di verde (a
causa dei vari messaggi di controllo inviati prima della comunicazione effettiva, ad
esempio lo switch popolerà la MAC table sfruttando il protocollo ARP, come spiegato
successivamente).

3) Prompt dei comandi:

Per installare il prompt dei comandi da un qualsiasi Computer o Notebook sulla rete, aprire Software Installation e spostare “Command Line” tra le applicazioni installate (“Installed”), per poi applicare i cambiamenti tramite il tasto in basso al centro (“Apply changes”).

<img src="images\installazione prompt.png" width="350" title="installazione prompt">

4) *Ping a un dispositivo della rete opposta:*

<img src="images\ping.png" width="350" title="ping">

Si può facilmente notare che la comunicazione in questo caso è andata a buon fine in quanto ogni messaggio che si è provato ad inviare è giunto a destinazione così come le risposte dal dispositivo coinvolto (pong).

```
4 packet(s) transmitted, 4 packet(s) received, 0% packet loss
```
=> 4 pacchetti trasmessi, 4 pacchetti ricevuti, non è stato perso alcun pacchetto nel
tentativo di comunicare con il dispositivo.

Durante il ping si possono vedere i cavi illuminarsi di verde.

5) *Approfondimento sul comportamento dello switch rispetto al ping:*
Quando si esegue un ping di un indirizzo ip dal prompt dei comandi, è possibile
notare come i cavi si illuminino in questo ordine:
1) host => switch
2) switch => tutti i dispositivi connessi
3) dispositivo contenente l’ip specificato nel ping => switch
Questo avviene in quanto lo switch non conosce il MAC address del dispositivo a cui
è dedicato l’indirizzo IP a cui ci si rivolge, quindi invierà prima un messaggio in
broadcast a scopo di popolare la propria MAC table, per poi reindirizzare il pacchetto
del ping in maniera diretta al dispositivo desiderato.
Lo switch opera tramite i MAC address, per questo non dovrebbe essere in grado
trasmettere messaggi in modalità broadcast (come gli hub), ma ciò è necessario
affinché prima si popoli la MAC table per poi reindirizzare il messaggio iniziale al
corretto destinatario.
Riassumendo, lo switch trasmette in broadcast un messaggio con il quale richiede ai
dispositivi connessi di comparare l’indirizzo IP specificato nel ping con il proprio, la
risposta arriverà solo dal dispositivo per il quale questa condizione è soddisfatta
(questa risposta contiene il MAC address del dispositivo coinvolto, che arriverà allo
switch e verrà collocato nella MAC table).
La MAC table definisce la porta corrispondente ad un dato indirizzo MAC, ciò che
invece unisce l’indirizzo IP al relativo MAC address è il protocollo ARP (Address
Resolution Protocol).

**Conclusione:** tramite questa prova abbiamo potuto osservare il funzionamento del
protocollo ARP utilizzando il comando ping e abbiamo intrapreso una prima
esperienza nella gestione di reti connesse tra loro (perciò anche la suddivisione e
configurazione dei vari dispositivi e l’assegnazione di indirizzi IP, sia manualmente
sia utilizzando DHCP Server).
