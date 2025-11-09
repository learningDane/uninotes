#uni 
Il processore ad ogni istante si trova o a livello di privilegio di **sistema**, o a livello **utente**, questa informazione è contenuta nel registro ___CS___ (code selector).

Per quanto riguarda la memoria, la parte ___M1___ è accessibile solo tramite livello di sistema, la parte ___M2___ invece anche dal livello utente, l'indirizzo limite che decide dove inizia M2 è scritto dal bootstrap in un registro del processore, e può essere solo cambiato dal sistema.

Il livello di privilegio può essere solo:
- innalzato (o lasciato inalterato) passando attraverso un ___gate della IDT___: istruzione `int $tipo` ($tipo compreso tra 0 e 255)
- abbassato (o lasciato inalterato) tramite l'istruzione ___IRETQ___.

Quando si prova ad eseguire una istruzione senza il privilegio necessario, il processore solleva una ___interruzione di Protezione___. L'utente non può quindi modificare il contenuto della IDT, poiché vorrebbe dire controllare la protezione, ciò viene realizzato *caricando la IDT in M1*, e rendendo privilegiata l'istruzione `lidtr` (che carica l'indirizzo della IDT nel registro **IDTR**).

Le routine eseguite tramite `int` prendono il nome di ___primitive di sistema___.
# Bootstrap
All'avvio il calcolatore si trova in modalità sistema e viene calcolato il **bootstrap loader** in memoria.
Questo si occupa di caricare le routine e le strutture dati del sistema all'inizio della memoria, infine scrive l'indirizzo limite (separatore M1/M2) in un registro del processore.

Finito il bootstrap, prepara una pila utente nello stato in cui l'avrebbe lasciata una interruzione proveniente da CS=utente, poi esegue una `iretq`.
# IDT
Ogni gate della IDT occupa 16 byte e contiene le seguenti informazioni:
- un ___bit P___ (presenza), che indica se il gate è rilevante
- ___puntatore___ alla routine a cui saltare (solo 8 byte poiché siamo all'inizio della memoria)
- un ___bit I/T___ che indica se il gate è di tipo Interrupt o Trap
- un ___campo L___ che indica il livello di privilegio a cui il processore si deve portare dopo aver passato il gate
- un ___campo DPL___ (descriptor privilege level) (o GL per gate level) che indica il _livello di privilegio necessario_ per poter attraversare il gate

Ci sono 3 modi per attraversare un gate della IDT:
1. Interruzione esterna
2. Eccezione
3. Interruzione Software (istruzione `INT`)
# Interruzioni Esterne
# Eccezioni
# Interruzioni Software
Sono del tutto analoghe alle interruzioni esterne e alle eccezioni di tipo trap.
In particolare queste salvano in pila l'indirizzo dell'istruzione successiva alla `int`, inoltre è sempre necessaria una `iretq`.

Le routine che vanno in esecuzione a seguito di una `int` prendono il nome di **primititve di sistema**.

`int` si comporta come una `call`, ma si rende necessario l'utilizzo di una nuova istruzione perché la call necessita di un preciso indirizzo a cui saltare, l'utente potrebbe saltare in mezzo ad una primitiva per saltare dei controllo per esempio. Inoltre se gli indirizzi vengono specificati in forma simbolica, il codice utente e il codice sistema necessiterebbero di essere collegati.
# Svolgimento di Una interruzione
Quando il processore accetta un'interruzione esterna o genera un'eccezione e esegue un'interruzione software esegue il seguente:
1. controlla il tipo dell'interruzione
	- se è una eccezione il tipo è implicito
	- se è interruzione esterna riceve il tipo dall'APIC
	- se è interruzione software il tipo è il parametro di `int` 
  usa il tipo come indice della IDT e accedere al corrispondente gate
2. se:
	- il bit P è zero, il processore genera un'eccezione per gate non presente (tipo 11)
	- se è una interruzione software (o una `int3`), se CS è inferiore di DPL genera una eccezione di protezione (tipo 13)
	- se L è inferiore di CS genera un'interruzione di protezione
	Se passa tutti i test salva in un registro ___SRSP___ di appoggio il contenuto corrente di %rsp
3. se CS è minore stretto di L esegue un cambio di pila, caricando un nuovo valore in %rsp
4. salva nella pila corrente (nuova se ha eseguito il cambio) 5 parole lunghe (8 byte), in questo ordine:
	1. una parola lunga rilevante per la segmentazione
	2. SRSP, che in caso di cambio di pila punta alla vecchia pila
	3. RFLAGS
	4. CS
	5. %rip (che si trova dunque in cima alla pila (LIFO))
5. azzera TF (disabilita una eventuale modalità single step), e azzera IF (interrupt flag) solo se il gate è di tipo Interrupt
6. salta all'indirizzo della routine puntata dal gate
# Svolgimento di IRETQ
1. se il livello di privilegio salvato in pila è superiore a CS genera una eccezione di protezione (`iretq` può solo abbassare il privilegio)
2. ripristina i valori di %rip, CS, RFLAGS e %rsp, prendendoli dalla pila in questo ordine
# Registro TR e Task State Segment (TSS)
>Strutture dati del sistema associate ad ogni processo:
>![[tss.svg]]

Il processore cambia Pila quando deve innalzare il livello di privilegio, il puntatore alla nuova pila è prelevato dal ___Task State Segment___ (o ___TSS___) corrente.

I TSS sono strutture dati in memoria M1 contenenti spazio per diverse informazioni, tra cui ==punt_nucleo==, il campo del TSS che contiene il puntatore alla pila di sistema.

In teoria ci dovrebbe essere un TSS per ogni processo, ma ad ogni istante solo uno è quello attivo, indicato dal registro ___%tr___ (task register), che può essere caricato attraverso l'istruzione `ltr`. 

Tutti i TSS sono descritti da una tabella ___GDT___ (global descriptor table), puntata dal registro ___%gtdr___, che può essere caricato attraverso l'istruzione `lgtdr`.
La GDT oltre a cose rilevanti per la segmentazione contiene una entrata per ogni TSS, contenente il suo indirizzo base (ovvero di partenza) e la sua grandezza in byte. 

Il registro %tr contiene l'offset dell'entrata corrispondente al TSS attuale.

>Attenzione, noi non useremo questa convenzione, invece avremo un unico TSS, caricando %tr una sola volta durante l'inizializzazione, del quale invece aggiorneremo il campo `punt_nucleo` ad ogni cambio di processo.
# Diritto di I/O in Intel
Nell'architettura intel la possibilità o meno di eseguire operazioni come disabilitazione delle interruzioni o utilizzo di I/O è determinata dal campo ___IOPL___ (I/O privilege level) (bit 13 e 12 di %F), che si trova nel registro dei flag ed indica il livello di privilegio minimo necessario per accedere a queste operazioni.

Il campo IOPL può essere ovviamente cambiato solamente a livello di sistema, il tentativo di modifica (tramite `popf`) da parte di un utente viene semplicemente ignorato e non genera eccezione (stessa cosa accade se si tenta di modificare il flag IF tramite `popf`).

> Perché? Penso che sia perché l'utente deve poter cambiare alcuni dei flag, quindi proteggere l'istruzione `popf` è fuori discussione, allora il processore si limita ad ignorare le modifiche fatte ai flag IOPL e IF dal livello utente