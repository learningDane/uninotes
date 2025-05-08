#uni 
Questo metodo è stato presentato da Walter R. Evans ne "Control System Synthesis by Rott Locus Method", sulla rivista [ieeexplore.com](ieeexplore.com).
![[controlloinfeedback.svg]]
Questo è un metodo per studiare nel piano complesso, l'effetto della reazione negativa sui poli del sistema in catena chiusa, a partire dalla conoscenza della [[Funzione di Trasferimento]] in catena aperta $G(s)$ (dove $G(s)$ è la fdt del sistema da controllare).
Noi tratteremo ___controllori proporzionali___, con quindi $C(s)=k$.

Calcolando la funzione di trasferimento in anello aperto otteniamo:
$$
K \cdot G(s)=K \cdot \frac{\prod_{i=1}^m(s-z_i)}{\prod_{i=1}^n(s-p_i)}=K \cdot \frac{n(s)}{d(s)}
$$
In anello chiuso otteniamo invece:
$$
W(s)=\frac{K \cdot G(s)}{1+K \cdot G(s)}=\frac{K \cdot n(s)}{d(s)+K \cdot n(s)}
$$
Notiamo quindi che gli zeri del sistema non cambiano passando da anello aperto a chiuso, cambiano invece i poli.

Chiamiamo quindi $d(s)+ K \cdot n(s)=0\to \frac{n(s)}{d(s)}=-\frac{1}{K}$ ___equazione caratteristica___ e chiamiamo invece ___Luogo delle Radici___ l'insieme delle radici dell'equazione caratteristica al variare di $K$.

Definiamo la seguente ___Condizione di Fase___:
$$
\begin{cases}
\angle n(s)- \angle d(s)=\pi \pm 2h\pi  & k>0 \\
\angle n(s)- \angle d(s)=0\pm2h\pi & k<0
\end{cases}
$$
e definiamo la seguente ___Condizione di Modulo___:
$$
\left| \frac{n(s)}{d(s)} \right|=\frac{1}{|K|}
$$
# Utilizzo
Una volta trovato il polo che vogliamo ottenere, in base alle specifiche, per trovare il relativo valore di $K$ applichiamo la seguente formula:
$$
K|_{s=s_i}=\frac{|d(s_i)|}{|n(s_i)|}
$$
# Sistemi di Secondo Grado: relazione tra frequenza naturale e smorzamento e luogo delle radici
Data una [[Funzione di Trasferimento]] $G(s)=\frac{w_n^2}{s^2+2 \xi w_n s + w_n^2}$, con i poli $s_{1,2}=-\xi w_n \pm w_n j \sqrt{1- \xi^2}$, il seguente grafico rappresenta la posizione dei poli in relazione allo smorzamento $\xi$ e alla frequenza naturale $w_n$:
![[luogoradicisistemasecondogrado.svg]]
- se $\xi=1$ abbiamo smorzamento perfetto, senza oscillazioni
- se $\xi<1$ abbiamo un sistema oscillante
- se $\xi>1$ abbiamo un sistema sovrasmorzato, con quindi una risposta lenta.
# Regole di Costruzione del Luogo delle Radici
## Regola 1
Il numero di radici in catena chiusa è uguale al numero di poli della funzione in ciclo aperto, che è uguale al numero di Rami del luogo delle Radici.
## Regola 2
Il luogo delle radici parte dai poli in ciclo aperto e arriva sugli zeri in ciclo aperto al finito o all'infinito.
## Regola 3
Tutto l’asse reale appartiene al luogo delle radici.
## Regola 4
Se $K>0$ appartengono al luogo delle radici tutti i punti che lasciano alla propria destra un numero ==dispari== di singolarità.
## Regola 5
Se $K<0$ appartengono al luogo delle radici tutti i punti che lasciano alla propria destra un numero ==pari== di singolarità.
## Regola 6
Il luogo delle radici è simmetrico rispetto all'asse reale.
# Regola 7
Il luogo delle radici ha rami che non si sovrappongono mai, al massimo si incrociano in punti singolari detti ___poli multipli___.
# Regola 8
Gli asintoti dividono il piano complesso in parti equiangole e simmetriche rispetto all'asse reale.
# Regola 9
Il centro degli asintoti è il baricentro delle singolarità e si calcola come segue:
$$
\sigma=\frac{\sum^np_i-\sum^mz_i}{n-m}
$$
# Poli Multipli
In un punto multiplo la radice multipla $s_i$ è soluzione di: $\frac{d'(s)}{d(s)}=\frac{n'(s)}{n(s)}$, e nel caso di $m$ zeri e $n$ poli si verifica che:
$$
\sum_{i=1}^n\frac{1}{s-p_i}=\sum_{i=1}^m\frac{1}{s-z_i}
$$
Risolvendo questa equazione quindi otteniamo i poli multipli.