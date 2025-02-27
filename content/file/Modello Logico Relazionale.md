#uni 
Proposto da Edward Frank Codd nel 1970 per favorire l'indipendenza dei dati dall'implementazione (i modelli precedenti basati sui puntatori erano inutilizzabili se si cambiava la macchina).
Si basa sul concetto matematico di relazione, con una variante. Le relazioni hanno naturale rappresentazione per mezzo di __Tabelle__.

Tutti i dati sono rappresentati  come ___relazioni___ e manipolati con gli operatori dell'[[Algebra Relazionale]] o del calcolo relazionale.

Una __relazione matematica__ è un sottoinsieme qualsiasi di un insieme prodotto da una qualche operazione tra uno o più insiemi detti ___Domini___. 
- Non c'è ordinamento tra le __tuple__ 
- non esistono tuple uguali
- ogni tupla è ordinata al suo interno

La struttura della tabella può essere posizionale, quindi l'ordine dei domini nella tabella dipende dall'ordine degli stessi nella relazione, oppure non posizionale, in cui a ciascun dominio di associa un nome unico nella tabella, che ne descrive il ruolo.
I riferimenti fra dati in relazioni diverse sono rappresentati per mezzo di ___valori___ dei domini che compaiono nelle tuple. 
# Definizioni
- __Relazione__:
	  dati $n>0$ insiemi $D_{1},D_{2},\dots,D_{n}$ non necessariamente distinti, il prodotto cartesiano $D_{1} \times D_{2} \times \dots \times D_{n}$ è costituito dall'insieme delle tuple $(v_{1},v_{2},\dots,v_{n})$ tali che $v_{i}$ appartiene a $D_{i}$, per $1 \leq i \leq n$.
	  Una ___Relazione Matematica___ sui domini $D_{1},D_{2},\dots,D_{n}$ è un sottoinsieme del prodotto cartesiano di cui sopra.
	  - il numero $n$ di elementi del prodotto cartesiano viene chiamato __grado__.
	  - il numero di elementi (cioè tuple) della relazione viene chiamato __cardinalità__ della relazione.
- __Attributo__: nome che assegnano agli insiemi $D_{1},D_{2},\dots$ in modo da non dover fare affidamento sulla notazione posizionale. In breve gli attributi sono i "nomi delle colonne".
	- nuova definizione di relazione: dato un insieme $X$ di attributi:
	  ___Una relazione su $X$ è un insieme di tuple su $X$.
- ___Schema di Relazione___: $R(X)$ con $R$ nome della relazione e $X$ insieme di attributi
- ___Schema di Base di Dati___: $R={R_1(X_1),...,R_m(X_m)}$ quindi un insieme di schemi di relazione
- Una tupla su un insieme di attributi $X$ è una funzione che associa a ciascun attributo $A \in X$ un valore nel dominio di $A$, il simbolo $t[A]$ denota il valore della tupla $t$ sull'attributo $A$ 
- ___Istanza di Relazione___ su uno schema $R(X)$: insieme $r$ di tuple su $X$ 
- ___Istanza di base di dati___ su uno schema $R$: insieme di relazioni $r={r_1,...,r_m}$ dove ogni $r_i$ è una relazione sullo schema $R_i(X_i)$ 
# Valore Nullo
Il modello relazionale impone ai dati una struttura rigida, se una informazione manca non conviene usare valori particolari, viene utilizzato il valore ___NULL___. Si devono però imporre restrizioni sulla presenza di valori nulli in una relazione.
__NULL__ può volere dire per esempio:
- valore sconosciuto
- valore inesistente
- valore senza informazione

__I DBMS non distinguono i tipi di valore nullo!__ Questa differenza esiste sono nella testa del programmatore.
# Chiave e Superchiave
Un insieme $K$ di attributi è una __superchiave__ per una relazione $r$ se $r$ non contiene due tuple distinte $t_1$ e $t_2$ con $t_1[K]=t_2[K]$.

K è una __chiave__ per $r$ se è una superchiave minimale di $r$  (ovvero non contiene un'altra superchiave).

Una relazione è un insieme e per definizione quindi non può avere due elementi (le tuple) uguali, quindi ogni relazione ha almeno una chiave, la superchiave rappresentata dall'insieme degli attributi su cui è definita.
### Valori NULL e chiavi
I valori NULL nelle chiavi non permettono di identificare le tuple, per ovviare a questo problema vietiamo valori NULL su una delle chiavi, questa prenderà il nome di __Chiave Primaria__.
Gli attributi che costituiscono la chiave primaria sono normalmente evidenziati, in genere tramite una sottolineatura.

| _matricola_ | cognome | nome  |
| ----------- | ------- | ----- |
| 65473       | Pippi   | Pippo |
| 78645       | Lippi   | Lippo |
in questo esempio matricola è chiave primaria, visibile attraverso l'italico.
### Chiavi esterne
Data una relazione $R$, un insieme di attributi è __chiave esterna__ se compare come chiave in un'altra relazione.
Una chiave esterna garantisce il soddisfacimento del [[#Vincolo di Integrità Referenziale]], e garantisce che ad ogni tupla di $R$ sia associata una tupla nell'altra relazione.
# Vincoli di Integrità
Un vincolo di integrità è una funzione booleana associata ad una base di dati e chiamata su ogni istanza di essa, che se soddisfatta esprime la correttezza del [[Database]] rispetto all'applicazione.
Questi permettono una descrizione più accurata della realtà, sono utili nella progettazione e sono usati nei [[DBMS]] nella esecuzione delle interrogazioni.
I vincoli corrispondono a proprietà reali e interessano tutte le istanze e se sono tutti soddisfatti garantiscono la correttezza dello schema.
Esistono due tipi di vincoli di integrità:
- [[#Vincoli intrarelazionali]] 
- [[#Vincoli interrelazionali]] 
### Vincoli intrarelazionali
Il suo soddisfacimento è definito rispetto ad una singola relazione della base di dati.
- ___Vincolo di Tupla___: soddisfacimento valutato osservando __le singole tuple__ una per volta.
- ___Vincolo di dominio___ (o sui valori): soddisfacimento valutato osservando __1 singolo attributo__, una tupla per volta (ad esempio: valori compresi tra $18$ e $30$).
- ___Vincoli di chiave___:
	Le chiavi definite su schemi di relazione sono particolari vincoli di integrità, detti vincoli di chiave.
	- La chiave primaria __deve essere unica e non nulla__.

I vincoli di chiave sono i più importanti vincoli del modello relazionale e sono particolari vincoli che fanno parte della categoria [[Dipendenza Funzionale]].
### Vincoli interrelazionali
Il suo soddisfacimento è definito rispetto a più relazioni della base di dati.

---
##### Vincolo di Integrità Referenziale
Un vincolo di integrità referenziale fra gli attributi $X$ di una relazione $R_1$ e una relazione $R_2$ impone ai valori su $X$ in $R_1$ DIVERSI da NULL di comparire come valori della chiave primaria di $R_2$.
Nota che in questo caso l'ordine degli attributi tra cui è stabilito il vincolo è significativo.
### Reazione alla violazione di vincoli
Quando si tenta di compiere un'operazione che viola un vincolo entrano in gioco diversi meccanismi, che prendono il nome di ___azioni compensative___.