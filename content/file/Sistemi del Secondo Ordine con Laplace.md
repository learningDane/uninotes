#uni 
Supponiamo di aver risolto un sistema fisico, otteniamo quindi una [equazione differenziale](Equazioni%20Differenziali.md) del secondo ordine:
$$
a_2\frac{d^2y}{dt^2}+ a_1\frac{dy}{dt}+a_0y=b_0u
$$
Applicando la [proprietà di derivata della Trasformata di Laplace](Trasformata%20di%20Laplace.md#Proprietà%20di%20derivazione%20in%20t), e dopo passaggi di manipolazione algebrica otteniamo:
$$
Y(s)=\underbrace{\frac{b_0}{a_0+a_1 \cdot s + a_2 s^2}U(s)}_\text{risposta in evoluzione forzata} + \underbrace{\frac{a_2 \cdot s \cdot y(0)+a_2 \cdot \dot y(0)+a_1 \cdot y(0)}{a_0+a_1 \cdot s +a_2 \cdot s^2}}_\text{risposta in evoluzione libera}
$$
Se il sistema è stabile, dopo un certo tempo $t$, la risposta in evoluzione libera tende a $0$ e possiamo quindi ignorarla.
# Poli
Possiamo quindi ora trovare i poli della risposta forzata:
$$
\begin{matrix}
Y(s)=\frac{b_0}{a_0+a_1 \cdot s + a_2 s^2}U(s)  \\
p_{1,2}=\frac{-a_1 \pm \sqrt{\Delta}}{2 \cdot a_2} \\
\Delta=a_1^2-4\cdot a_0 \cdot a_2
\end{matrix}
$$
## Poli Reali
Scriviamo ora la funzione $G(s)=\frac{Y(s)}{U(s)=1}=Y(s)$ nelle due forme di Bode ed Evans, introducendo 4 variabili e le relative relazioni con i parametri del sistema:
$$
\begin{matrix}
\text{Bode:} \quad G(s)=G(0)\frac{1}{(1+s \cdot T_1)(1+ s \cdot T_2)}, \quad G(0)=\frac{b_0}{a_0} \\
\text{Evans:} \quad G(s)=\frac{\frac{b_0}{a_2}}{(s+p_1)(s+p_2)} \\
p_1 \cdot p_2=\frac{1}{T_1 \cdot T_2}=\frac{a_0}{a_2} \\
p_1 + p_2=\frac{-a_1}{a_2} \\
T_1 =\frac{1}{p_1}, \quad T_2=\frac{1}{p_2}
\end{matrix}
$$
Calcoliamo la risposta al gradino:
$$
\begin{matrix}
Y(s)=G(s) \cdot U(s)= \frac{\frac{b_0}{a_2}}{(s+p_1)(s+p_2)}\cdot\frac{1}{s}=\frac{A}{s}+\frac{B}{s+1/T_1}+\frac{C}{s+1/T_2} \\
A=\frac{b_0}{a_0}=G(0) \\
B=\frac{T_1}{T_2-T_1}\cdot G(0) \\
C=-\frac{T_2}{T_2 -T_1} \cdot G(0) \\
y(t)=G(0) \cdot (1+\frac{T_1 \cdot e ^{-tT_1}-T_2 \cdot e ^{-tT_2}}{T_2-T_1}) \cdot1(t)
\end{matrix}
$$
> Grafico della risposta al gradino di un generico sistema di secondo ordine con poli reali distinti:
> ![[rispostaalgradinosistemasecondoordinepolirealidisinti.svg]]
## Poli Reali Coincidenti
Calcoliamo la risposta al gradino di un sistema di secondo grado con poli reali coincidenti:
$$
\begin{matrix}
Y(s)=G(s) \cdot U(s)=\frac{b_0/a_2}{\left( s+\frac{1}{T_2} \right)^2}=\frac{A}{s}+\frac{B}{s+1/T}+\frac{C}{(s+1/T)^2} \\
T^2=\frac{1}{p^2}=\frac{a_2}{a_0} \\
A=\frac{b_0}{a_0}=G(0) \\
B=-G(0) \\
C=-\frac{G(0)}{T} \\
y(t)=G(0) \cdot(1-e^{-t/T}\cdot(1+\frac{1}{T}))+1(t)
\end{matrix}
$$
## Poli Complessi Coniugati
### Risposta Libera
Ridenominiamo la parte reale e la parte e la parte complessa dei poli:
$$
\begin{matrix}
G(s)=\frac{Y(s)}{U(s)}=\frac{b_0}{a_0+a_1 \cdot s + a_2 s^2} \\
p_{1,2}=\frac{-a_1\pm\sqrt{a_1^2-4 \cdot a_0 \cdot a_2}}{2 \cdot a_2} \\
\alpha=-\frac{a_1}{2 \cdot a_2} \\
\beta=\sqrt{\frac{a_0}{a_2}(1-\frac{a_1^2}{4 \cdot a_2 \cdot a_0})} \\ \\
\text{Pulsazione di Risonanza:} \\
w_0=\sqrt{\frac{a_0}{a_2}} \\ \\
\text{Smorzamento:} \\

\xi=\frac{a_1}{2 \sqrt{a_0 \cdot a_2}}
\end{matrix}
$$
- Lo smorzamento descrive l'energia dissipata dal sistema.
- Se $\alpha$ fosse nullo (la parte reale), vorrebbe dire che $a_1$ sarebbe nullo e quindi lo sarebbe anche lo smorzamento e il sistema oscillerebbe all'infinito.

Possiamo anche riscrivere la forma di Bode e quella di Evans in funzione di questi nuovi parametri:
$$
\begin{matrix}
\text{Bode:} \quad G(s)=\frac{G(0)}{1+2 \cdot \xi \cdot\frac{s}{w_0}+\frac{s^2}{w_0^2}} \\
\text{Evans:} \quad G(s)=\frac{G(0) \cdot w_0^2}{s^2+2\cdot \xi \cdot w_0 \cdot s+w_0^2}
\end{matrix}
$$
# Risposta al Gradino di Sistemi del Secondo Ordine
Calcoliamo la risposta al gradino di questi sistemi:
$$
\begin{matrix}
y(t)=L^{-1}\{G(s) \cdot \frac{1}{s}\}= \\
y(t)=G(0)\cdot[1-e^{- \xi w_0 t}(\cos(\underbrace{\sqrt{1-\xi^2}\cdot w_0}_\text{Pulsazione} \cdot t)+\frac{\xi}{\sqrt{1-\xi^2}}\sin(\underbrace{\sqrt{1-\xi^2} \cdot w_0}_\text{Pulsazione} \cdot t))] \cdot 1(t) \\ \\

\text{Forma compatta:} \\
y(t)=1-e^{-\xi w_o t}\sqrt{1+\frac{\xi ^2}{1-\xi^2}}\sin\left(w_0 \sqrt{1-\xi^2}\cdot t+ \arctan\left(\frac{\sqrt{1-\xi^2}}{\xi}\right)\right)
\end{matrix}
$$
e disegnamone un generico grafico qualitativo:
![[rispostaGradinoSistemiSecondoGrado.svg]]
## Parametri Caratteristici
- $t_d$: tempo di ritardo, il tempo necessario a raggiungere il 50% del guadagno statico
- $t_r$: tempo di risposta, il tempo necessario a raggiungere il valore del guadagno statico: $\text{per un target di 90\%G(0):}\quad t_r=\frac{1.8}{w_n}$ 
- $s$ ( o $M_p$): overshoot, la massima elongazione relativa, di solito in percentuale: $s\%=100e^{\frac{\xi \pi}{\sqrt{1-\xi^2}}}$
- $t_p$ (o $t_{max}$): tempo di massima elongazione: $t_{max}=\frac{\pi}{w_n \sqrt{1- \xi ^2}}$ 
- $t_s$ (o $t_{ass}$): tempo di assestamento, il tempo necessario per raggiungere (e mantenere) un valore compreso in una certa fascia di tolleranza $\epsilon$, di solito del $2\%$, oppure del $5\%$: $t_{ass}=\frac{1}{\xi w_n}\ln(valore\%)$  
- $T_P$: periodo di oscillazione, periodo tra due picchi: $T_P=\frac{2 \pi}{w_n \sqrt{1- \xi^2}}$ 