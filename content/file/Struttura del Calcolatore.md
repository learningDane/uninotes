#uni 
![[strutturacalcolatore.svg]] 
Reminder sulla memoria che gli studenti dimenticano spesso:
- La [[Memoria]] è ad accesso casuale, ovvero l'accesso a due celle diverse è indifferente dal punto di vista di [[complessità]] computazionale.
- Il significato del contenuto in memoria dipende dall'uso che se ne fa, non ha significato intrinseco
Reminder su I/O:
- Le periferiche sono di natura diverse, necessitiamo di interfacce per renderle uguale al processore.
- Letture/Scritture su interfacce possono avere effetti collaterali, al contrario delle letture/scritture in memoria (una periferica può reagire ad un accesso da parte del processore).
Bus:
- tutti i dispositivi sentono il processore, ma solo uno risponde, quale viene determinato dalle maschere di select sull'indirizzo che vuole il processore.
- nell'architettura Intel x86 gli indirizzi di I/O stavano su uno spazio di memoria separato dal resto, sui dispositivi moderni non è più così e si ha uno solo spazio di memoria.
Bootstrap:
- nei primi computer il bootstrap doveva essere inserito manualmente dagli operatori all'avvio, ora questo sta nella [[Rom]] (per esempio questa contiene il BIOS).


