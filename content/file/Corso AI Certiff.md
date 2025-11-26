(Riferimento a slide inviate per email)

Rivoluzione dell'intelligenza artificiale tramite [[Machine Learning]] e [[Deep Learning]].
## Intelligenza Artficiale
In generale qualsiasi cosa risponde a una richiesta anche gli assistenti vocali addestrati a riconoscere scenari predefiniti e basta.
Addestrare una AI è esattamente uguale a insegnare a un umano: 
1. Fornisco dei test (dei compiti da valutare)
2. Partono le "lezioni" tenute dal teacher bot
3. Ogni iterazione caccia le versioni dei bot che non arrivano alla sufficienza
Questo processo rende l'AI __scalabile__. Il processo è completamente sconosciuto al supervisor umano (sappiamo che funziona ma non come fa a funzionare nel senso quali processi fa per arrivare alla soluzione).
### Machine Learning
Sistemi che possono imparare e applicare la conoscenza a compiti non esplicitamente definiti in precedenza ( ad esempio: imparo l'algoritmo dell'addizione; so fare qualsiasi addizione. Ti mostro n esempio di X e Y; sai riconoscere X e Y).
#### Reti Neurali

##### Deep Learning
Utilizza [[Rete Neurale]] complesse con molti strati (ispirate al cervello). Impara dai dati in modo autonomo cioè riesce a migliorarsi e creare qualcosa di "nuovo" (ad esempio: imparo l'algoritmo dell'addizione; riesco a capire che utilizzando questo algoritmo con qualche accortezza ricavo l'algoritmo della moltiplicazione senza che nessuno me l'abbia mai presentata)

## AI Predittiva
AI predittiva è efficace in funzione all'efficacia e alla corretta rappresentazione della realtà che vuoi modellare dei dati che gli fornisci.
### Campi di applicazione
1.  __Regression__: Risponde a domande tipo "Quanto/i".
2.  __Classification__: Risponde a domande tipo "si o no" "Quale categoria?".
3.  __Manutenzione Predittiva__: Si usa l'AI per prevedere quando il sistema X potrebbe avere un problema
## AI Generativa (LLM)
E' un tipo di [[Rete Neurale]] profonda (basata su deep learning) specializzato nell'elaborazione e generazione di dati.
La generazione dell'LLM si basa sul calcolo del dato più probabile nel contesto in cui si trova.
Per eseguire questi calcoli LLM stende tutte le parole in uno spazio multidimenzionale, ogni parola viene suddivisa in categorie  (ad esempio: "auto" sarà più vicino alla categoria "veicolo veloce" rispetto "bicicletta)
#### Database Vettoriale
Ogni parola all'interno di un LLM viene trasformato in un vettore cui __"dimensione"__ (più corretto __modulo e direzione__) determina una caratteristica della parola (ogni categoria 
ha un __range di dimensioni__) (ad esempio: il range di "veicolo veloce" va da 1300 a 1400, "auto" verrà trasformato in 1340, "bicicletta" diventerà 1301, "aereo" diventerà 1380 (numeri non rappresentativi))

#### Reasoning Model
Permette di ottenere risposte molto più complesse e risoluzioni a problemi molto complessi.
Viene usato LLM per creare prompt che generano processi neurali.

### Prompting
Più contenuto inserisci nel prompt, più ottieni dal modello. Gli agenti usati da applicazioni che si appoggiano a LLM più generali riesco a verticalizzarli sul contesto del proprio sistema proprio tramite un prompt (ogni volta però che utilizzo l'agent creato è sempre bene __riallegare il prompt di contesto__).
La struttura di un prompt è definita de è la seguente:
1. Istruzione: devi definire cosa vuoi fare (esempio "traduci", "analizza")
2. Contesto
3. Esempi
4. Formato
5. Persona: individuo che sta 
6. Tono
#### Istruzione
Task che deve eseguire AI che posso essere di 2 tipi:
1. __Simple__-Task-Request: singola instruzione da eseguire
2. __Multi__-Task-Request: più instruzioni connesse una con l'altra
#### Contesto
Sono le informazioni aggiuntive che aiutano a contestualizzare il contesto all'IA. Un contesto efficace si costruisce così:
1. Qual'è il __background__ dell'utente?
2. Qual'è il __risultato__ che ci si aspetta?
3. Quali sono le __condizioni__ di partenza?
#### Esempi
Riguardano esempi di __Input e Output__ desiderati
#### Formato
La struttura che deve avere la risposta desiderata (ad esempio "Genera l'output in __formato tabellare__ con le colonne Nome, Età e Indirizzo"). E' fondamentale per ottenere la risposta nel formato corretto.
#### Persona
Il personaggio o al ruolo immaginario che deve assumere il chatbot per risponderti. Definire la persona aiuta a focalizzare il prompt su un destinatario specifico e rende le risposte più coerenti  (è un campo che fa parte del contesto).
#### Tono
Legato alla [Persona], definisce meglio ancora il ruolo che deve avere il chatbot durante la risposta (ad esempio "usa un tono amichevole" o "...come se stessi scrivendo a un amico" o "...mantenendo un tono professionale e oggettivo"). Utile farsi generare una lista di toni direttamente dall'AI.
#### Tecniche di prompt
1. __Zero__-Shot Prompting
2. __Few__-Shot Prompting
3. __Chain-of-Thought__: in un [Reasoning Model] già viene fatto. un modo per forzare la catena è aggiungere frasi come "spiega i passaggi" o "pensa ad alta voce", in ogni caso farsi spiegare perché ha fatto determinate cose.

#### Errori degli LLM
Esistono degli errori che producono negli output errati
1. Essere vaghi
2. Mancanza di background
3. Allucinazioni: riempire buchi di informazioni con falsità
4. "Conoscenza" non aggiornata: ovvero conoscono il mondo fino a un certo punto. Spesso usano, per provare a riempire buchi d'informazione, a fare ricerche su internet e spesso e volentieri usano forum come Reddit (questo trascendere dai deep research)
#### Tecniche di validazione del prompt
Per avere risultati migliori senza "svarioni" posso aggiungere delle frasi che risolvono alcuni problemi di allucinazioni e condizionamenti:
1. "evita tutti i bias"
2. "evita di darmi ragione a prescindere"
3. "non aggiungere informazioni per riempire buchi"

#### Automation Process Canvas
E' un framework strutturato e progettato per aiutare le organizzazioni a identificare, analizzare e pianificare l'automazione dei processi aziendali utilizzando LLM.
Un esercizio che cerca di rispondere alla domanda "cosa posso fare con l'AI?".
1. __Mappatura dei Processi__: definire i processi (una sequenza di passaggi per trasformare un input(esempio: risorse) in un output(esempio: prodotto)) da dover gestire (esempio: Reparto Commerciale -> Gestione..)
2. __Suddivisione in Task__: dividere il processo (atomizzazione) in piccole attività che sono necessaria a completare il processo (__divide et impera__). I task possono essere di 2 tipi:
	1. __Strategico__: esempio "definizione degli obbiettivi di una campagna pubblicitaria", "pianificazione del budget"(facile da __Velocizzare__ e non automatizzare con un LLM, non si può automatizzare per adesso essendo sicuri del risultato). Dopo la generazione del task il consiglio è di chiedere a un altro LLM di analizzare prima lui in modo critico il task appena generato e in conclusione rivedere tutto il risultato
	2. __Operativo__: esempio "creazione dei contenuti per la campagna"
3. __Informazioni Aggiuntive__: le informazioni aggiuntive da inserire sono i task li posso definire tramite 2 parametri __Frequenza__ e __Effort__ (tabelle in presentazione)
4. __Posizionamento sul Canvas__: il canvas non è altro che una rappresentazione cartesiana (dove sulla x c'è l'__Effort__ e sulla y la __Frequenza__) dei task
