#uni 
Un diagramma di Bode è una rappresentazione grafica della [[Risposta in Frequenza]] di un [[Sistema LTI]] e che consiste in due grafici che rappresentano rispettivamente l'ampiezza (o modulo) e la fase della funzione complessa di risposta in frequenza.
Questo diagramma può anche essere usato su sistemi instabili, dei quali quindi non ha senso studiare una risposta in frequenza.
- il modulo $|G(jw)|$ viene espresso in deciBel: $|G(jw)|_{dB}=20\log_{10}(|G(jw)|$.
- la fase viene espressa linearmente, in gradi o in radianti.
- per la pulsazione viene usata una scala logaritmica invece, quindi una unità equivale ad un fattore 10
- Una unità sull'ascissa prende il nome di ___decade___: ovvero la distanza in scala logaritmica tra due numeri cui rapporto è 10.
- ___Ottava___ è invece la distanza in scala logaritmica tra due numeri cui rapporto è 2.

È importante osservare che per le proprietà logaritmo del prodotto e della proprietà di [[Convoluzione]] della [[Trasformata di Laplace]], se volessi trovare il diagramma di Bode di due sistemi collegati in serie, basta sommare i grafici dei due sistemi.
# Rappresentazione di una FdT tramite il diagramma di Bode
Porto la [[Funzione di Trasferimento]] in Forma di Bode:
$$
G(jw)=

\frac {\overbrace {K_B} ^\text{Guadagno di Bode}}
{ \underbrace{(jw)^h}_\text{Poli nell'origine} }

\frac{\prod_{i=1}^{m-n} ( \overbrace{1\pm jwT_{zi}}^\text{zeri semplici} )}
{\prod_{i=1}^{n-h-r}( \underbrace{1\pm jwT_{pi}}_\text{Poli semplici})}

\frac{\prod_{i=1}^{n}( \overbrace{1\pm jw\frac{2\xi_{zi}}{w_{0zi}}-\frac{w^2}{w_{0zi}^2}}^\text{zeri complessi coniugati} )}
{\prod_{i=1}^{r}( \underbrace{1\pm jw\frac{2\xi_{pi}}{w_{0pi}}-\frac{w^2}{w_{0pi}^2}}_\text{Poli complessi coniugati} )}
$$
Costruisco ora il diagramma di Bode come somma delle singole [[#Funzioni Elementari]].
# Funzioni Elementari
## Guadagno Costante
$$
\begin{matrix}
G(s)=k \\
G(jw)=|k|e^{j\phi} \\
|G(jw)|=|k| \\
\phi G=\begin{cases}
0  & Im(k)>0 \\
-\pi  & Im(k)<0
\end{cases}
\end{matrix}
$$
![[rispostaarmonicaguadagnocostante.svg]]
## Polo nell'Origine
$$
\begin{matrix}
G(s)=\frac{1}{s} \\
G(jw)=\frac{1}{jw} \\
|G(jw)|=\frac{1}{w} \\
\phi G=-\frac{\pi}{2}
\end{matrix}
$$
![[rispostaarmonicapoloorigine.svg]]
## Polo Semplice
$$
\begin{matrix}
G(s)=\frac{1}{1+\tau s} \\
G(jw)=\frac{1}{1+ \tau j w} \\
|G(jw)|=\frac{1}{\sqrt{1+\tau^2w^2}} \\
\phi G=-\arctan(\tau w)
\end{matrix}
$$
![[rispostaarmonicamodulopolosemplice.svg]]![[rispostaarmonicafasepolosemplice.svg|500]] 
## Zero Semplice
$$
\begin{matrix}
G(s)=1+\tau s \\
G(jw)=1+\tau j w \\
|G(jw)|=\sqrt{1+\tau ^2 w^2} \\
\phi G=\arctan(\tau w)
\end{matrix}
$$
![[rispostaarmonicamodulozerosemplice.svg]]
![[rispostaarmonicafasezerosemplice.svg|500]]
## Polo Complesso
$$
\begin{matrix}
G(s)=\frac{1}{1+\frac{2 \xi }{w_0}s+\frac{s^2}{w_0^2}} \\
G(jw)=\frac{1}{1+\frac{2 \xi }{w_0}jw-\frac{w^2}{w_0^2}} \\ 

|G(jw)|=\frac{1}{\sqrt{\left(1-\frac{w^2}{w_0^2}\right)^2+4\frac{w^2}{w_0^2}\xi^2} }  &   \begin{cases}
|G(jw)|_{dB}=0 & w<<w_0 \\
|G(jw)|_{dB}=40\log(w_0)-40\log(w) & w>>w_0 \\
|G(jw)|=\frac{1}{2\xi} & w=w_0
\end{cases} \\
\phi G(jw)=atan2\left(\frac{2\xi w w_0}{w_0^2-w^2}\right) 
 &   \begin{cases}
\phi G(jw)=0  & w<<w_0 \\
\phi G(jw)=-\frac{\pi}{2}  & w=w_0 \\
\phi G(jw)=-\pi & w>> w_0
\end{cases} 

\end{matrix}
$$
![[rispostaarmonicapolocomplessoModulo.gif|500]]
![[rispostaarmonicapolocomplessoFase.gif|500]]
## Zero Complesso
## Ritardo Puro