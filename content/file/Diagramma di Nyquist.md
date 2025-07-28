#uni 
Questo diagramma serve per rappresentare la risposta in frequenza della [[Funzione di Trasferimento]] in forma polare di sistemi SISO in catena chiusa, a partire dalla conoscenza del sistema in catena aperta.
Gli assi sono in scala lineare, per questo non è adatto per rappresentare moduli molto piccoli.
Può essere tracciato per punti al variare di $\omega$.
Viene normalmente tracciato a partire dalla conoscenza del [[Diagramma di Bode]] della funzione. 
# Metodo
1. Trovare [[Diagramma di Bode]].
2. Dal piano complesso posso escludere tutti i quadranti in cui sicuramente il diagramma di nyquist non passa (in base alla fase assunta nel diagramma di bode).
3. Trovare quadrante (angolo) di partenza: $\theta = h \cdot \frac{\pi}{2}$, con $h$ tipo del sistema (oppure guardare da dove parte il diagramma della fase).
4. Se il sistema è di tipo diverso da $0$ ha sicuramente un asintoto, per trovarlo calcolare $\lim_{w \to 0} G(jw)$ e scomporre in parte reale ed immaginaria.
5. Trovare l'angolo di arrivo, quindi il limite di $w$ che tende ad $\infty$ del diagramma di fase.
6. Specchio il diagramma rispetto all'asse reale
7. Partendo da $0^-$, compio una mezza rotazione all'infinito in senso orario per ogni polo nell'origine. 
# Criterio di Nyquist
Il criterio di Nyquist è un criterio per giudicare la stabilità di un sistema in catena chiusa a partire dalla conoscenza del sistema in catena aperta.

>Un sistema a retroazione unitaria è **stabile** se il **numero di avvolgimenti** in senso antiorario del diagramma di Nyquist attorno al punto $(-1 \ ; \ 0)$ è **uguale al numero di poli a parte reale positiva del sistema in anello aperto** $L(s)=C(s) \cdot G(s)$.

Una volta tracciato il diagramma di Nyquist per il sistema in catena aperta $G(s)$, definiamo:
- $N_{ao}$: il numero di rotazioni in senso antiorario attorno al punto $\left( \frac{-1}{k},0 \right)$.
- $P^+$: il numero in catena aperta ($G(s)$) di poli a parte reale positiva.
- $Z=N_{ao}-P^+$: il numero di Poli instabili in catena chiusa

>Quindi: il sistema è stabile in catena chiusa se e solo se $Z=0$, inoltre è sicuramente instabile se $N_{ao}<0$ (ovvero compie rivoluzioni in senso ORARIO attorno a $(\frac{-1}{k},0$).

Perché funziona? Quando chiudi un sistema $G(s)$ in catena chiusa ottiene $G_{c.chiuso}=\frac{G(s)}{1+G(s)}$ e vuoi quindi che il denominatore sia lontano da $0$, ovvero vuoi che $G(s)$ sia lontano da $-1$. Mettendo un controllore proporzionale $k$, la $G(s)$ diventa $k \cdot G(s)$, quindi vuoi che questa funzione sia lontana dal punto $\left( \frac{-1}{k},0 \right)$.
# Particolari utili
- Approssimazione di Taylor: $\frac{1}{1+x} \approx 1-x$ per $x \to 0$.