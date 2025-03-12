#uni 
Questo è una famiglia di linguaggi dichiarativi basati sul calcolo dei predicati del primo ordine. Un altro modo per esprimere query oltre all'[[Algebra Relazionale]].
In questi linguaggi invece di descrivere il modo in cui arrivare al risultato, noi specifichiamo le __proprietà__ che deve avere il risultato, senza preoccuparci di come il [[Database]] ci arrivi.

Questa famiglia si divide in più gruppi ma noi affrontiamo solo:
- __TRC__: calcolo (relazionale) sui domini:
- __DRC__: calcolo (relazionale) sulle tuple con dichiarazioni di range
	- su questo si basa l'[[SQL]].

Noi useremo una notazione non posizionale.
Le espressioni hanno la seguente forma:
$$
\{ x : P(x) \}
$$
# Calcolo relazionale sui Domini
Le espressioni hanno la seguente forma: 
$$
\{A_1:x_1,...,A_k:x_k|f\}
$$

dove:
- $f$ è una formula a partire da formule atomiche, connettivi logici, booleani e quantificatori. Le formule atomiche possono essere di due tipi:
  1.  $R(A_1:x_1,...,A_P:x_p)$ dove $R(A_1,....,A_p)$ è uno _schema di relazione_ e $x_i$ sono variabili
  2. $x\theta y$ oppure $x\theta c$ con $x,y$ variabili, $c$ costante e $\theta$ operatore di confronto
- $A_i$ è un attributo
- $x_i$ è una variabile libera
- $A_1:x_1,...,A_n:x_n$ è chiamata ___target list___ e descrive il risultato
Il risultato è una relazione sugli attributi $A_1,...,A_k$ che contiene tuple di valori per le variabili libere $x_1,...,x_k$ che rendono vera la formula $f$ rispetto ad una istanza di base di dati a cui l'espressione è applicata.

