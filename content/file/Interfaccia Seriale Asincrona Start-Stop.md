#uni 
Queste comunicano con dispositivi esterni in accordo ad un vecchio standard del 1969, il **EIA-RS232**.
Si utilizza una unica linea di collegamento, sulla quale vengono trasmessi l'uno dopo l'altro i bit, questi bit vengono inviati a gruppi, detti __Trame__. 
Non ci sono specifiche sul tempo che può trascorrere tra una trama e l'altra, i bit invece all'interno di una trama devono essere inviati con una cadenza regolare, intervallati di un tempo __T__, detto __tempo di bit__.
Il numero di bit inviati nell'unità di tempo, all'interno di una trama, è detto __bit-rate__, e vale $\frac{1}{t}$.
Le trame sono costituite da un numero di bit che va da 7 a 12.
Una parte di questi bit (detti __bit utili__) costituisce l'informazione vera.
In generale una trama contiente:
- un bit di start
- 8 bit utili
- un eventuale bit di parità
- uno o due bit di stop
# Funzionamento
Tra una trama e l'altra, la linea viene mantenuta in uno stato detto __marking__ (ovvero 1), il bit di start, ovvero la scesa della linea in stato __spacing__ (0), segna l'inizio della trasmissione, utilizzando la codifica __NRZ__ ogni bit utile è trasmetto tenendo la linea in marking o spacing a seconda che sia 1 o 0.
Dopo gli 8 bit utili arriva l'eventuale bit di parità e poi gli 1 o 2 bit di stop, dopodiché la linea viene mantenuta in marking fino al prossimo bit di start, a segnalare l'inizio della prossima trama.
> Il Bit meno significativo (__LSB__) segue temporalmente il bit di start.

```
              start   1     0              0   0    stop
marking: ---         ---         ---                --- ----------
             \     /     \     /      ecc         /
spacing:       ---         ---            --- ---
			<- LSB                         -> MSB
```
