#uni 
Anche detto modello __E-R__, è il [[Modello dei dati]] concettuale più diffuso.
Uno schema __E-R__ sebbene necessario non è quasi mai sufficiente ad esprimere tutti i dettagli di una applicazione, ci sono dei vincoli non esprimibili e per questo si rende necessario associarci una documentazione di supporto. Quando si costruisce uno schema E-R va tenuto conto della normalizzazione su entity e relationship.

Uno schema (concettuale) E-R non è quasi mai sufficiente da solo a rappresentare tutti i dettagli di un'applicazione, ci sono vincoli indescrivibili ed è quindi necessario associare una documentazione di supporto.
# Costrutti del Modello E-R
## Costrutti Principali
### Entity
Una entità è una classe di oggetti (fatti, persone, cose) con proprietà comuni ed esistenza _autonoma_.
Non cambia da una istanza all'altra: un "impiegato" rimane sempre un "impiegato" senza altre proprietà note oltre a quelle che lo definiscono "impiegato".
Ogni entità ha un nome che la identifica univocamente nello schema, il nome deve essere espressivo e si deve fare riferimento a opportune convenzioni, eg. usare sempre il singolare.

- Le entità vengono rappresentate tramite rettangoli con il proprio identificatore al centro.
### Relationship
Questa è un legame logico fra due o più entity, può venire chiamata relazione, correlazione oppure associazione.

Ogni relationship ha un nome, espressivo, singolare e possibilmente deve essere un sostantivo, non un verbo (per evitare di dare un verso alla relationship).

Alcuni esempi: Residenza (fra persona e città), esame (fra studente e corso).

Una occorrenza di relationship _binaria_ è una coppia di occorrenze di entità, una per ognuna delle due entità coinvolte. 
Una occorrenza di relationship _n-aria_ è una tupla di occorrenze di entità, una per ogni $n$ entità coinvolte.
Quando una stessa relationship è connessa tramite due frecce ad una stessa entity, si dice ___ricorsiva___, o ___mista___ se inoltre è anche connessa ad altre relationship. Ogni freccia può specificare un diverso ruolo.

Nell'ambito di una relationship non ci possono essere occorrenze ripetute.

- vengono rappresentate tramite rombi con al centro il proprio nome, collegati alle proprie entity.

> Relationship Mista con Ruoli:
![[relationshipmistaconruoli.svg]]
### Attributo
Un attributo è una proprietà elementare di una entity o di una relationship: associa ad ogni occorrenza di entity o relationship un valore, appartenente al dominio dell'attributo.
Un attributo __composto__ raggruppa attributi che presentano affinità di una medesima entity o  relationship, ad esempio _via, numero, civico_ e _cap_ formano _indirizzo_.

- gli attributi composti vengono rappresentati come ellissi con al centro il proprio nome, e poi gli attributi che li formano

> Rappresentazione Grafica degli Attributi e degli attributi Composti:
> ![[rappresentazioneattributi.svg]]
## Altri Costrutti
### Cardinalità
Può essere di relationship o di attributo.
##### Cardinalità di Relationship
Questa è una coppia di coppie valori, ognuna associata alla relativa entity coinvolta.
Specifica il numero minimo e massimo di occorrenze della relationship cui ciascuna occorrenza di entità può partecipare.

Per semplicità utilizziamo solo 3 simboli:
- $0$ e $1$ per la cardinalità minima:
  - $0=$ partecipazione opzionale
  - $1=$ partecipazione obbligatoria
- $1$ e $N$ per la cardinalità massima ($N$ non pone alcun limite)

Possiamo con la cardinalità massima distinguere 3 tipi di relationship:
- ___uno a uno___: $(k,k) - (k,k)$ 
- ___uno a molti___: $(k,k) - (k,N)$ 
- ___molti a molti___: $(k,N) - (k,N)$ 
_eg:_ $Impiegato \ (1,1) \ Residenza \ (0,N) \ Città$ 

> Rappresentazione delle cardinalità di Relationship:
> ![[rappresentazioneCardinalità.svg]]
### Identificatore di _entity_ 
Questo è uno strumento per identificare univocamente delle occorrenze di una _entity_ (come la chiave nel [[Modello Logico Relazionale]]). 
Ogni entity deve possedere almeno un identificatore ma può averne di più.

Un identificatore può essere costituito da:
- attributi dell'entity: ___identificatore interno___.
- attributi + identificatore interno di entità esterne, raggiunte attraverso relationship: ___identificatore esterno___, (possibile solo attraverso una relationship $(1,1)$. 
> Rappresentazione degli identificatori:
> ![[rappresentazioneidentificatori.svg]]
### Generalizzazione
Mette in relazione una o più entity $E_1,E_2,...$ con una entity $E$ che le comprende come casi particolari, si dice che $E$ è una ___generalizzazione___ (o genitore) di $E_1,E_2,...$, che invece si dicono ___specializzazioni___ (o sottotipi o figlie) di $E$.

- ___ereditarietà___: Ogni proprietà di $E$ è significativa per le figlie e non viene rappresentata esplicitamente.

Ogni occorrenza delle figlie è occorrenza anche di $E$.

Si dice Generalizzazione __Totale__ se ogni occorrenza del Genitore è occorrenza di almeno una delle figlie, altrimenti di dice __Parziale__.
Si dice __Esclusiva__ se ogni occorrenza del genitore è occorrenza di al più una figlia, altrimenti di dice __Sovrapposta__.

Se una generalizzazione ha solo un'entità figlia si parla di __Sottoinsieme__.
Il genitore di una generalizzazione totale può non avere identificatore, purché lo abbiano le entità figlie.

Possono esistere gerarchie a più livelli e multiple generalizzazioni allo stesso livello; un'entità può essere inclusa in più gerarchie, sia come genitore che come figlia.

>Rappresentazione di generalizzazione:
>![[rappresentazioneGeneralizzazioni.svg]]
# Esempi
#### Dizionario dei dati (entity):

| entity    | descrizione             | attributi                 | identificatore |
| --------- | ----------------------- | ------------------------- | -------------- |
| impiegato | dipendente dell'azienda | codice<br>cognome<br>nome | codice         |
| ecc       |                         |                           |                |
#### Dizionario dei dati (relationship)

| relazioni | descrizione                  | componenti                | attributi |
| --------- | ---------------------------- | ------------------------- | --------- |
| afferenza | afferenza ad un appartamento | impiegato<br>dipartimento | data      |
#### Regole di Vincolo
1. Il direttore di un dipartimento deve afferire a tale dipartimento
2. un impiegato non deve avere uno stipendio maggiore del direttore del dipartimento al quale afferisce
3. _ecc.._ 
#### Regole di Derivazione
1. il numero di impiegati di un dipartimento si ottiene contando gli impiegati che afferiscono a tale dipartimento
2. _ecc..._ 