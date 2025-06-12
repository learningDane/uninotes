#uni 
Questo diagramma serve per rappresentare la risposta in frequenza della [[Funzione di Trasferimento]] in forma polare di sistemi SISO.
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
# Criterio di Nyquist
# Particolari utili
- Approssimazione di Taylor: $\frac{1}{1+x} \approx 1-x$ per $x \to 0$.