#uni 
fino a cap 3.6.1
cap 3.7 : deadlock "blocco critico"


---
slide "Synchronization":
# Classical Problems of Synchronization
## Bounded-Buffer Problem
- $N$ buffers that can hold $1$ item
- semaphore `mutex` initialized to $1$
- semaphore `msg` initialized to $0$
- semaphore `buf` initialized to $N$

structure of the producer process:
```c++
do
{
	< produce an item in nextp >
	wait(buf); // there has to be space left in the buffer
		wait (mutex); // wait for nobody accessing the buffer
		< add item to the buffer >
		signal (mutex);
	signal(msg); // new message available!
} while (TRUE);
```

structure of the consumer process:
```c++
do 
{
	wait (msg); // wait for new message
		wait(mutex) // wait for nobody accessing the buffer to nextc
		< remove item from buffer >
		signal(mutex);
	signal(buf); // new space available in the buffer
	< consume the item in nextc >
} while (TRUE);
```
## Readers and Writers Problem
A data set in shared among a number of processes: writers and readers.
We want to allow multiple readers to read the data set concurrently, at the same time. Writers though must be mutually exclusive.
- data set
- semaphore `mutex` = 1, operated on `readcount`
- semaphore `wrt` = 1, regulating the writing on the data set
- integer `readcount` = 0

structure of writer process:
```c++
do
{
	wait(wrt);
	< writing >
	signal(wrt);
} while (TRUE);
```

structure of reader process:
```c++
do
{
	wait(mutex);
		readcount++;
		if (readcount == 1) wait {wrt}; // if there were no readers, there could be a writer, so we have to wait for wrt
	signal(mutex);
	
	< reading >
	
	wait (mutex);
		readcount--;
		if (readcount == 0) signal (wrt);
	signal(mutex);
} while (TRUE);
```
## Dining-Philosophers Problem
Il problema dei 5 filosofi:
Abbiamo una tavola rotonda, con al centro un piatto di riso. Attorno al tavolo sono seduti 5 filosofi, $\{P1,P2,P3,P4,P5\}$.
Questi filosofi pensano (thinking), e mentre pensano non hanno bisogno di mangiare.
Dopo aver pensato, un filosofo diventa affamato (hungry) e deve mangiare (eating).
Sul tavolo ci sono 5 bacchette (chopstick), disposte perpendicolarmente alla circonferenza ed equidistanti l'una dall'altra, $\{ C1,C2,C3,C4,C5\}$.

Quando un filosofo vuole mangiare, prende prima la bacchetta alla sua destra, poi quella alla sua sinistra, infine con entrambe le bacchette può mangiare.

Indichiamo il fatto che $Pi$ ha la bacchetta $Ci$ con una freccia orientata da $Ci$ a $Pi$.
Indichiamo il fatto che $Pi$ è bloccato in attesa di $Ci$ con una freccia orientata tra i due.

> Notiamo che è possibile ottenere un ciclo, questo vuol dire che è possibile il **deadlock**.

# Monitors
Monitors are high-level abstraction that provide a mechanism for process synchronization.
The monitor is an abstract data type, the internal variables are only accessible by code within the procedure.
==Only one process may be active within the monitor at a time==.
```c++
monitor monitorName 
{
	// declaration of shared variables
	procedure P1(..) {...}
	..
	procedure Pn(..) {...}
	
	initialization code (..) {...}
}
```

Given a condition $x$:
There are two possible operations on the variable $x$:
- `x.wait()` : a process that invokes this operation is suspended until a `x.signal()` is performed
- `x.signal()` : this resumes one of the processes (if any) that invoked `x.wait()`. If there are no processes in a waiting state, the `signal` has no effect on the variable.

If the process `P` invokes a `x.signal()`, with `Q` in `x.wait()` state: `Q` is resumed and `P` must wait, there are two possible options:
- **signal and wait**: `P` waits until `Q` leaves the monitor or waits for another condition
- **signal and continue**: `Q` waits until `P` leaves the monitor or waits for another condition
## Implementation of a Monitor using semaphores
### Signal and wait
## Resuming processes within a monitor
We introduce the **conditional-wait** construct of the form `x.wait(c)`, where `c` is the *priority number*.
If there are several processes queued on the condition `x`, and a `x.signal()` is executed, the process with the lowest priority number (so highest priority) is scheduled next.