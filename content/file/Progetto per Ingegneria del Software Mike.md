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
### Requisiti Funzionali

#### Must
1. M01) Il Sistema deve prelevare la [[Carriera]] e l'[[Anagrafica Studente]] da [[Gestione Carriera Studente]] 
2. M02) Il Sistema deve consentire all'unità didattica di ([[Generare un Prospetto di Laurea]]:classe):user case) con tutti laureandi per la [[Commissione]] (come in fig. n)(figure ed appendici vanno in fondo al documento)
3. M03) Il Sistema deve fornire una interfaccia grafica all'[[Unità Didattica]](attrice del sistema)
4. M04) Il Sistema deve consentire all'[[Unità Didattica]] di accedere ai [[Prospetti di Laurea]] dei laureandi per la [[Commissione]] (sono tutti insieme)(noi dobbiamo consentire solo l'accesso ai prospetti e non la visualizzazione, per quest'ultima ci pensa il pdfReader del browser, noi forniamo solo l'url)
5. M05) Il Sistema deve consentire all'[[Unità Didattica]] di inviare a ciascun laureando il proprio prospetto di laurea tramite un unico pulsante
6. M06) Il Sistema, quando fa una generazione, elimina i precedenti prospetti generati
7. M07) Il Sistema deve consentire all'[[Amministratore]] di aggiungere un nuovo corso di laurea tramite [[File di Configurazione]]( in questo file non inserisco dati che si "consumano" ma che riutilizzo, ad esempio la data di laurea di un appello dopo che è passata si e "consumata", una informazione che non si consuma è ad esempio TMAX che è un parametro fisso che riutilizzo ad ogni utilizzo del sistema per sempre(fino a che non cambia di sistema))
8. M08) Il Sistema deve consentire all'[[Amministratore]] di configurare i parametri di calcolo tramite file di configurazione (a livello software ogni volta che avvio il sistema faccio un parse del file per verificare che non ci siano modifiche
9. M09) Il file di configurazione (in JSON) deve poter essere modificato dall'[[Amministratore]] come file di testo
10. M10) il Sistema deve consentire all'[[Amministratore]] di configurare gli [[Esami Informatici]] tramite file di configurazione
11. M11) Il Sistema deve consentire all'[[Unità Didattica]] di inserire la lista delle matricole con il metodo di "copy-paste" o di inserimento
12. M12) Il [[File di Configurazione]] deve essere completato dell'informazioni che necessita dall'[[Amministratore]] in tutti i campi necessari per quel corso di laurea (struttura del file in fig. n)
13. M13) Il Sistema deve consentire all'[[Unità Didattica]] di CONFIGURARE un Filtro Manuale sugli esami visualizzati (per il singolo o per tutti gli studenti inseriti) per poter individuare gli esami che non sono necessari al conseguimento della laurea in esame
  
### Requisiti non Funzionali 
1. N01) Il Sistema deve essere sviluppato in linguaggio PhP
2. N02) Il Sistema deve essere sviluppato su IDE PhpStorm
3. N03) Il Sistema deve essere messo in produzione in ambiente WordPress
4. N04) Il Sistema non deve contenere credenziali personali nel codice o nei file di 		configurazione
5. N05) Il Sistema deve conservare dati personali lo stretto necessario (ovvero dopo 2 settimane dall'appello cancello)(norma GDPR)
6. N06) Il Sistema deve essere protetto da accessi non autorizzati (verrà fatto con WordPress)
7. N07) Il Sistema deve essere portabile su altri computer con il medesimo ambiente di sviluppo e produzione
8. N08) il SIstema deve avere un manuale di installazione , d'uso e di configurazione
### Configurazione Software
Serve una pagina per poter configurare il software, si seleziona quale CdL modificare e poi selezionare quale sezione modificare (reportistica, filtri ecc).
# Attori
### Cineca
Cineca è un consorzio interuniversitario senza scopo di lucro formato da 120 enti pubblici. È il consorzio che si occupa di sviluppare il software per la gestione delle università.