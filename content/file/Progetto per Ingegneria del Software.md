#uni 
> [link materiale ausiliario](https://docenti.ing.unipi.it/m.cimino/isw/res/progetto/)


Progettare un **Sistema** che generi prospetti di Laurea.
Si collega al Gestione Carriera Studente.
Il sistema ha una interfaccia ad oggetti per Cineca ESSE3 (software gestione carriera studente).
Metodi esemio:
GestioneCarrieraStudente.restituisciAnagraficaStudente(123456)
GestioneCarrieraStudente.restituisciCarrieraStudente(123456)
# Note
- Gli esami che non fanno media vengono indicati con il voto=0;
- Il software deve essere configurabile nei parametri, parametri $T$ e $C$.
# Requisiti
## Requisiti Funzionali
##### MUST HAVE (DEVE): REQUISITO FONDAMENTALE PER IL SISTEMA
- M01) Il Sistema deve consentire all'unità  didattica di generare un prospetto di laurea con tutti laureandi per la commissione 
- M02) Il Sistema deve fornire una interfaccia grafica all'unità  didattica
- M03)
- M04) Il Sistema deve consentire all'unità didattica di generare il prospetto di laurea del singolo laureando per il medesimo
- M05) Il sistema deve consentire all'unità didattica di accedere ai prospetti di laurea dei laureandi.
- M06) Il sistema deve consentire all'unità didattica di inviare a ciascun laureando il proprio prospetto di laurea
- M07) Il Sistema deve fornire una interfaccia grafica all'unità didattica
- M08) Il Sistema deve consentire all'amministratore di aggiungere un nuovo corso di laurea tramite file di configurazione
- M09) Il Sistema deve consentire all'amministratore di passare parametri di calcolo e reportistica tramite file di configurazione (formato email per studenti)
- M10) Il Sistema deve consentire all'amministratore di configurare il filtro esame tramite file di configurazione
- M11) Il sistema deve consentire all'amministratore di configurare gli esami informatici tramite file di configurazione
- M12) Il Sistema deve consentire la verifica automatica della completezza della carriera del laureando (es. tutti gli esami superati, nessun debito formativo).
- M13) Il Sistema deve gestire eventuali errori di connessione con il sistema Gestione Carriera Studente e notificare l’unità didattica==.
- M14) Il Sistema deve registrare in un log tutte le operazioni di generazione e invio prospetti==.

1. Il sistema prende in ingresso: Corso di Laurea (menù a scelta), Data di Laurea (da Calendario), Elenco di Matricole dei Laureandi (inserimento libero) - Segreteria Centrale, Unità didattica (personale di Ateneo - Dottoressa D'Attilio)
2. Il sistema preleva le carriere dei laureandi dal sistema di Gestione Carriera Studente
3. Il sistema invia una email ad ogni laureando con il proprio ==prospetto==
4. Il sistema fornisce una interfaccia grafica all'==unità didattica== per inserire: il corso di laurea, data di laurea, elenco matricole di laureandi.
5. La ==carriera== è composta da: matricola, corso di laurea, anno di immatricolazione e, per ogni esame
##### SHOULD HAVE (DOVREBBE): REQUISITO IMPORTANTE CHE PERO' PUO' ESSERE OMESSO
S01) Il Sistema dovrebbe consentire all'amministratore di configurare il valore della lode
S02) Il Sistema dovrebbe consentire la cancellazione di tutti i dati relativi all'appello di laurea
##### COULD HAVE (POTREBBE): REQUISITO OPZIONALE (DA REALIZZARE SE C'E' TEMPO)
C01) Il Sistema potrebbe consentire all'unità  didattica di proseguire l'invio dei prospetti di laurea dopo una interruzione
C02) Il Sistema potrebbe fornire una interfaccia grafica all'amministratore per accedere ai file di configurazione
##### WANT TO HAVE (VORREBBE): REQUISITO CHE PUO' ESSERE REALIZZATO IN SUCCESSIVE RELEASE
W01) Il Sistema vorrebbe consentire all'unità  didattica di ricevere una email con la conferma di invio dei prospetti
W02) Il Sistema vorrebbe consentire all'unità  didattica di generare un prospetto con le statistiche dell'appello di laurea
## Requisiti non Funzionali 
- Serve una pagina per poter configurare il software, si seleziona quale CdL modificare e poi selezionare quale sezione modificare (reportistica, filtri ecc).
- GDPR il sistema deve coservare i dati non oltre il necessario
- il sistema deve essere sviluppato su IDE Phpstorm
- Il sistema deve essere protetto da accessi non autenticati
- il sistema deve essere messo in produzione su ambiente wordpress
- il sistema non deve contenere credenziali personali enl codice o nei file di configurazione
- il sistema deve essere portabile su altri computer con il medesimo ambiente di sviluppo
- il sistema deve avere un manuale di uso ed installazione
# Attori
### Cineca
Cineca è un consorzio interuniversitario senza scopo di lucro formato da 120 enti pubblici. È il consorzio che si occupa di sviluppare il software per la gestione delle università.
# Caso d'uso dettagliato
## InviaProspettiCommissione
1. UnitaDidattica seleziona il CdL
2. SYSTEM mostra il *CdL* selezionato
3. UnitaDidattica clicca sul pulsante Invia Prospetti
4. for each prospetto laureando
   4.1. if il prospetto è stato correttamente inviato
      4.1.1. SYSTEM visualizza il messaggio "inviato prospetto n di TOT"
      4.1.2. attende 13 secondi
   4.2. else 
      4.2.1. SYSTEM visualizza il messaggio "errore di invio prospetto n di TOT"
      4.2.2. exit loop 
        end if 
   end for each 
# gdpr
1. dopo che abbiamo costruito l'oggetto con il file json, il sistema deve eliminare ogni informazione non utilizzata
# Consigli
1. aggiungere note nel progetto, altrimenti alla discussione non si ricorda il perché delle cose