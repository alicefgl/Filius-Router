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

2)I pc delle due reti non comunicavano tramite ping per i seguenti motivi:
  - il DHCP server della prima rete non era impostato in modo da definire il gateway dei dispositivi collegati ad esso: di conseguenza questi ultimi non disponevano di una via di uscita dalla rete.
  - sul pc della seconda rete non era impostata l'opzione che specifica l'utilizzo del DHCP come metodo di configurazione, il pc disponeva perciò di una configurazione statica ed errata.

3) Il comando PING utilizza il protocollo ARP:
   - PING (da relazione): è un comando eseguibile dal prompt dei comandi, viene utilizzato per effettuare controllo sulla diagnostica di una rete in quanto è possibile contattare un dispositivo tramite il proprio indirizzo ip ed ottenere una risposta (pong) che comunica se il dispositivo è presente sulla rete (fornendo il tempo impiegato a rispondere) o meno.
Se il dispositivo non è presente sulla rete o il ping non è in grado di arrivare ad esso (ad esempio potrebbe essersi compromesso un collegamento), il risultato del ping sarà un Timeout, il quale indica che non è stata ricevuta alcuna risposta.
Nel caso in cui il dispositivo sia presente e fornisca una risposta, è possibile visualizzare a schermo la latenza del ping stesso, cioè il tempo durante il quale il pacchetto naviga sulla rete prima che ritorni una risposta accettabile. La latenza viene misurata in millisecondi.
Questo comando utilizza il protocollo ARP come spiegato successivamente.
  -Protocollo ARP (Address Resolution Protocol - da relazione): opera al livello di accesso alla rete, è necessario per definire le relazioni tra indirizzi IP e MAC.
Questo servizio può essere utilizzato, ad esempio, quando si vuole comunicare ad un dispositivo di una sottorete diversa da quella in cui ci si trova per conoscere l’indirizzo IP del gateway. 
In questa prova è stato utilizzato questo protocollo per far popolare la MAC table allo switch di una rete, in quanto è stato fornito solamente l’indirizzo IP tramite un ping (che utilizza infatti questo protocollo).
Il primo ARP che viene trasmesso sulla rete è inviato tramite broadcast (quindi il MAC address sarà uguale a FF:FF:FF:FF:FF:FF), il destinatario che riconosce di avere indirizzo IP uguale a quello contenuto nell’ARP lo completa con il proprio MAC address per poi reinviarlo al mittente. Se il messaggio iniziale deve uscire da una LAN (come nel caso della prova), inizialmente esso dovrà arrivare al router per poi essere indirizzato dal gateway (del quale MAC address sarà riconosciuto da un’ARP locale). Tendenzialmente il router indirizzerà il messaggio tramite il percorso migliore rilevato dalla routing table.
