#uni 
Una **Giunzione PN** è l’unione tra due tipi diversi di materiale semiconduttore: uno di tipo P e uno di tipo N ([[Drogaggio]]). È uno dei componenti fondamentali dell’elettronica moderna (per esempio nei diodi, nei transistor e nei LED).

> Giunzione P/N: 
> ![[giunzionePN.svg]]

Quando uniamo questi due semiconduttori (che essendo di tipo diverso hanno diverse concentrazioni $P$ ed $N$), si mette in moto il fenomeno della diffusione ([[Corrente di Diffusione]]): le lacune, abbondanti in P, cercando di muoversi verso N, dove invece sono minoritarie, gli elettroni in N fanno il duale, c'è quindi una tendenza dei portatori di carica a ricombinarsi in prossimità della giunzione.

Si viene a creare quindi in prossimità della giuntura una **zona di svuotamento**, larga $W$, una zona priva di portatori di carica.

Questa tendenza genera un campo elettrico dentro il componente (diretto da N verso P), causato dal fatto che in P vi sono atomi accettatori non più bilanciati dalle lacune, e in N vi sono atomi donatori non più bilanciati da elettroni liberi, generando una differenza di carica tra il semiconduttore P e il semiconduttore N.

Questo campo elettrico comincia ad opporsi al movimento dei portatori di carica, creando una corrente di drift, raggiungendo una situazione di equilibrio in cui non vi è (a livello macroscopico) una corrente nel componente, anche perché questo porterebbe ad un **livello di Fermi** non uniforme, il che all'equilibrio è impossibile:
$$
\vec J_{tot} = \vec J_P + \vec J_N = \vec J_\text{P,diffusione} + \vec J_\text{P,drift} + \vec J_\text{N,diffusione} +\vec J_\text{N,drift} = 0
$$


Il potenziale che si genera nel componente prende il nome di **potenziale di built-in** (o Potenziale di contatto / Potenziale di barriera intrinseco) e vale:
$$
\text{Potenziale di Built-in:} \quad V_0 = \Delta \varphi=\frac{K_B \cdot T}{q}\ln(\frac{N_A \cdot N_D}{n_i^2})
$$
dove:
- $\varphi$ è il potenziale elettrico
Di solito $V_0$ vale attorno a $0.8\text V$.

È tuttavia impossibile misurarlo sperimentalmente con un semplice voltmetro poiché nel momento in cui colleghiamo i morsetti del nostro strumento ad Anodo e Catodo si creano due nuove zone di svuotamento con tanto di relativo potenziale di contatto, e lo strumento, rilevando la somma di questi potenziali di contatto e quello di built-in, misura $0$: 
$$
V_1 + V_2 + V_0 = 0
$$
# Applicazione di una tensione esterna

> Polarizzazione diretta:
> ![[giunzionePN_polarizzazione_diretta.svg]]

Se aggiungo un generatore di tensione esterno $V$ e lo collego in **polarizzazione diretta**, ovvero polo positivo di $V$ all'anodo e negativo al catodo, diminuisco la differenza di potenziale interna, che causa una diminuzione del campo elettrico autogenerato, che annullava la corrente di diffusione. 
Diminuendo il campo elettrico la corrente di diffusione prevale su quella di drift e cominciano a notare a livello macroscopico una corrente diretta nello stesso verso di quella di diffusione, ovvero da polo positivo a negativo, ovvero da $P$ a $N$.

Questo aumento di corrente è esponenziale:
- per attraversare la giunzione e creare una corrente di diffusione, le cariche devono avere un'energia maggiore di $E=q\cdot V_0​$.
- la statistica di Maxwell-Boltzmann ci dice che il numero di cariche in grado di superare una barriera di energia E è proporzionale a:
$$
e^{-\frac{E}{K_B\cdot T}}
$$
Quando invece applichiamo una tensione $V$, la barriera diventa $q\cdot (V_0-V)$, aumentando quindi esponenzialmente il numero di cariche in grado di creare corrente di diffusione.

In definitiva la corrente totale, diretta dall'anodo al catodo, aumenta esponenzialmente all'aumentare della tensione (in polarizzazione diretta) applicata.
## Polarizzazione Inversa
Se invece collego il polo positivo del generatore al catodo e quello negativo all'anodo, ovvero collego in **polarizzazione inversa**, la barriera di energia diventa $E=V_0+V$, diminuendo esponenzialmente il numero di cariche che sono in grado di creare corrente di diffusione.

Notiamo però che il campo elettrico, seppur più potente, genera comunque una corrente di drift flebile, poiché essendo indirizzato da $N$ a $P$, dalla zona $N$ cerca di muovere le lacune verso $P$ e dalla zona $P$ cerca di muovere gli elettroni verso $N$, però le lacune sono minoritarie nella zona $N$, e gli elettroni sono minoritari nella zona $P$ (per via della [[Legge di Azione di Massa]]), questo significa che si la corrente di drift aumenta, ma di un valore che nella pratica è considerato $0$, quindi a livello macroscopico vi è una quasi impercettibile corrente totale da $N$ verso $P$.

> La corrente di drift, indipendente dalla tensione applicata e generata solamente dai portatori di carica minoritari, creati in generazione termica, prende il nome di **Corrente di Saturazione Inversa** e si indica con $I_S$:
> $$
> I_S= I_\text{p,drift} + I_\text{n,drift}
> $$
# Legge di Shockley
La giunzione PN quindi funge da rubinetto ad una via sola, se vi applico una tensione in polarizzazione diretta aumenta esponenzialmente la corrente da $P$ a $N$, se invece applico una tensione in polarizzazione inversa ottengo una flebile corrente da $N$ a $P$, la corrente di saturazione inversa.

La corrente totale netta che attraversa la giunzione PN vale:
$$
\large
\text{Legge di Shockley:}\quad
I=I_S\cdot \left( e^{\frac{V}{\eta\cdot V_T}}-1 \right)
$$
dove:
- $V$ è la tensione applicata alla giuntura (positiva se in polarizzazione diretta)
- $I_S$ è la corrente di saturazione inversa (la corrente di drift): normalmente vale: $10^{-15}A< I_S <10^{-9}A$
- $\eta$ è il **Fattore di Idealità**, che varia tra 1 (ideale) e 2
- $V_T$ è la tensione termica: $V_T=\frac{K_B\cdot T}{q}$, a temperatura ambiente vale circa $26\text{mV}$ 
# Valore di W: la dimensione della zona di svuotamento

$$
W=\sqrt{\frac{2\epsilon}{q}\left(\frac{1}{N_A}+\frac{1}{N_D} \right)\left( V_0-V \right)}
$$
dove:
- $\epsilon$ è la permittività dielettrica del materiale

Quindi:
- più droghiamo il semiconduttore è più la zona di svuotamento diventa stretta
- se applico una polarizzazione diretta la zona di svuotamento diventa più stretta

>Poiché questa zona priva di cariche isola due zone conduttive, si comporta esattamente come il dielettrico di un condensatore.