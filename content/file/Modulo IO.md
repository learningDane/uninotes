#uni 
La gestione delle interruzioni tramite il meccanismo dei driver, come abbiamo visto ([[IO nel nucleo]]), è poco flessibile ed efficiente, per due motivi:
- il driver deve essere eseguito ad interruzioni disabilitate poiché manipola le code dei processi. Questo porta a far aspettare anche interruzioni a più alta priorità.
- il driver non si può bloccare, in quanto non è un processo, il che è molto limitante in sistemi complicati che gestiscono rete e filesystem.

Risolviamo il secondo problema rendendo il driver un processo, inoltre facciamo in modo che l'interruzione non mandi in esecuzione il driver, ma un handler che si limita a sbloccare il processo driver.

Il primo problema invece va risolto con la disabilitazione delle interruzioni nei soli punti critici, ovvero nei punti in cui si manipolano strutture dati condivise, code dei processi eccetera.
Questa soluzione porta però a grandi complicazioni nel codice, allora invece rendiamo questo processo NON di livello sistema, per cui l'unico modo che ha per modificare strutture dati del livello sistema è tramite primitive.

Introduciamo allora il **modulo IO**, il cui scopo è realizzare le primitive per l'accesso alle periferiche, gestendo le richieste di interruzione tramite cosiddetti **processi esterni**, nel senso che sono esterni al modulo sistema anche se ne svolgono funzioni.

I file che contengono il codice di questo nuovo modulo sono caricati in IO/condivisa, e conterranno primitive e strutture dati riguardanti l'IO.

Il modulo IO quindi:
- gira a interruzioni abilitate
- gira con la CPU a livello sistema
- offre primitive invocabili dal livello utente
- usa primitive invocabili solo dal livello sistema, oltre che primitive invocabili dal livello utente

L'accesso a queste nuove primitive di IO sarà possibile anch'esso tramite istruzioni INT, ma le relative entrate nella IDT punteranno questa volta al modulo IO.
# Codice
sistema.cpp:
```c++
/*! @brief Tabella che associa ogni piedino dell'apic con il des_proc del relativo processo esterno
 *
 * Associazione IRQ -> processo esterno che lo gestisce
 */
des_proc* a_p[apic::MAX_IRQ];

/*! @brief Parte C++ della primitiva activate_pe().
 *
 * Attiva un processo esterno, primitiva chiamabile solo da livello sistema (modulo IO)
 * Mette questo descrittore nella corretta entrata della tabella a_p, invece che in coda
 * pronti
 *  @param f		corpo del processo
 *  @param a		parametro per il corpo del processo
 *  @param prio		priorità del processo
 *  @param liv		livello del processo (LIV_UTENTE o LIV_SISTEMA)
 *  @param irq		IRQ gestito dal processo
 */
extern "C" void c_activate_pe(void f(natq), natq a, natl prio, natl liv, natb irq);
```

La decisione di non associare inizialmente gli handler a entrate della IDT deriva dalla volontà di mantenere la priorità come assegnata dalla activate_pe: data la priorità dei processi esterni come `= MIN_EXT_PRIO + prio`, (dove `MIN_EXT_PRIO` è una costante e `prio` è la priorità passata alla activate_pe, numero naturale <256), la activate_pe programma l'apic in modo tale che il piedino `i` (`i` è il parametro `irq` passato alla funzione) manda il tipo `prio`, inoltre all'entrata `prio` della IDT installa il gate che punta a `handler_i`

sistema.s:
```c++ (asm)
# serve un handler_i per ogni piedino a cui vogliamo associare un processo esterno
handler_i:
	call salva_stato
	call inspronti // mette il proc attuale in testa a pronti (era sicuramente il proc a prio maggiore)
	/// Metto in esecuzione il processo esterno
	/// {
	movq a_p+$i*8, %rax
	movq %rax, esecuzione
	# equivale a esecuzione=a_p[i]
	/// }
	call carica_stato
	iretq



a_wfi:
	call salva_stato
	call apic_send_EOI
	call schedulatore
	call carica_stato
	iretq
```

io.cpp:
```c++
extern "C" void estern(natl i)
{
	des_io *d = &array_des_io[i]; // d è il puntatore al descrittore dell'interfaccia
	
	for (;;) {
		... // corpo processo esterno
		wfi(); // sospensione in attesa della prossima interruzione
	}
}
```

io.s:
```c++ (asm)
.global wfi
wfi:
	int $TIPO_WFI
	ret
```
## Esempio di primitiva di lettura
Codice del processo esterno:
```c++
// file: io.cpp
extern "C" void estern(natl id)
{
	des_io *d = &array_des_io[id];
	
	for (;;) {
		d->quanti--;
		if (d->quanti == 0)
			outputb(0, d->iCTL); // disabilito interrupt dispositivo, PRIMA di leggere byte
		char c = inputb(d->iRBR);
		*d->buf = c;
		d->buf++;
		if (d->quanti == 0) 
			sem_signal(d->sync); // DOPO aver trasferito il byte, poiché questo processo esterno non è atomico e la sem_signal potrebbe svegliare qualche altro processo
		wfi();
	}
}
```