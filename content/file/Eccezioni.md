#uni 
Le prime 32 entrate della IDT, sono riservate per le eccezioni.
Con questo termine indichiamo condizioni speciali, o errori, che il processore rileva durante la sua normale esecuzione.
I tipi delle eccezioni sono fissi e consultabili sul manuale del processore.

Le eccezioni sono classificabili come segue:
- **trap**: vengono sollevate *tra* l'esecuzione di una istruzione e la successiva (penso che sia legato al cambiamento di `%rip`). Il processore salva il pila l'indirizzo dell'istruzione successiva, come per le interruzioni esterne.
- **fault**: vengono sollevate *durante* l'esecuzione di una istruzione. Il processore salva in pila l'indirizzo dell'istruzione che stava eseguendo al verificarsi del fault. L'idea è che la routine può cercare di correggere il problema che ha causato il fault. Per fare questo dobbiamo essere in grado di tornare allo stato del processore prima che eseguisse l'istruzione: per quanto riguarda i registri il processore apporta le modifiche in delle copie di lavoro e trasferisce il contenuto da queste copie nei registri effettivi solo al termine dell'istruzione.
- **abort**: possono verificarsi in qualsiasi momento e indicano errori particolarmente gravi