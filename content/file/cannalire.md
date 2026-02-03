

18/11
- [x] Rinnovo della licenza. Chiarimento paradigma controllore-modello-vista: GeneratoreProspetti, CarrieraStudente, ProspettoStudente. Ridenominazione della classi candidate secondo UpperCamelCase. Modifica e aggiunta dei requisiti inerenti ai prospetti di laurea specificando il contenuto di essi. Rimodellazione del diagramma UML. Rimossa classe CommissioneLaurea poiché non utile al Sistema, a essa non vengono spediti i prospetti via mail ma in formato cartaceo.

20/11
- [x] Dettagliamento del caso d'uso GeneraProspetti in forma testuale. Dubbi su come farlo in ambiente VisualParadigm: assenti ID, descrizione e flow. Dubbi su momento della generazione dei diagrammi di sequenza in seguito alla lettura di VP4UML_DetailedUseCase.pdf. Glossario: aggiunta di Gestione Carriera Studenti, CdL, Carriera dello studente, studente come alias di laureando, aggiunta di plurali. Possibilità di classe AnagraficaLaureando da confermare successivamente, ridondanza con Laureando?

02/12
- [ ] Esportazione del diagramma dei casi d'uso nella documentazione. Rimozione di tabelle di esportazione non utili alla documentazione. Dettagliamento del caso d'uso ApriProspetti. Modifica di GeneraProspetto in GeneraProspetti. Rivisitazione dei casi d'uso GeneraProspetto: aggiunta di if in caso di errore nella generazione dei prospetti. Perplessità emerse sulle classi ipotizzate durante la revisione dei casi d'uso dettagliati.

09/12
- [ ] Confronto con collega circa alcune criticità nelle successive fasi di progetto. Esportazione dei casi d'uso in dettaglio nella documentazione con conseguente riformattazione. Prove di realizzazione CRC card su Visual Paradigm riguardando anche la teoria di queste. Ascolto di chiarimenti dei colleghi riguardo i momenti del progetto in cui devono essere generati i diagrammi di sequenza. Prova preliminare di generazione dei diagrammi di sequenza.

11/02
- [ ] Revisione del lavoro già svolto nel workflow requisiti, analisi del lavoro da svolgere nel workflow analisi. Ripasso teorico del workflow, con attenzione all'ordine da seguire nella realizzazione degli artefatti. Ripresa familiarità con l'interfaccia di Visual Paradigm in particolare per la realizzazione dei nuovi artefatti.

12/02
- [x] Emersa durante la realizzazione delle CRC cards la necessità delle classi Esame, GestioneCarrieraStudente. Conseguente evidenziazione nell'elenco dei requisiti. Separazione di GeneraProspetti in 2 classi diverse per studente e commissione, separazione di CarrieraStudente in 2 classi diverse per discriminare gli studenti di ingegneria informatica. Realizzate prime CRC cards: in particolare individuazione degli attributi della classe esame a partire dal file JSON. Aggiungere sottoclasse esame inf?

13/02
- [ ] Proseguita la realizzazione delle CRC cards. Particolari attenzioni per gli attributi della classe CarrieraLaureando, dubbi su quelli effettivamente rilevanti. GeneratoreProspettiLaureandi come collaboratore di GeneratoreProspettiCommissione. Classi diverse per prospetto e generatore del prospetto? Generazione delle classi nel diagramma di analisi a partire dalle CRC. Cambio nomi delle funzioni membro in lower camel case.

14/02
- [ ] Approfondito confronto con collega in merito alla possibilità di modifica delle classi inerenti alla generazione dei prospetti. Permangono dubbi. Aggiunta di operazioni nel diagramma di analisi con conseguente revisione delle responsabilità nelle rispettive CRC cards. Dipendenze nel diagramma di analisi in seguito a ripasso degli aspetti teorici. Necessario array esami all'interno della classe carriera? Dubbi su generalizzazione/extend per carriera studente inf.

15/02
- [x] Revisione del diagramma di analisi: modifica di di alcune dipendenze da `<<use>>` a `<<call>>`, rimozione degli operatori di visibilità poiché non consigliati in analisi. Per stesso motivo non trattata molteplicità. Ulteriori conferme su bontà di quanto svolto in seguito a confronto con collega. Iniziata realizzazione dei diagrammi di sequenza per apertura e invio dei prospetti. Necessario usare funzioni a questo livello? Confronti su aspetti teorici anche con workflow di progetto.

16/02
- [ ] Diagrammi di sequenza: ultimato quello relativo all'invio dei prospetti e quello riguardante la loro creazione. Riscontrate notevoli difficoltà con l'editor, tra cui la modifica del tipo di frammento in break. Lieve cambiamento al caso d'uso GeneraProspetti: rimossa possibilità che vi sia un errore durante la generazione. Durante la realizzazione del diagramma di flusso per questo caso d'uso si è deciso di fare il frammento riferimento InizializzaCarriera per la gestione del caso di ing inf.

17/02
- [ ] Modifiche al diagramma di sequenza di GeneraProspetti: aggiunta richiesta  esami elenco informatici da file configurazione durante la creazione del prospetto. Invertite l'aggiunta del prospetto dello studente a quello della commissione e l'aggiunta della simulazione in modo da non dover impiegare anche una classe ProspettoSimulazione. Modifica dipendenza <<extend>> in generalizzazione per carriera studente inf. Impaginazione del workflow analisi, serie problematiche con renderizzazione .svg.

18/02
- [ ] Ripasso PHP anche grazie all'aiuto di un collega. Ridiscusse con lui alcune scelte implementativa. Iniziata la realizzazione delle classi Carriera, GestioneCarriera, Esame. Emersa la necessità del campo dataIscrizione nel laureando per verificare se abbia diritto al bonus. Dubbi su esami sovrannumerari: mettere esami cdl in file configurazione e verificare se il nome esame sia presente? sovran_flag? Rivedere anche gestione esame informatici, forse flag in classe esame superfluo.

20/02
- [ ] Risolti dubbi su esami da rimuovere, sovran_flag, esami che non fanno media, grazie a confronto con collega. Realizzata quindi classe FileConfigurazione e bozze dei relativi file .json. Piccole modifiche nelle classi già realizzate e loro completamento, in particolare gestione degli esami. Da decidere se organizzare diversamente dati di GestioneCarriera. Realizzata classe CarrieraStudenteInf e gestione relativo flag inf. Distinzione in cfuCurricolari e cfuMedia in CarrieraStudente.

21/02
- [ ] Iniziata realizzazione delle classi GeneraProspetto. Utilizzo della libreria FPDF per la gestione dei pdf. Emersi diversi dubbi durante la realizzazione di queste classi: modificare le chiamate rispetto alle dipendenze inizialmente ipotizzate nel diagramma delle classi di analisi? Prime idee su InviaProspetti: mandare i prospetti in seguito alla loro realizzazione oppure poter permettere di generare più serie di prospetti e poi permettere di inviarli in seguito reintroducendo input? Dubbio risolto da casi d'uso in dettaglio.

23/02
- [ ] Ultimate classi GeneraProspetto e GestoreEmail. Non trovato alcun modo per riutilizzare i pdf già generati per i laureandi con le classi proposte dal committente. Realizzate InterfacciaGrafica, index.php e API. Enfasi su controllo matricole per verifica esistenza e correttezza del cdl. Modificate FIleConfigurazione e GestioneCarriera per utilizzo metodi statici. Prime verifiche di funzionamento in ambiente wordpress: corretti errori riguardanti require, json e path. Prime revisioni del codice.

24/02
- [ ] Ulteriori revisioni del codice con particolare attenzione nei confronti dei tipi dei campi, del tipo di ritorno dei metodi e della visibilità di questi in vista della generazione degli artefatti del workflow progetto. Risolto problema in apertura dei prospetti: riformattazione degli spazi nel link. Prove invio mail con casella di posta personale. Ulteriori prove per generazione dei prospetti: da verificare meglio correttezza, e gestione della cancellazione di questi.

26/02
- [ ] Realizzazione del diagramma delle classi di progetto a partire dal codice. Modificati alcuni operatori di visibilità nel codice grazie alla migliore visione d'insieme. Realizzazione del diagramma dei flussi di progetto a partire dal codice: grande uso dei blocchi ref per snellire i diagrammi. Accorpati alcuni metodi nel codice con scopi correlati, migliorata la gestione degli esami informatici che si attiva solo nel caso del cdl in ing inf.

- [ ] Realizzazione del diagramma di dislocazione. Riscontrate difficoltà per la specifica dei tipi di artefatto. Realizzazione della classe di testing: controllo anagrafica, bonus inf, presenza cdl, presenza esami nel prospetto, valori nel prospetto. Difficoltà in particolare per il controllo degli esami, è stato necessario un array di appoggio per i nomi degli esami. Realizzata interfaccia di testing e eseguito test: sistema perfettamente funzionante.

27/02
- [ ] Impaginazione dei workflow progetto e implementazione: generazione immagini vettoriali da Visual Paradigm e rimozione della filigrana. Stesura documento di collaudo del sistema. Mostrare caso di errore o esito positivo? Stesura dei manuali utente, amministratore e installazione. Riportata interfaccia utente indicando gli elementi presenti in essa. Revisione dell'intera documentazione per trovare eventuali refusi. Chiesta revisione a committente per il completamento del lavoro.
