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
da qui in poi trattiamo della materia [[Calcolatori elettronici]] del secondo anno.
La CPU intel x86 può accedere a singoli byte, word, long e 8byte.
Immaginiamo la memoria come una colonna di righe da 8 byte.
`movq 8byte` sposta l'intera riga di 8 byte.
La memoria può essere costruita tale che il MSB finisca all'indirizzo più grande (BIG ENDIAN), oppure in modo che sia il LSB a finire nell'indirizzo più grande (LITTLE ENDIAN). Questa differenza non ci interessa, al massimo riguarda il [[Compilatore]].
L'architettura intel è Little Endian, come la maggior parte delle altre architetture.
![[Memoria 2025-02-24 12.04.40.excalidraw]]
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
![[Pasted image 20250224123143.png|400]]
