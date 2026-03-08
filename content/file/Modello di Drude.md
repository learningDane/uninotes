#uni 
Il **modello di Drude** è un modello classico che descrive il comportamento elettrico e termico dei metalli trattando gli elettroni di conduzione come un gas di particelle libere che si muovono all’interno del reticolo ionico.

È uno dei primi tentativi teorici di spiegare:
- la conduzione elettrica
- la conduzione termica
- la legge di Ohm su base microscopica

Sebbene fondandosi su alcune assunzioni errate, ha portato ad una formula per il calcolo della conducibilità quasi corretta.
# Ipotesi fondamentali
Il modello si basa sulle seguenti assunzioni:
- gli elettroni sono particelle classiche
- gli ioni del reticolo sono fissi
- gli elettroni subiscono urti casuali con:
  - ioni
  - impurità
  - difetti del reticolo
- tra due urti consecutivi, l’elettrone si muove di moto rettilineo uniforme
- il tempo medio tra due urti è costante (tempo di rilassamento τ)
# Moto degli elettroni senza campo elettrico
In assenza di campo elettrico a temperatura maggiore dello zero assoluto:
- il moto degli elettroni è caotico, è puro moto Browniano
- la velocità media è zero
- non c’è corrente macroscopica, ovvero non vi è **Corrente di Deriva**
# Moto degli elettroni con campo elettrico
Applicando un campo elettrico $E$ ogni elettrone subisce una forza $F = -qE$, con $q$ = modulo della carica (dell'elettrone), quindi accelera tra un urto e l’altro e si instaura una velocità media detta velocità di deriva $v_d$.
$$
\vec {\overline v} = v_{\text{drift}}= -\mu_n \cdot \vec E
$$

con $\mu_n$ **mobilità degli elettroni**, misurata in $\left[\frac{m^2}{V \cdot s}\right]$. 

> Nota che questo vale solo con valori di $\vec E$ contenuti, in caso contrario $v_\text{deriva}$ satura ad un certo valore.

$$
\begin{matrix}
N: \text{numero totale di elettroni}
\\
\Delta T: \text{tempo di osservazione:} \quad \Delta T=\large \frac{L}{v_d} 
\\
I=\large\frac{\Delta Q}{\Delta T}=\frac{N\cdot q}{\Delta T}=\frac{N\cdot v_d}{L}\cdot q
\\
\text{Densità di Corrente:} \quad J=\frac{N}{Vol}\cdot q \cdot v_d=n\cdot q \cdot \mu_n \cdot E
\end{matrix}
$$

Utilizziamo la **legge microscopica di Ohm**:
$$
J=\sigma \cdot E
$$
e otteniamo:
$$
\begin{matrix}
\vec J = \sigma \cdot \vec E
\\
\text{conducibilità:}\quad \sigma = n \cdot q \cdot \mu_n
\end{matrix}
$$

