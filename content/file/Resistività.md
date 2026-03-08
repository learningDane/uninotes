#uni 
La resistenza di un oggetto viene calcolata come: 
$$
R = \frac{L}{S}\rho
$$
con:
- $L$: lunghezza
- $S$: sezione
- $\rho$: **resistività**
$L$ ed $S$ sono parametri geometrici.

La **resistività** invece è un parametro che dipende dal materiale di cui è composto l'oggetto:
$$
\begin{matrix}
\text{Resistività:} \quad \rho \quad[\Omega\cdot m] 
\\
\text{Conducibilità:}\quad \sigma \quad[\Omega\cdot m]^{-1} \quad= \large \frac{1}{\rho}
\end{matrix}
$$
In base alla resistività (o conducibilità) possiamo distinguere i materiali in 3 categorie:
- **Conduttori** $10^{-2}< \rho$ 
- **Isolanti** $\rho > 10^{5}$ 
- **Semiconduttori**: $10^{-2}< \rho < 10^{5}$
	- ad esempio del [[Silicio]] può essere controllata la sua resistività attraverso il **drogaggio** ([[Silicio#Drogaggio]]).
# Conducibilità di un metallo
Utilizzando il [[Modello di Drude]] otteniamo che la conducibilità si calcola come:
$$
\sigma = n \cdot q \cdot \mu_n
$$
per un metallo abbiamo che:
- $n$ è circa $10^{21}\text{cm}^{-3}$ 
- $\mu_n$ è circa $500 \frac{\text{cm}^2}{V \cdot s}$ 
- $q$ è il modulo della carica dell'elettrone e vale $1,6\cdot 10^{-19}C$ 

Otteniamo quindi:
$$
\sigma\sim 8 \times 10^4(\Omega\cdot \text{cm})^{-1}\quad =\frac{1}{\rho}
$$
# Conducibilità di un Semiconduttore
Il [[Silicio]] però non compie un legame metallico ma covalente, gli elettroni non possono spostarsi a causa della forza di legame, questo allo zero assoluto, a temperature maggiori invece alcuni legami si rompono.

Indichiamo con $n_i$ la **concentrazione intrinseca** (dove intrinseco indica materiale *NON drogato*), il numero di elettroni che si liberano da legami e sono quindi abili a condurre e vale:
$$
n_i=B\cdot T^{3/2}\cdot e^{ \large \frac{-E_G}{2\cdot K_B \cdot T}}
$$
dove presenziano anche L'energia di legame, la costante di Bolzmann e $B$ dipende dal materiale.

Questa generazione di elettroni liberi prende il nome di **generazione termica**, che viene bilanciato in parte dal fenomeno di **ricombinazione termica**, fino ad un bilancio a regime pari a $n_i$.

La rottura di legame provoca le **lacune** (o vacanze), il campo elettrico provoca una catena di rottura e ricombinazione dei legami. 
Consideriamo le lacune con carica inversa a quella di un elettrone, con la stessa massa dell'elettrone ma una *mobilità* $\mu_p$ (vedi [[Modello di Drude]]) inferiore a $\mu_n$.

Per la conducibilità otteniamo quindi:
$$
\sigma = n_i \cdot\mu_n \cdot q+p\cdot \mu_p \cdot q
$$
con $n=n_i = n_p$, rispettando la [[Legge di Azione di Massa]].
# Legame tra Conducibilità e Temperatura
Abbiamo detto che la conducibilità si trova come:
$$
\sigma = nq\mu_n + pq\mu_p
$$
dove:
- $q$ con varia con la temperatura $T$ ovviamente
-  $\mu_n$ e $\mu_p$ invece: all'aumentare della temperatura aumentano le vibrazioni reticolari, causando più urti e di conseguenza diminuendo la mobilità proporzionalmente a $T^{\frac{3}{2}}$ ($T$ in Kelvin compresa tra $20$ e $600$ gradi)
- per $n$ e $p$ invece bisogna differenziare tra silicio intrinseco e drogato:
	- nel silicio intrinseco abbiamo $n=p=n_i$, che abbiamo detto ($n_i$) aumenta esponenzialmente con $T$. In definitiva *nel silicio intrinseco la conducibilità aumenta con la temperatura*
	- nel silicio drogato: prendiamo per esempio il drogaggio di tipo P: $p \approx N_A^-$ e $n\approx \frac{n_i^2}{N_A^-}$, quindi all'aumentare della temperatura _$p$ resta fisso_ e $n_i$ aumenta, ma avendo $N_A^- \approx p >>n$, _$n$ sale di poco_ ed in definitiva prevale la diminuzione della mobilità, diminuendo la conducibilità. Per il drogaggio tipo N vale il duale, $p$ sale poco e $n$ resta fisso, arrivando allo stesso effetto finale. Quindi *nel silicio drogato la conducibilità diminuisce con la temperatura* 

Il variare della conducibilità al variare della temperatura viene utilizzato nei sensori di temperatura integrati.