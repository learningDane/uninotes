 #uni 
# And
>[!Theorem] Probabilità Condizionata
>$$
>P(A|B)=\frac{P(A\cap B)}{P(B)}
>$$

>[!Theorem] Teorema di Bayes
>$$
>P(B|A)=\frac{P(A|B)P(B)}{P(A)}
>$$

>[!Theorem] Distribuzione Normale
>$$
>\large
>f_{\cal N}\left(x\right)=\frac{1}{\sqrt{2\pi \sigma ^2}}e^{\frac{-(x-\eta)^2}{2\sigma ^2}}
>$$
# Sang
>[!theorem] Trasformata Continua di Fourier (TCF)
>$$
>\large
>\begin{matrix}
>\text{Equazione di Analisi:} & X(f)=\int x(t)e^{-j2\pi f t}dt
>\\
>\text{Equazione di Sintesi:} & x(t)=\int X(f)e^{-j2\pi f t}df
>\\
>\text{Univocità:} & x(t) \iff X(f)
>\end{matrix}
>$$

>[!theorem] Teorema di Parseval
>$$
>\large
>E_x=\int |x(t)|^2dt=\int |X(f)|^2df
>$$
>densità spettrale di energia: $\large \cal E_x(f)=| \mathnormal X(f)|^2$

> [!Theorem] Densità Spettrale di Energia
> $$
> \large
> \large \cal E_x(f)=| \mathnormal X(f)|^2
> $$

> [!Theorem] Densità Spettrale di Potenza
> Per i segnali a potenza media finita si ha:
> $$
> \large
> P_x=\int \cal P _x (f)df
> \atop
> \large
> \cal {P}_ x (f)=\lim_{ \mathnormal T \to \infty} \frac{| \mathnormal X(f)|^\mathnormal 2}{\mathnormal T}
> $$

> [!Theorem] Relazione tempo-banda
> - Un segnale di breve durata nel tempo ha uno spettro largo in frequenza.
> - Un segnale con spettro stretto in frequenza ha una lunga durata nel tempo.
> 
> Legame durata nel tempo - durate in frequenza:
> $$
> \Delta_t\Delta_f\approx \text{costante}
> $$

>[!Theorem] Teoremi della trasformata di Fourier
>Linearità:
>$$
>x(t)=ax_1(t)+bx_2(t)\iff  X(f)=aX_1(f)+bX_2(f)
>$$
>Dualità:
>$$
>x(t)\iff X(f) \quad \leftrightarrow \quad X(t) \iff x(-f)
>$$
>Teorema del Ritardo:
>$$
>\begin{matrix}
>y(t)=x(t-t_0) \iff Y(f)=X(f)e^{-j2 \pi f t_0}
>\\
>\to |Y(f)|=|X(f)|
>\\
>\to \angle Y(f)=\angle X(f)-2\pi f t_0
>\end{matrix}
>$$
>Un ritardo Temporale modifica lo spettro di fase introducendo un fase che cresce linearmente con la frequenza ma non cambia lo spettro di ampiezza.

> [!Theorem] Teorema della Modulazione
> $$
> x(t)\cos (2\pi f_o t) \iff \frac{X(f-f_0)+ X(f+f_0)}{2}
> $$
> Lo spettro viene traslato di $f_0$ e dimezzato in ampiezza.
> Ovvero lo spettro viene sdoppiato in due copie grandi la metà centrate una in $+f_0$ e una in $-f_0$.
> 
> Per la demodulazione:
> 1. Moltiplico il segnale nel tempo per $\cos(2 \pi f_0 t)$
> 2. Ottengo lo spettro originale al centro e due copie grandi un quarto centrate in $\pm 2f_0$ 
> 3. applico un filtro passa basso per filtrare le due copie non desiderate

> [!Theorem] Teorema del prodotto e della Convoluzione
> $$
> \begin{matrix}
> z(t)=x(t) \cdot y(t) \quad \leftrightarrow \quad Z(f)=\int_{v=-\infty}^\infty X(v)Y(f-v)dv = X(f) \otimes Y(f)
> \\ \\
> X(f)\cdot Y(f) \iff x(t) \otimes y(t)
> \\ \\
> Z(f)=X(f)\cdot Y(f)
> \end{matrix}
> $$
> _Il supporto dell'integrale di convoluzione tra 2 funzioni con estensione limitata è data dalla somma delle due estensioni_.

> [!Theorem] Calcolo della Banda a `-3` dB
> $$
> 10\log _{10} \left(\frac{|X(B_{-3\text{dB}})|^2}{|X(f_0)|^2}\right)=-3 \text{dB}
> $$
> La Banda a `-3` dB è l'ampiezza dell'intervallo frequenziale in cui il modulo della trasformata del segnale non scende di oltre 3 dB rispetto al valore di riferimento in $f_0$ (normalmente $f_0=0\text{Hz}$).
> Ovvero è l'ampiezza dell'intervallo frequenziale in cui il segnale in modulo non scende sotto metà del modulo nella frequenza portante.
> 
> Convenzione: la banda di un segnale modulato è doppia di quella del segnale non modulato.

> [!Theorem] Calcolo della Banda al 99% dell'Energia
> $$
> \large
> \int _ {-B_{99}}^{B_{99}} |X(f)|^2df=0.99 E_x=0.99 \int|X(f)|^2df
> $$

> [!Theorem] Rapporto tra durata del segnale e Banda
> Un segnale a durata finita non può avere una banda finita.
> Se moltiplichiamo il segnale per una `rect` (simuliamo la finitezza nel tempo), vorrebbe dire convolure il segnale per una `sinc`, che ha supporto infinito, quindi il risultato ha banda illimitata.

>[!Theorem] TCF di segnali ad energia infinita
>Per i segnali ad energia infinita (per esempio quelli periodici), non esiste la TCF.

>[!Theorem] Nota
>Il valore della trasformata di un segnale nella sua frequenza portante è uguale all'integrale nel tempo del segnale:
>$$
>X(0)=\int_{-\infty}^{\infty} x(t) dt
>$$ 

>[!Theorem] Funzione Delta di Dirac $\delta(t)$
>$$
>\delta(t)=\frac{du(t)}{dt}
>\atop
>u(t)=\int \delta(t)dt
>$$
>La funzione delta di Dirac è invariante al prodotto di convoluzione.
>La funzione delta di Dirac è Pari.

>[!Theorem] Proprietà Campionatrice
>$$
>\int \delta(t-t_0) x(t)=x(t_0)
>$$

>[!Theorem] Sistemi Lineari Stazionari (SLS)
>$$
>y(t)=x(t) \otimes h(t) \quad =\int x(\beta)h(t-\beta)d\beta
>$$
>Dove $h(t)$ è la risposta impulsiva del sistema:
>$$
>h(t)=\cal T[\delta(\alpha),t)]
>$$
>ovvero l'uscita del sistema quando si applica in ingresso una delta di Dirac.

>[!Theorem] Risposta in frequenza di un SLS
>Applichiamo il teorema della convoluzione:
>$$
>y(t)=x(t) \otimes h(t) \quad \iff \quad Y(f)=X(f)H(f)
>$$
>La TCF della risposta impulsiva si chiama **Risposta in frequenza** del sistema.

>[!Theorem] Teorema di Integrazione
>Integrare nel tempo corrisponde a dividere per $2j \pi f$ nel dominio della frequenza:
>$$
>\int_{-\infty}^tx(\tau)d\tau \quad \iff \quad\frac{X(f)}{2j \pi f}
>$$

>[!Theorem] Teorema di Derivazione
>Derivare nel tempo corrisponde a moltiplicare per $2j \pi f$ nel dominio della frequenza:
>$$
>\frac{dx(t)}{dt} \quad \iff \quad 2j \pi f \cdot X(f)
>$$

>[!Theorem] SLS in cascata e in parallelo
>In cascata:
>$$
>h(t)=h_1(t) \otimes h_2(t) \quad \iff \quad H(f)=H_1(f)\cdot H_2(f)
>$$
>In Parallelo:
>$$
>h(t)=h_1(t) + h_2(t) \quad \iff \quad H(f)=H_1(f)+ H_2(f)
>$$

>[!Theorem] Filtri Non Distorcenti
>Un filtro si dice non distorcente se vale:
>$$
>y(t)=K\cdot x(t-t_0) \quad \iff \quad Y(f)K \cdot X(f) e^{-2j\pi f t_0} \quad \implies H(f)=K \cdot e^{-2j \pi f t_0}
>$$
>Ovvero il filtro ha risposta in ampiezza Piatta e risposta in fase Lineare.
>
>In realtà è solo necessario che ciò valga nella Banda del segnale.

>[!Theorem] Trasformata Discreta Di Fourier (TDF)
>$$
>\large
>\begin{matrix}
>\text{Equazione di Analisi:} & \overline X(f)=\sum_n x(nT)e^{-j2\pi f \cdot nT}dt
>\\
>\text{Equazione di Sintesi:} & x(nT)=T\int_{\frac{-1}{2T}}^{\frac{1}{2T}} \overline  X(f)e^{-j2\pi f \cdot nT}df
>\\
>\text{Univocità:} & x(nT) \iff \overline X(f)
>\end{matrix}
>$$
>Si dimostra che:
>$$
>\overline X(f)=f_c \sum_k X(f-k f_c) \quad \quad f_c=\frac{1}{T}
>$$
>ovvero lo spettro si replica ai multipli della frequenza di campionamento, ovvero la TCF del segnale analogico viene periodicizzata.

>[!Theorem] Condizione di Nyquist
>Dobbiamo scegliere una frequenza di campionamento tale da evitare l'_aliasing_ (si sommano le bande di due repliche), ovvero:
>$$
>f_c \geq f_N = 2 B
>$$
>dove $f_N=2B$ è la frequenza minima di campionamento.
>
>Segnali reali però hanno banda illimitata, poiché sono finiti nel tempo, dobbiamo allora introdurre un **filtro anti-aliasing**, che limita la banda a $B'$, ottenendo una _nuova condizione di Nyquist_:
>$$
>f_c \geq f_N = 2 B'
>$$

>[!Theorem] Massima Frequenza Udibile dall'orecchio umano
>La minima frequenza udibile dall'orecchio umano è circa $20$ Hz.
>La massima frequenza udibile dall'orecchio umano è circa `20` KHz.
>Frequenza di campionamento standard: $44.1$ kHz per CD, $48$ kHz per DVD.

>[!Theorem] Interpolazione
>$$
>\hat x(t)=\sum_n x[n]\cdot p(t-nT)
>$$
>Potremmo usare **Interpolazione a mantenimento**, usando come interpolatore la funzione $p(t)=\text{rect}(\frac{t-\frac{t}{2}}{T}) \iff P(f)=T\cdot \text{sinc}(fT)e^{-j \pi f T}$, ma questo introduce distorsioni.
>
>Usiamo invece l'**interpolatore cardinale**:
>$$
>P(f)=T \text{rect}(fT) \quad \iff \quad p(t)=\text{sinc}\left(\frac{t}{T}\right)
>$$
>Notiamo che in frequenza, moltiplicando per una `rect` (con un adeguato $T$) filtriamo gli alias, mantenendo solamente la copia in banda base.

>[!Theorem] Teorema del Campionamento [Claude Shannon, 1949]
>Se $x(t)$ è limitato in banda e campionato con $f_c \geq 2B$, allora può essere ricostruito esattamente dai suoi campioni $x[n]$ tramite **interpolazione cardinale**.
>$$
>\hat x(t)=\sum_n x[n] \text{sinc}\left( \frac{t-nT}{T}\right)=x(t)
>$$

>[!Theorem] Interpolazione cardinale reale
>Quanto abbiamo visto nella pratica è irrealizzabile perché $p(t)=\text{sinc} (\frac{t}{T})$ è illimitato nel tempo -> somma infinita di campioni. 
>
>Inoltre non è realizzabile in tempo reale perché l'interpolatore cardinale non è *causale*, ma questo non è un problema per esempio per la ricostruzione di un file salvato su disco, situazioni in cui ho tutti i campioni, passati e futuri.
>
>Per evitare la somma infinita di campioni invece tronchiamo l'interpolatore cardinale:
>$$
>p_\Delta(t)=\text{sinc}\left(\frac{t}{T}\right)\text{rect} \left(\frac{t}{\Delta}\right)
>\atop
>\hat x(t)=\sum_n x[n] \cdot p_\Delta\left( {t-nT}\right)
>$$
>Dove la scelta di $\Delta$ è un compromesso tra complessità e accuratezza.
>
>Infine per rendere la ricostruzione causale, dopo aver troncato l'interpolatore cardinale è necessario traslarlo nel tempo:
>$$
>p_\Delta(t-\frac{\Delta}{2})
>$$
>ottenendo:
>$$
>\hat x(t)=\sum_n x[n] \cdot p_\Delta\left( t-nT -\frac{\Delta}{2} \right)
>$$
>in modo che la risposta impulsiva sia nulla per $t<0$, rendendo l’interpolatore causale.
# Teoria dei Codici
>[!Theorem] Variabili
>$R$: rate di informazioni utili sul totale: $R=\frac{k}{n}$
>$k$: bit in ingresso (per blocco)
>$n$: bit di uscita (per parola)
>$T_b$: tempo di bit in ingresso: ogni quanto arriva un nuovo bit in *ingresso*
>$T_c$: tempo di bit in uscita
>$$
>k\cdot T_b = n \cdot T_c
>$$
>$R_b$: velocità di trasmissione di bit in ingresso $R_b=\frac{1}{T_b}$
>$R_c$: velocità di trasmissione di bit in uscita: $R_c=\frac{1}{T_c} \geq R_b$ 
>`blocco`: insieme di bit in ingresso
>`parola`: insieme di bit in uscita

>[!Theorem] Codici a Ripetizione
>Un codice a ripetizione usa blocchi di dimensione di un bit, e parole di dimensione di n bit, per un rate di $R=\frac{1}{n}$, con $n$ dispari.
>Si esegue una decodifica a maggioranza.
>Rivela fino a $n-1$ errori.
>Corregge fino a $\frac{n-1}{2}$ errori.
>La probabilità di sbagliare $t$ bit in una parola di $n$ bit è:
>$$
>p(t,n)=\binom{n}{k}p^t(1-p)^{n-t}
>$$
>dove $p$ è la probabilità di errore su un bit.
>
>La probabilità di errore della parola di codice è (con $p_{e,b}$ prob. errore su un bit):
>$$
>P_{e,c}= \sum_{t=\frac{n+1}{2}}^n\binom n t p_{e,b}^t (1-p_{e,b}) ^{n-t} \approx\binom{n}{\frac{n+1}{2}}p_{e,b}^{\frac{n+1}{2}}
>$$

>[!Theorem] Codici a controllo di Parità
>$R=\frac{k}{k+1}$, usano solo un bit di ridondanza, detto **bit di parità**. È un codice a blocchi, con blocchi di $k$ bit.
>Il bit di parità è calcolato facendo la somma modulo 2 dei bit della stringa.
>Rivela errori con numero di bit coinvolti dispari, quindi sbaglia solo se sbaglio almeno 2 bit.
>La correzione avviene tramite ritrasmissione.

>[!Theorem] Codici a blocco lineari
>Ogni parola è una combinazione lineare (con coefficienti gli elementi di $b$) delle righe di una matrice generatrice. Sono codici a blocchi di $k$ bit.
>$b$: blocco in ingresso
>$c$: parola in uscita
>Un codice a blocco lineare è l'insieme delle $2^k$ parole $c=[c_1,c_2,...,c_n]$ generate dalla trasformazione lineare del blocco di bit $b$.
>$$
>\text c^{1\times n}=\text b^{1\times k} \text G^{k\times n}=\sum_i^k b_i g_i
>$$
>dove $\text G$ è la **Matrice generatrice del codice**.
>i bit $b_i$ fungono da coefficienti ($0$ o $1$) che selezionano quali righe di $\mathbf G$ sommare modulo $2$.
>
>Proprietà:
>1. Ogni parola di codice è combinazione lineare delle righe di $\mathbf G$
>2. Il codice è costituito da **tutte** le possibili combinazioni delle righe di $G$
>3. La somma di due parole di codice è ancora una parola di codice
>4. la `n-pla` di tutti zeri è sempre una parola di codice
>
>**Distanza di Hamming** $d_H(c_1,c_2)$: è il numero di posizioni in cui le due parole differiscono tra loro. Equivale al rango della matrice di controllo di parità $H$.
>**Peso di Hamming** $w(c)$: numero di posizioni in cui la parola differisce da 0.
>**Distanza Minima** $d_{\min}=\min_{i\neq j}d_H(c_i,c_j)=\min_kd_H(c_k,0)=min_kw(k)$ è la minima distanza di hamming, equivale al minimo peso di hamming. *Più alta è la distanza minima e meglio è il codice*.

>[!Theorem] Codice a Blocco Lineare Sistematico
>Una parola di codice a blocco lineare sistematico è composta da $k$ bit di informazione e $n-k$ bit di parità.
>$$
>\mathbf G^{k\times n}=[\mathbf I_k,\mathbf P^{k\times(n-k)}]
>\atop
>\mathbf c^{1\times n} = \mathbf{bG} = \mathbf b[\mathbf I_k,\mathbf P]=[\mathbf b, \mathbf {bP]=[\mathbf b^{1\times k}, \mathbf p^{1\times (n-k)}]}
>$$
>con $\mathbf P$ **matrice di parità**.
>
>**Matrice Controllo di Parità**:
>$$
>\mathbf{H}=[\mathbf P^T,\mathbf I_{n-k}]
>$$
>per ciascuna parola di codice si ottiene (nota: $P+P=I$):
>$$
>\mathbf{cH}^T=\mathbf {bGH}^T=0
>$$

>[!Theorem] Codici di Hamming
>I codici di Hamming sono definiti da un parametro $m \geq 2$:
>$$
>\begin{matrix}
>n=2^m-1
>\\
>k=2^m-m-1
>\end{matrix}
>$$
>La matrice di parità $P$ viene costruita così che le colonne di $H=[p^T,I_{n-k}]$ siano tutte le possibili $2^m-1$ combinazioni di $m$ bit (esclusa l'n-upla di tutti 0).
>*La distanza minima di qualsiasi codice di Hamming è* $d_\min = 3$.

>[!Theorem] Rivelazione degli errori
>Un codice è in grado di rilevare con certezza fino a $d_\min -1$ errori

>[!Theorem] Correzione degli errori
>Un codice lineare a blocchi è in grado di correggere fino a $\frac{d_\min -1}{2}$ errori.

>[!Theorem] Decodifica a massima Verosimiglianza (ML)
>Trovare il vettore $\hat x$ fra tutte le $2^k$ parole di codice che massimizza la probabilità condizionata $P(y|x)$. Si dimostra che:
>$$
>\hat x = \arg \max_{x\in \cal C}P(y|x)=\arg\min _{x\in \cal C}d_H(y,x)
>$$
>con $x$ parola trasmessa e $y$ parola ricevuta.

>[!Theorem] Decodifica a Sindrome
>Si definisce $s$ sindrome di $y$:
>$$
>s=\mathbf {yH}^T=(\mathbf x + \mathbf e)\mathbf H^T= \mathbf x \mathbf H ^t + \mathbf e \mathbf H^T= \mathbf e \mathbf H^T
>$$
>Proprietà:
>1. La sindrome $s$ è composta da $n-k$ cifre binarie
>2. ciascuna sindrome é associata a $2^k$ pattern di errore, ottenuti sommando al vettore $\mathbf e$ le $2^k$ parole di codice.
>Se $s\neq 0$ c'è un errore.
>
>Il decodificatore compie le seguenti operazioni:
>1. Calcola la sindrome $\mathbf s = \mathbf y \mathbf H^T$
>2. Associa la sindrome all'errore di peso minimo a cui corrisponde la sindrome associata a $y$ (il **coset leader**): $s \to e_{CL}(s)$
>3. Corregge l'errore sommando il **coset leader** alla n-upla $y$: $\hat x = y + e_{CL}(s)$ 
>
>Nota: la decodifica a sindrome coincide per costruzione con la decodifica a massima verosimiglianza.

# Sistemi di Comunicazione

>[!Theorem] Modulatore
>Il modulatore associa $Q$ bit a simboli di un alfabeto di cardinalità $M$, interpolando simboli genera il segnale analogico (**filtro di trasmissione**) in banda base, ed infine modula il segnale alla frequenza portante $f_0$, ottenendo un segnale analogico a radio-frequenza.
>$$
>\begin{matrix}
>Q=\log _2 M & \text{Numero di Bit per Simbolo}
>\\
>M= 2^Q & \text{Cardinalità dell'alfabeto dei Simboli}
>\\
>T_d=\frac{1}{R_d} & \text{Tempo per bit}
>\\
>T_s=T_d \cdot Q & \text{Intervallo di Segnalazione (tempo per simbolo)}
>\\
>f_s=\frac{1}{T_s}=\frac{R_d}{Q} & \text{Frequenza di Segnalazione}
>\end{matrix}
>$$
>La frequenza di segnalazione diminuisce all'aumentare della cardinalità dei simboli.
>
>Il segnale analogico $s_T(t)$ è dato da:
>$$
>s_T(t)=\sum_i a_i g_T(t-i \cdot T_s)
>$$
>e quello a radio-frequenza (modulato) è:
>$$
>s_T(t)=\sum_i a_i g_T(t-i \cdot T_s)\cos(2 \pi f_0 t)
>$$

>[!Theorem] Sistemi di Comunicazione PAM
>PAM - Pulse Amplitude Modulation
>Questi sistemi usano tipicamente una **mappa antipodale**, ovvero a valore medio nullo, con una cardinalità potenza di `2`: $M=2^Q$.
>Ad ognuno degli $M$ valori possibili per $Q$ bit viene assegnata una ampiezza del segnale.
>Il segnale analogico è **aleatorio** poiché dipende da simboli aleatori.

>[!Theorem] DSP
>La Densità Spettrale di Potenza del segnale trasmesso è:
>$$
>\begin{matrix}
>S_s(f)=\frac{1}{T_s}S_a(f)|G_T(f)|^2
>\\ \text{con} \quad S_a(f)=\sum_mR_a(m)e^{-2j\pi f M T_s} \quad \text{TDF della funzione di autocorrelazione dei simboli}
>\\
> \text{se: simboli incorrelati, mappa simmetrica, simboli equiprobabili}
> \\
> \text{allora} \to R_a(m)=\begin{cases} E\{ a_i^2\} =\sigma_a^2 & m=0 \\ \eta_a^2=0 & m \neq 0\\ \end{cases}
>\end{matrix}
>$$

>[!Theorem] Segnale Ricevuto-Segnale Trasmesso
>$$
>r(t)=\sum_i\sqrt \beta_i \cdot s_T(t-\tau_i) + w(t)
>$$
>Il segnale ricevuto in linea d'aria non è distorto: è attenuato e ritardato nel tempo.
>Però in realtà il mezzo non è spazio libero e il segnale ha più percorsi, ognuno con una attenuazione e un ritardo diversi.
>
>Il rumore è **AWGN**: additive white gaussian Noise. Un rumore è gaussiano bianco se è Gaussiano e ha DSP: $S_w(f)=\frac{N_0}{2}=\frac{K_B \cdot Temp_{Antenna}}{2}$ costante. Il rumore viene poi filtrato in ricezione, ottenendo un rumore $n(t)=w(t) \otimes g_R(t)$ non più bianco: $S_n(f)=\frac{N_0}{2} |G_R(f)|^2$, con valore medio nullo.
>
>In definitiva il segnale che arriva in ingresso al **demapper** (decodificatore di canale) è:
## Dimensionamento dei Filtri Trasmissione e Ricezione

>[!Theorem] **Condizione di Nyquist**
>data la risposta impulsiva globale del sistema PAM $g(t)=g_T(t) \otimes g_R(t)$:
>dobbiamo eliminare l'**interferenza intersimbolica**:
>$$
>\underbrace{ \begin{cases} g(mT_s)\neq 0 &m=0 \\ g(mT_s) = 0 & \forall m \neq 0 \end{cases}} _\text{Nel Tempo} \quad \iff \quad \underbrace {B\geq \frac{1}{2T_s} }_\text{in Frequenza}
>$$

>[!Theorem] Massimizzazione Del SNR
>$$
>\max \frac{g^2(0)}{E_{g_R}}
>$$
>ovvero un filtro adattato:
>$$
>g_R(t)=g_T(-t) \implies G_R(f)=G^*_T(f)
>$$

>[!Theorem] Impulsi a Coseno Rialzato (RCR)
>RCR sta per Raised Cosine Roll-off.
>Sono impulsi caratterizzati da un parametro $\alpha \in [0,1]$, detto **fattore di roll-off**.
>La loro trasformata presenta una parte piatta di valore $T_s$, che si estende fino a $\frac{(1-\alpha)}{2T_s}$. A questa parte piatta fa poi seguito la **zona di roll-off**, che si estende fino a $\frac{(1+\alpha)}{2T_s}$, durante la quale $G_{RCR}(f)$ scende dal valore $T_s$ a $0$.
>Nota: alla frequenza $f=\frac{1}{2}T_s$, $G_{RCR}(f)$ vale $\frac{T_s}{2}$ indipendentemento da $\alpha$.
>![[Pasted image 20260629185416.png]]
>Nel dominio del tempo l'impulso RCR ha la seguente espressione:
>$$
>g_{RCR}(t)=\frac{\sin(\pi t/T_s)}{\pi t /T_s}\frac{\cos(\alpha \pi t / T_s)}{1-(2 \alpha t /T_s)^2}
>$$
>e il grafico assomiglia a una $\text{sinc}(t/T_s)$. 
>Al diminuire di $\alpha$ nella frequenza assomiglia sempre più a una $\text{rect}$.
>a
>La scelta del fattore di Roll-off è quindi un compromesso tra efficienza spettrale (che migliora al decrescere di $\alpha$) e sensibilità agli errori di sincronizzazione (che diminuisce al crescere di $\alpha$).
>
>Combinando la condizione di Nyquist per l'annullamento dell'ISI e la massimizzazione del SNR otteniamo:
>$$
>G_T(f)=G_R(f)=\sqrt {G_{RCR}(f)}=G_{RRCR}(f) \quad \text{Root Raised Cosine Roll-Off}
>$$
>essi non sono impulsi di Nyquist, ma lo è la loro convoluzione.
>![[Pasted image 20260630115429.png]]

>[!Theorem] Filtro adattato
>$$
>g(t)=p(-t+t_0)
>$$
>Il filtro si dice adattato all'impulso $p(t)$ e massimizza il rapporto segnale rumore del segnale nell'istante $t_0$ quando il rumore in ingresso è bianco.
>La risposta in frequenza del filtro è:
>$$
>H(f)=\text{TCF}\{ p(t-t_0) \}=P^*(f)e^{-2j\pi f t_0}
>$$
>e ha quindi modulo $|H(f)|=|P(f)|$. Per cui nel dominio della frequenza il filtro adattato amplifica le zone frequenziali dove $|P(f)|$ è maggiore (quindi elevato SNR) e attenua dove $|P(f)|$ è minore (basso SNR).

>[!Theorem] Probabilità di Errore nei sistemi di comunicazione
>Al demapper arriva in ingresso (se i simboli sono equiprobabili):
>$$
>z(k)=\text{Simbolo Trasmesso} + n'(k) \implies z(k) \sim \cal N(\text{Simbolo Trasmesso}, \sigma_{n'}^2)
>$$
>con $\sigma_{n'}^2=\frac{\sigma_{n}^2}{\beta g^2(0)}$ ovvero il rumore in ingresso amplificato e normalizzato, e con $\sigma_n^2=\frac{N_0}{2}E_{g_R}$.
>Di solito con filtri RRCR: $P(e) \approx Q(\frac{1}{\sigma_{n'}})=Q\left( \sqrt{ \frac{6}{M^2-1}\frac{E_r}{N_0} }  \right)$ 
>
>Energia media ricevute per Simbolo (con $G_T(f)=G_{RRCR}(f)$):
>$$
>E_S=\frac{A^2}{3}(M^2-1)
>$$
>**SER**:
>$$
>SER=\frac{2(M-1)}{M}Q(\frac{1}{\sigma_\eta})
>$$
>con $\frac{1}{\sigma_\eta}=\sqrt{ \frac{6(E_S/N_0)}{M^2-1} }$ 

>[!Theorem] Mappatura di Gray
>Una mappatura di Gray è costruita in modo che simboli adiacenti differiscano di 1 solo bit.
>Sistemi di comunicazione con mappatura di Gray hanno probabilità di errore su un bit:
>$$
>P(e)=P(e)\cdot \frac{1}{\log _2 M}
>$$

>[!Theorem] Sistemi PAM con filtri RRCR
>Banda Impiegata da un sistema PAM con filtro RCR:
>$$
>B_T=\frac{1+\alpha}{2T_s}
>$$
>Efficienza spettrale:
>$$
>\eta_{sp}=\frac{R_d}{B_T}=[bit/s/Hz]
>$$
>con $R_d=\frac{\log_2M}{T_s}$.
>
>Quindi l'efficienza spettrale del sistema aumenta al crescere della cardinalità $M$ dell'alfabeto impiegato.
>
>L'efficienza energetica decresce al crescere di $M$.
>
>Si definisce **perdita energetica** di un sistema rispetto ad un altro l'aumento in dB del rapporto $E_d/N_0$ necessario per raggiungere la stessa SER.

>[!Theorem] Sistemi QAM, con $M^2-\text{QAM}$ 
>DSP:
>$$
>S_{RF}(f)=\frac{S_T(f-f_0)+S_T(f+f_0)}{4}
>$$
>Banda:
>$$
>B_s=\frac{1+\alpha}{r\log_2M^2}\frac{1}{T_b}
>$$
>quindi la QAM dimezza la banda necessaria.
>
>Efficienza Spettrale:
>$$
>\eta_s=\frac{R_b}{B_s}=\frac{r\cdot \log M^2}{1+\alpha}
>$$
>Probabilità di Errore:
>$$
>P(e)=2Q(\sqrt{\beta/N_0})=2Q\left(\sqrt{\frac{6E_s}{(M^2-1)N_0}}\right)
>$$
>Rapporto $E_s/N_0$:
>$$
>\frac{E_s}{N_0}=\frac{\beta E_{RF}}{N_0}=\frac{\beta}{2N_0}\frac{M^2-1}{3}
>$$
# Trasformate Notevoli

| Nome                       | tempo                                      | frequenza                               |
| -------------------------- | ------------------------------------------ | --------------------------------------- |
| f. esponenziale monolatera | $x(t)=e^{-t/T}u(t)$                        | $X(t)=\frac{T}{1+2j\pi f T}$            |
| funzione rettangolare      | $x(t)=\text{rect}\left(\frac{1}{T}\right)$ | $X(t)=T\text{sinc}(fT)$                 |
| f. Seno Cardinale          | $x(t)=\text{sinc}(2Bt)$                    | $\frac{1}{2B}\text{rect}(\frac{f}{2B})$ |
|                            | $x(t)=\text{sinc}^2(2 Bt)$                 | $\frac{1}{2B}\text{tri}(\frac{f}{4B})$  |
| Delta di Dirac             | $\delta(t)$                                | $\Delta(f)=1$                           |
| Funzione Costante          | $1(t)=1$                                   | $\delta(-f)=\delta(f)$                  |
| Coseno                     | $x(t)=\cos t(2 \pi f_0 t)$                 | $\frac{\delta(f-f_0)+\delta(f+f_0)}{2}$ |
note:
- seno cardinale: $\text{sinc}(\alpha)=\frac{\sin(\pi\alpha)}{\pi \alpha} \quad \forall \alpha \neq 0,\quad \text{sinc}(0)=1$ 
