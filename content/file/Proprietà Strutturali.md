#uni 
Le 3 proprietà strutturali di un sistema sono: la stabilità, la raggiungibilità e l'osservabilità, e sono determinate dalle matrici di struttura del sistema.
# Stabilità
Questa proprietà dipende unicamente dal movimento libero del sistema [^3], che possiamo comunque evitare di calcolare ([[Stabilità secondo Lyapunov]]).
Dipende solamente dalla matrice $A$.

Il movimento $\tilde{x}$ è stabile se $\forall \epsilon>0, \exists \delta >0 : \forall \delta_{x_0} \text{ per cui } ||\delta_{x_0}|| \leq 0 \text{ risulti } ||\delta_x(t)|| \leq \epsilon, t \geq 0$ 

$\tilde{x}$ è asintoticamente stabile se inoltre $\lim_{t\to \infty} || \delta_x(t)||=0$ 

___Teorema___: un movimento (o uno stato di equilibrio) di un sistema lineare stazionario è stabile, asintoticamente stabile o instabile se e solo se tutti i movimenti (o gli stati di equilibrio) del sistema sono rispettivamente stabili, asintoticamente stabili o instabili.

___Teorema___: Un sistema lineare stazionario:
- è stabile se e solo se tutti i movimenti liberi dello stato sono limitati;
- è asintoticamente stabile se e solo se tutti i movimenti liberi dello stato tendono a zero per $t \to \infty$;
- è instabile se e solo se almeno un movimento libero dello stato non è limitato.
### Stabilità e Autovalori
___Teorema___: un sistema LTI è asintoticamente stabile se e solo se tutti i suoi autovalori hanno parte reale negativa.

___Teorema___: un sistema LTI è instabile se almeno uno dei suoi autovalori ha parte reale positiva.

I punti nel Piano di Gauss con coordinata Reale minore di zero prendono il nome di ==regione asintoticamente stabile==. 

Se $Re(\lambda) \leq 0 \forall \lambda$ (la parte reale di almeno un autovalore è nulla) allora il sistema sicuramente non è asintoticamente stabile, può comunque essere stabile o instabile.
È instabile se e solo se tra i $\lambda_i \text{ con } Re(\lambda_i)=0$, ne esiste almeno uno cui corrisponda un miniblocco di Jordan di dimensione maggiore di uno, poiché in questo caso nel movimento libero comparrebbe un modo del tipo $t^k$ eventualmente moltiplicato per un seno, con $k>0$, che tende a più infinito per $t \to \infty$.

Se non vi sono autovalori multipli sull'asse immaginario (un solo $Re(\lambda)=0$) allora il sistema risulta stabile se e solo tutti i suoi autovalori hanno parte reale negativa o nulla.
### Tabella Riepilogativa

| stabilità  | Modi          | Autovalori                                                                                                                          |
| ---------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Asintotica | tendono a $0$ | $Re(\lambda) <0$                                                                                                                    |
| Marginale  | limitati      | $Re(\lambda) \leq 0$ e per i $\lambda$ per cui $Re(\lambda)=0$, $q$ (dimensione del blocco di jordan relativo) $=1$, ovvero $mg=ma$ |
# Raggiungibilità
Questa proprietà riguarda la possibilità di far assumere allo stato di un sistema dinamico un valore prefissato, agendo sull'ingresso, ed è legata alle matrici $A,B$.

___Definizione___: uno stato $\tilde{x}$ di un [[Sistema LTI]] si dice ___raggiungibile___ se $\exists \tilde{t}>0$ e $\tilde{u}$ (ingresso forzato), definito tra $0$ e $\tilde{t}$, tali che, detto $\tilde{x_f(t)}, 0 \leq t \leq \tilde{t}$ il movimento forzato dello stato generato da $\tilde{u}$ risulti $\tilde{x}_f(\tilde{t)}=\tilde{x}$.

Un sistema con tutti gli stati raggiungibili si dice ___completamente raggiungibile___.
Questa è una proprietà che dipende dalla risposta forzata.

>Nei sistemi LTI la raggiungibilità coincide con la controllabilità.

In base a questa proprietà possiamo dividere gli stati in:
- raggiungibili: $x_R$
- non raggiungibili: $x_{NR}$ 

___Teorema___: per verificare se un sistema è completamente raggiungibile calcoliamo la ___matrice di raggiungiblità___ $M_R=[B \quad AB \quad A^2B \quad ... \quad A^{n-1}B]$ con $n$ ordine del sistema, condizione necessaria e sufficiente per la raggiungibilità è che $rank(M_R)=n$, ovvero la matrice di raggiungibilità abbia rango massimo. 
### Scomposizione
Se il sistema non è completamente raggiungibile scompongo e isolo la parte non raggiungibile:
1. costruisco la matrice di trasformazione $T_R$:
	1. scegliamo $n_r$ colonne linearmente indipendenti in $M_R$(ogni stato raggiungibile è combinazione lineare di queste colonne).
	2. ci aggiungo poi $n-n_r$ colonne linearmente indipendenti dalle precedenti.
2. Trasformo[^2] ora il sistema tramite la matrice $T_R$: $\hat{A}=T_R^{-1} \cdot A \cdot T_R, \quad \hat{B}=T_R^{-1} \cdot B, \quad \hat{C}=C \cdot T_R$ 
3. Ottengo una $\hat{A}$ che è sempre della forma: $\hat{A}=\begin{bmatrix}\hat{A}_a & \hat{A}_{ab}  \\ 0 &  \hat{ A}_b\end{bmatrix}$ dove:
	- $\hat{A}_a$ è sempre raggiungibile
	- $\hat{A}_b$ è sempre non raggiungibile
	- $\hat{A}_{ab}$ rappresenta l'influenza degli stati non raggiungibili su quelli raggiungibili.

Se la parte non raggiungibile è asintoticamente stabile, si dice che il sistema è ___stabilizzabile___.

Per un sistema completamente controllabile esiste sempre almeno un ingresso che permette di andare da un certo stato ad un altro, per ogni coppia di stati.
# Osservabilità
Questa proprietà indica la possibilità di determinare il valore dello stato interno iniziale a partire dalla conoscenza della sua uscita, ed è legata alle matrici $A,C$.

___Definizione___: uno stato $\tilde{x}\neq 0$ di un [[Sistema LTI]] si dice ___non osservabile___ se, qualunque sia $\tilde{t}>0$ finito, detto $\tilde{y}_l(t),t \geq 0$, il movimento libero generato da $\tilde{x}$, risulta $\tilde{y}_l(t)=0,0\leq t \leq \tilde{t}$.
Un sistema privo di stati non osservabili si dice ___completamente osservabile___.

L'osservabilità è legata alla risposta libera e all'equazione di uscita.

___Teorema___: condizione necessaria e sufficiente è che la ___matrice di osservabilità___ abbia rango massimo:
$$
rank\left(\begin{bmatrix}
C\\ CA\\ .\\.\\CA^{n-1}
\end{bmatrix}\right)=n
$$

Anche questa proprietà divide gli stati in due insiemi:
- stati osservabili: $x_O$
- stati non osservabili: $x_{NO}$
### Scomposizione
Posso isolare la parte non osservabile:
1. costruisco la matrice $T_O$:
	1. seleziono $n-n_o$ vettori $\xi_i$ linearmente indipendenti, tali che $M_O \xi_i=0 \text{ ovvero } span({\xi_i})=x_{NO}$, quindi compongo una base del kernel di $M_O$. Sono non osservabili tutti e solo i vettori ottenibili come combinazione lineare dei vettori $\xi_i$.
	2. seleziono $n_o$ vettori linearmente indipendenti per completare la matrice, tali che: $det(T_o^{-1}) \neq 0$ e quindi la matrice risulti invertibile.
2. eseguo un cambio di variabile[^2] attraverso la matrice di trasformazione $T_O$: $\hat{A}=T_O^{-1} \cdot A \cdot T_O, \quad \hat{B}=T_O^{-1} \cdot B, \quad \hat{C}=C \cdot T_O$ 
3. ottengo una matrice $\hat{A}$ sempre della forma: $\hat{A}=\begin{bmatrix}\hat{A}_a & 0 \\ \hat{A}_{ab} & \hat{A}_b\end{bmatrix}$ e $\hat{C}=\begin{bmatrix}\hat{C}_a  & 0\end{bmatrix}$ con $\hat{A}_a$ parte osservabile e $\hat{A}_b$ parte non osservabile.
   Ed infine vale: $aut(\hat{A})=aut(A)=aut(\hat{A}_a)+aut(\hat{A}_b)$ 

[^2]: [[Sistema LTI#Trasformazioni Equivalenti]]
# Forma Canonica
È possibile dimostrare che si può portare ogni sistema in una forma che evidenzia le parti osservabili e raggiungibili, che prende il nome di ___forma canonica___.
La matrice di trasformazione $T_K$ utilizzata in questo procedimento prende il nome dall'ingegnere Ungherese [[Kalman]].
Si ottiene:
$$
\begin{matrix}
\hat{x}=\begin{bmatrix}
\hat{x}_a\\\hat{x}_b\\ \hat{x}_c\\\hat{x}_d
\end{bmatrix}
& \hat{A}=\begin{bmatrix}
\hat{A}_a & \hat{A}_{ab}  & \hat{A}_{ac} & \hat{ A}_{ad} \\ 0  & \hat{ A}_b &  0  &  \hat{ A}_{bd} \\ 0  & 0 & \hat{A}_c & \hat{A}_{cd}\\0 & 0 & 0 & \hat{A}_d
\end{bmatrix}
 & \hat{B}=\begin{bmatrix}
\hat{B}_a\\ \hat{B}_b\\0\\0
\end{bmatrix} & \hat{C}=\begin{bmatrix}
0 & \hat{C}_b & 0 & \hat{C}_d
\end{bmatrix}
\end{matrix}
$$
dove gli elementi non nulli di $\hat{B}$ sono le parti raggiungibili, quelli non nulli di $\hat{C}$ sono le parti osservabili.
Troviamo quindi:
- $\hat{x}_a$: raggiungibile e non osservabile
- $\hat{x}_b$: raggiungibile e osservabile
- $\hat{x}_c$: non raggiungibile e non osservabile
- $\hat{x}_d$: non raggiungibile e osservabile

![[formacanonica1.svg]]
# Forma Minima
Un sistema completamente osservabile e raggiungibile è detto in ___forma minima___.

Questo in quanto non è possibile usare un numero di variabili di stato minore del suo ordine per descrivere la relazione ingresso-uscita.

Le parti non raggiungibili e/o non osservabili sono inutili ai fini dello studio del movimento forzato.
# Ispezione diretta
Affrontiamo ora due metodi per velocizzare lo studio della raggiungibilità osservabilità di un sistema.
### Ispezione diretta per la raggiungibilità
___Lemma PBH___ (Popov, Belevitch, Hautus): un [[Sistema LTI]] è completamente raggiungibile se e solo se:
$$
rank[(\lambda \cdot Id-A)\ |\ B]=n, \quad\forall\lambda\in C
$$

Potrebbe sembrare necessario analizzare questa condizione per ogni valore complesso, ma se $\lambda$ non è una autovalore di $A$ allora la condizione è sempre verificata, poiché $det(\lambda \cdot Id -A) \neq 0 \implies rank(\lambda \cdot Id -A)=n$, per la definizione di autovalore ($det(\lambda \cdot Id -A)=0$).
Devo quindi solo verificare il lemma per ogni autovalore di $A$.

La dimostrazione è sugli appunti del giorno 12/03/2025 e viene fatto per assurdo

Un sistema con $\mu$ miniblocchi associati a $\lambda_i$ può essere raggiungibile solo se ha almeno $\mu$ ingressi (per arrivare ad ottenere $n$ colonne linearmente indipendenti).
### Ispezione diretta per l'osservabilità
___Lemma PBH___: un sistema LTI è completamente osservabile se e solo se:
$$
rank \begin{bmatrix}
\lambda \cdot Id-A \\C
\end{bmatrix}=n, \quad \forall \lambda\in C
$$

Anche in questo caso basta analizzare i soli autovalori di $A$.

Tutte le colonne $C_{i,1}$ dei corrispondenti blocchi di Jordan devono essere linearmente indipendenti.

[^3]: [[Sistema LTI#Formula di Lagrange]]
