#uni 
```c++
/**
 * Come ottenere la pila sistema di un processo e cosa vi è contenuto
 */
natq* pila = ptr_cast<natq>(trasforma(p->cr3, p->contesto[I_RSP]));
/*
rip            = pila[0];
cs             = pila[1];
flags          = pila[2];
%rsp           = pila[3];
*/

/**
 * @brief Parte C++ della primitiva access()
Primitiva utilizzata dal modulo I/O per controllare che i buffer passati dal livello utente siano accessibili dal livello utente (problema del Cavallo di Troia) e non possano causare page fault nel modulo I/O (bit P tutti a 1 e scrittura permessa quando necessario).
@param begin base dell’intervallo da controllare
@param dim dimensione dell’intervallo da controllare
@param writeable se true, l’intervallo deve essere anche scrivibile
@param shared se true, l’intevallo deve trovarsi in utente/condivisa
@return true se i vincoli sono rispettati, false altrimenti
 */
bool c_access(vaddr begin, natq dim, bool writeable);


/**
 * @brief Traduzione di un indirizzo virtuale in fisico.
La funzione percorre un TRIE in modo analogo a quanto la MMU fa in hardware, e restituisce la traduzione di un dato indirizzo virtuale (o zero se la traduzione è assente).
@param root_tab indirizzo fisico della tabella radice del TRIE
@param v indirizzo virtuale da tradurre
@return indirizzo fisico corrispondente, o zero se _v_ non è mappato
 */
paddr trasforma(paddr root_tab, vaddr v);


/**
 * @brief Abortisce il processo corrente.
Come terminate_p(), ma mostra lo stato del processo sul log.
 */
void c_abort_p(bool selfdump = true);


/**
 * @brief Converte da intero a puntatore a void.
L’intero deve poter essere contenuto in un puntatore (4 byte a 32 bit, 8 byte a 64 bit) In caso contrario la funzione chiama @ref fpanic().
@tparam From un tipo intero
@param v valore (di tipo _From_) da convertire
@return puntatore a void
 */
template <> static inline void *voidptr_cast<unsigned long>(unsigned long v);
// void* voidptr_cast(unsigned long v);
// typedef unsigned long vaddr


/**
 * @brief Converte da intero a puntatore non void.
L’intero deve essere allineato correttamente e deve poter essere contenuto in un puntatore (4 byte a 32 bit, 8 byte a 64 bit) In caso contrario la funzione chiama @ref fpanic().
@tparam To tipo degli oggetti puntati
@tparam From un tipo intero
@param v valore (di tipo _From_) da convertire
@return puntatore a _To_
 */
ptr_cast<typename To>(From v);


/**
 *@brief Invalida una entrata del TLB.
@param v indirizzo virtuale di cui invalidare la traduzione
 */
void invalida_entrata_TLB(vaddr v);


/**
 * @brief Verifica un id di semaforo
@param sem id da verificare
@return true se sem è l’id di un semaforo allocato; false altrimenti
 */
bool sem_valido(natl sem);

/// Processi

des_proc* des_p(natl id);

void schedulatore();

void inserimento_lista(des_proc* &p_lista, des_proc* p_elem);

des_proc* rimozione_lista(des_proc* &p_lista);

void inspronti();

/**
 * @brief Sospende il processo corrente.
@param n numero di intervalli di tempo (n cicli del timer)
 */
void delay(natl n);

/// Semafori

/*
 * @brief Crea un nuovo semaforo.
@param val numero di gettoni iniziali
@return id del nuovo semaforo, o 0xFFFFFFFF in caso di errore
 */
natl sem_ini(natl v)

/*
 * @brief Estrae un gettone da un semaforo.
@param sem id del semaforo.
 */
void sem_wait(natl sem)

/*
 * @brief Inserisce un gettone in un semaforo.
@param sem id del semaforo
eventualmente sblocca un processo in attesa
 */
void sem_signal(natl sem)

/// Memoria Virtuale

/**
 * @brief Lettura di cr2.
@return contenuto di cr2
 */
vaddr readCR2();

/*! @brief Estrae un frame dalla lista dei frame liberi.
 *  @return indirizzo fisico del frame estratto, o 0 se la lista è vuota
 */
paddr alloca_frame();

/*! @brief Restiuisce un frame alla lista dei frame liberi.
 *  @param f		indirizzo fisico del frame da restituire
 */
void rilascia_frame(paddr f);

/*! @brief Alloca un frame libero destinato a contenere una tabella.
 *
 *  Azzera tutta la tabella e il suo contatore di entrate di valide.
 *  @return indirizzo fisico della tabella
 */
paddr alloca_tab();

/*! @brief Dealloca un frame che contiene una tabella
 *
 *  @warning La funzione controlla che la tabella non contenga entrate
 *  valide e causa un errore fatale in caso contrario.
 *
 *  @param f 		indirizzo fisico della tabella
 */
void rilascia_tab(paddr f);

/*! @brief Incrementa il contatore delle entrate valide di una tabella
 *  @param f 		indirizzo fisico della tabella
 */
void inc_ref(paddr f);

/*! @brief Decrementa il contatore delle entrate valide di una tabella
 *  @param f 		indirizzo fisico della tabella
 */
void dec_ref(paddr f);

/*! @brief Legge il contatore delle entrate valide di una tabella
 *  @param f 		indirizzo fisico della tabella
 *  @return 		valore del contatore
 */
natl get_ref(paddr f)
{
	return vdf[f / DIM_PAGINA].nvalide;
}

/*! @brief Crea tutto il sottoalbero necessario a tradurre tutti gli
 *         indirizzi di un intervallo.
 *
 * L'intero intervallo non deve contenere traduzioni pre-esistenti.
 *
 * I bit RW e US che sono a 1 nel parametro _flags_ saranno settati anche in
 * tutti i descrittori rilevanti del sottoalbero. Se _flags_ contiene i bit PCD e/o PWT,
 * questi saranno settati solo sui descrittori foglia.
 *
 * Il parametro _getpaddr_ deve poter essere invocato come _getpaddr(v)_, dove _v_ è
 * un indirizzo virtuale. L'invocazione deve restituire l'indirizzo fisico che
 * si vuole far corrispondere a _v_, o zero in caso di errore.
 *
 * La funzione, per default, crea traduzioni con pagine di livello 1. Se
 * si vogliono usare pagine di livello superiore (da 2 a @ref MAX_PS_LVL) occorre
 * passare anche il parametro _ps_lvl_.
 *
 * @tparam T	tipo di _getpaddr_
 * @param tab	indirizzo fisico della radice del TRIE
 * @param begin	base dell'intervallo
 * @param end	limite dell'intervallo
 * @param flags	flag da settare
 * @param getpaddr funzione che deve restituire l'indirizzo fisico
 * 		   da associare ad ogni indirizzo virtuale.
 * @param ps_lvl livello delle traduzioni da creare
 * @return	il primo indirizzo non mappato (_end_ in caso di successo)
 */
template<typename T>
vaddr map(paddr tab, vaddr begin, vaddr end, natl flags, T& getpaddr, int ps_lvl = 1);

/*! @brief Elimina tutte le traduzioni di un intervallo.
 *
 * Rilascia automaticamente tutte le sottotabelle che diventano vuote dopo aver
 * eliminato le traduzioni. Per liberare le pagine vere e proprie, invece,
 * chiama la funzione _putpaddr()_ passandole l'indirizzo virtuale, l'indirizzo
 * fisico e il livello della pagina da eliminare.
 *
 * @tparam T	tipo di _putpaddr_
 * @param tab	indirizzo fisico della radice del TRIE
 * @param begin	base dell'intervallo
 * @param end	limite dell'intervallo
 * @param putpaddr funzione che verrà invocata per ogni traduzione eliminata
 */
template<typename T>
void unmap(paddr tab, vaddr begin, vaddr end, T& putpaddr);
```
---
```asm
# settaggio di un flag, resettaggio con andw e la negazione del numero del flag
pushf
orw $numerodelflag, (%rsp)
popf
```