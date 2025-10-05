#uni 
Qui vengono caricati i dati che servono per eseguire un programma, variabili ecc.

La ___memoria___ è un insieme di __celle__, ed ogni cella è in genere delle dimensioni di un byte (8 bit).

Un __oggetto__ è un gruppo di celle consecutive che vengono considerate dal programmatore come un'unica cella informativa.
Ogni oggetto ha due attributi:
1. __Indirizzo__ ovvero l'indirizzo della prima cella.
2. __Valore__ ovvero il contenuto di tutte le celle.
Ogni oggetto ha un __tipo__, dal quale si rileva automaticamente il range di valori consentiti e le operazioni consentite.

Un oggetto può essere __dichiarato__ e __definito__, una dichiarazione noon associa locazioni di memoria o azioni eseguibili, una definizione invece associa una locazione di memoria o un'azione eseguibile.

---
da qui in poi trattiamo della materia [[Calcolatori Elettronici]] del secondo anno.

---
La CPU intel x86 può accedere a singoli byte, word, long (double word) e qadruple word.
==Immaginiamo la memoria come una colonna di righe da 8 byte==.
`movq 8byte` sposta l'intera riga di 8 byte.
La memoria può essere costruita tale che il MSB finisca all'indirizzo più piccolo (BIG ENDIAN), oppure in modo che sia il LSB a finire nell'indirizzo più piccolo (LITTLE ENDIAN). Questa differenza non ci interessa, al massimo riguarda il [[Compilatore]].
L'architettura intel è Little Endian, come la maggior parte delle altre architetture, compresa quella del nostro calcolatore.
![[memoria1.svg|400]]
# L'offset
L'offset è la distanza tra due indirizzi, ovvero la differenza tra i due: conta quanti byte devo saltare per arrivare al secondo. L'offset da 1 a 7 è 6.
Ha anche senso parlare di offset negativi: l'offset da 1 a -2 è -3.
Gli indirizzi sono pensati in maniera circolare, poiché è così che la CPU opera somma e differenza: se all'estremo superiore sommo 1 torno all'estremo inferiore.
Posso quindi chiedermi quale sia la differenza tra $X$ e $Y$, con $X>Y$, posso scriverla come $X-Y$ e quindi viene negativa, oppure posso fare $|X-Y|_{{range}}$.
Posso scrivere l'insieme degli indirizzi come:
$$
[x,y) \text{ con} \{n|x\leq n \leq y\}
$$
# Allineamenti
Dire che un oggetto$x$ è allineato a $2^m$ vuol dire che  $x$ è multiplo di $2^m$, ovvero ha $m$ bit megno significativi resettati.
Dire che un oggetto $x$ è allineato ad un oggetto vuol dire che è allineato a $sizeof(oggetto)$.
Dire che un oggetto è allineato naturalmente vuol dire che è allineato a se stesso.
![[allineamento1.svg]]
# Limitazioni dell'architettura
Il formato delle istruzioni Intel consente un solo operando in memoria, tuttavia ci possono essere istruzioni con operandi impliciti, ad esempio l'istruzione `POP (%RDI)` ha due operandi in memoria poiché la pila è in memoria.

Il massimo numero di celle di memoria centrale nell'architettura Intel è $2^{54}$.
# Comunicazione CPU-Memoria
![[cpuRAM1.svg]]
- $/be$: byte enabler
La CPU emette il numero di riga e il numero dei byte delle celle interessate.
È possibile mettere una stessa informazione su due righe diverse (solo nell'architettura [[Intel]]) anche se il compilatore cerca in tutti i modi di evitarlo.

Pensiamo alla RAM come composta da 8 chip "larghi" un byte e lunghi tanto quanto la RAM che vogliamo ottenere, uniti uno accanto all'altro, cosicché ognuno formi una colonna. Come possiamo collegarli alla [[CPU]]?
- $A$ è l'indirizzo della riga e va collegato in parallelo in quanti è a comune con tutti i chip
- $/be$ va scomposto e connesso in serie poichè ogni chip corrisponde ad un diverso bit
- $D$ va collegato come $/be$
- infine $WR$ e $RD$ vanno collegati in parallelo
Ultimo particolare: i chip di RAM devono capire che il processore stia effettivamente chiamando loro, ciò viene implementato tramite una maschera di select $/s$, come abbiamo visto a [[Reti Logiche]]. Inoltre ai chip interessa solo l'offset relativo a loro stessi, dividiamo quindi $A$ in $/cs$ e $AA$, e colleghiamo la $A$ dei chip ad $AA$ e la $/cs$ dei chip all
omonima.
# Accesso a celle su righe diverse
Come abbiamo detto è possibile depositare o prelevare una stessa informazione su righe diverse:
![[memoria2.svg]]
L'offset di questa locazione è: $\text{offset}={nRiga+}\text{/}be$, in questo caso sarebbe $13=8+5$ e una possibile istruzione che utilizzi questa locazione è:`MOVQ 13, %RAX`.

Una domanda che sorge spontanea è: chi si occupa del fare implicitamente i ==due== accessi in memoria che richiede tale offset? Qualcuno potrebbe pensare che è il software, invece è l'hardware, nel microcodice del processore è prevista questa istruzione, questo spiega per quale motivo per esempio nell'architettura [[ARM]] questo accesso non è disponibile.