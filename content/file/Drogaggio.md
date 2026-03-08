#uni 
Il Drogaggio è una tecnica che consiste nel rimpiazzare alcuni atomi di un semiconduttore con altri atomi, di un gruppo chimico superiore o inferiore ([[Periodic Table]]).

Il caso più comune è drogare Silicio con Fosforo, Arsenico o Boro.

L'obiettivo del Drogaggio è regolare la conduzione del semiconduttore, introducendo lacune o elettroni liberi.
# Tecniche di Drogaggio
Esistono più tecniche di drogaggio, che si differenziano per costi, complessità e precisione.
## Tecnica da Laboratorio
Il metodo più facile, e meno preciso, è quello di spalmare sulla superficie del semiconduttore il materiale drogante e sottoporre il tutto ad alte temperature, a questo punto per effetto della [[Corrente di Diffusione]] il drogante entrerà naturalmente a fare parte del reticolo cristallino.
## Tecnica Industriale
Industrialmente il drogaggio si ottiene tramite l'**Impiantazione Ionica**, utilizzando un **impiantatore**, il quale genera ioni di drogante e li "spara" sul semiconduttore.
A questa prima fase segue l'**annihilazione termica**, svolta a temperature estremamente elevate ($\sim 1000^\circ \text C$) durante la quale vengono eliminate impurità per via della [[Corrente di Diffusione]].

Questa procedura può essere resa meno invasiva, in modo da causare meno danni al reticolo, "sparando" gli ioni droganti attraverso un primo strato di un altro materiale, rallentando gli ioni e mantenendo contenuti i danni.

Questa tecnica permette di più finemente controllare il drogaggio.
# Tipi di Drogaggio
Sono possibili due tipi di drogaggio, che possono coesistere sullo stesso semiconduttore, divisi in base al gruppo del drogante introdotto nel reticolo.
## Drogaggio di tipo N - gruppo superiore
Per drogare tipo N il Silicio (gruppo IV) necessitiamo di droganti del gruppo V, di solito vengono usati fosforo e arsenico, entrambi mortali in ambito pratico.
Il drogaggio tipo N punta ad aumentare il numero di elettroni liberi (da qui "N"), introducendo droganti con un elettrone sull'orbitale più esterno in più al Silicio.

Tramite la teoria dei reticoli è possibile dimostrare che a temperatura ambiente, gli elettroni in surplus sono in grado di staccarsi dall'atomo di drogante, e diventare quindi elettroni liberi, questo processo prende il nome di **Donazione di Elettrone**, dove l'atomo drogante che dona l'elettrone prende il nome di **atomo donatore**.

La concentrazione di atomi donatori viene indicata con $N_D$ e normalmente vale $10^{14}\text{cm}^{-3} <N_D <10^{21}\text{cm}^{-3}$.
Viene anche indicata con $N_D^+$, ad indicare il fatto che avendo perso un elettrone questi atomi sono carichi positivamente

Teniamo conto del fatto che aumentando il numero (e la concentrazione) di elettroni liberi, aumentiamo anche il fenomeno della ricombinazione.

Sfruttando la [[Legge di Azione di Massa]]:
![[Legge di Azione di Massa]]
possiamo notare che a temperatura ambiente raggiungiamo una bilancio in equilibrio come segue:
$$
\large
\begin{matrix}
n \approx N_D
\\
p\approx\frac{n_i^2}{n}\approx \frac{n_i^2}{N_D}
\\
\implies n \gt p
\end{matrix}
$$

## Drogaggio di tipo P
Il drogaggio tipo P è esattamente il duale del drogaggio tipo N, per cui utilizza droganti del gruppo chimico (nel caso del Silicio) III, come il Boro.

Per ogni atomo di drogante introdotto, introduciamo una lacuna.

L'atomo di Boro che riceve un elettrone dal reticolo prende il nome di **Accettatore di Elettrone**.

La concentrazione di accettatori viene indicata con $N_A$ ($N_A^-$) e di solito vale $10^{14}\text{cm}^{-3}\lt N_A\lt 10^{21}\text{cm}^{-3}$.

All'equilibrio abbiamo:
$$
\large
\begin{matrix}
p=N_A
\\
n=\frac{n_i^2}{N_A}
\\
\implies p \gt n
\end{matrix}
$$
# Considerazioni finali
Va rimarcato che $N_D^+$ e $N_A^-$ sono cariche *fisse* nel reticolo.

È possibile nello stesso semiconduttore utilizzare sia drogaggio N che P.

In natura i semiconduttori non sono mai intrinseci.