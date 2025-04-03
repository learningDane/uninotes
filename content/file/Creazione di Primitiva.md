#uni 
# Passaggio di Parametri
Basta che nella dichiarazione della primitiva c_primitiva io aggiunga che si deve aspettare un parametro: extern void c_primitiva(natq a) {etc}
# Esercizi
due primitive:
- leggi: blocca programma chiamante che aspetta che qualcuno scriva
- scrivi: fa in modo che chiunque abbia chiamato la leggi, si svegli e ottenga l'argomento di scrivi
Per design prima viene chiamata la leggi poi la scrivi

Terza primitiva: pulisci
Se chiamo scrivi prima di leggi, leggi non è bloccante e leggi legge e basta.

Pulisci: se chiamo leggi dopo la scrivi si deve comunque bloccare, quindi deve annullare una eventuale scrivi.