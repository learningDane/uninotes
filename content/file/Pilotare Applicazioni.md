#uni 
# STDIN, STDOUT e STDERR
STDIN, STDOUT e STDERR sono descrittori di default, vengono generati automaticamente al momento dell'esecuzione del programma e la loro apertura e chiusura viene gestita dal sistema operativo.
Possono essere acceduti con le seguenti macro, definite in `unistd.h`:
- STDIN_FILENO: macro che rappresenta il file descriptor di STDIN
- STDOUT_FILENO: macro che rappresenta il file descriptor di STDOUT
- STDERR_FILENO: macro che rappresenta il file descriptor di STDERR
# dup2
La funzione `dup2` permette di duplicare un file desceriptor:
```c
int dup2(int target, int newfd);
```
- `target` è il file descriptor da duplicare
- `newfd` è il file descriptor dove verrà messa la copia di `target`
- il ritorno è negativo se c'è stato errore
- la funzione *chiude il file descriptor `newfd`* (se precedentemente aperto) prima di duplicare il `target`.
## Redirezione degli standard file descriptors
Si possono combinare `pipe` e `dup2` per redirigere il flusso dei dati dagli standard IO verso altri file descriptors:
```c
int main() {
	int pipe_fd[2];
	pid_t pid;
	
	pipe(pipe_fd);
	pid = fork();
	
	if (pid == 0) {
		//figlio
		//chiudo estremità non usata
		close(pipe_fd[0]); // estremo per la lettura
		
		// redirigo lo stdout verso la pipe
		dup2(pipe_fd[1], STDOUT_FILENO);
		
		execl("/bin/ls","ls","-l",NULL);
	}
	
	if (pid > 0) {
		// padre
		char buffer[1024];
		int nread = -1;
		int index = 0;
		
		// chiudo estremità non usata
		close(pipe_fd[1]); // estremo per scrittura
		//approccio generale per la lettura
		while(nread != 0) {
			nread = read(pipe_fd[0], &buffer[index], sizeof(buffer)-1);
			buffer[index+nread] = '\0';
			index += nread;
		}
		printf("il padre ha letto: %s\n", buffer);
	}
	return 0;
}
```
# Redirezione di una applicazione
Esempio:
Ho una applicazione che non posso modificare, non ne posseggo il sorgente e non conosciamo il linguaggio usato.
Questa applicazione permette di inserire input da terminale (STDIN) e restituisce output su terminale (STDOUT).

Voglio "pilotare" questa applicazione con un programma in [[C]] che fa da intermediario tra me e l'applicazione:
- creo 2 pipe
- fork
- redirigo stdin e stdout del figlio
- trasformo il figlio nell'applicazione
- il padre pilota il figlio seguendo:
	- le mie esigenze
	- i vincoli dell'applicazione

```c
int FtS[2]; //father to son
int StF[2] //son to father
pid_t pid;

pipe(FtS);
pipe(StF);
pid = fork();
if (pid == 0) { // figlio
	close(FtS[1]); // chiudo scrittura padre->figlio
	close(StF[0]); // chiudo lettura figlio->padre
	
	//duplico FtS[0] e lo metto al posto di stdin e chiudo la copia extra
	dup2(FtS[0],STDIN_FILENO); // quello che manda il padre finisce in stdin
	close(FtS[0]);
	
	//duplico StF[1] e lo metto al posto di stdout e chiudo la copia extra
	dup2(StF[1], STDOUT_FILENO); // quello che l'applicazione manderebbe in stdout finisce al padre
	close(StF[1]);
	
	execl(<path_applicazione>,<nome_applicazione>,NULL);
}

else { //padre
	// un buffer per ricevere da terminale uno per inviare al figlio
	char sendbuffer[1024];
	char receivebuffer[1024];
	
	// intero per gestire il ritorno della read
	int nread;
	
	// chiudo le estremità non utilizzate
	close(FtS[0]); // chiudo lettura padre->figlio
	close(StF[1]); // chiudo la scrittura figlio->padre
	
	// preparo la stringa da mandare al figlio e la mando
	// \n è l'invio (ritorno carrello) ed è fondamentale
	sprintf(sendbuffer,"<formato stringa applicazione>\n");
	write(FtS[1],sendbuffer,strlen(sendbuffer));
	
	// ricevo la risposta dal figlio
	nread=read(StF[0], receivebuffer, sizeof(receivebuffer)-1);
	receivebuffer[nread]='\0';
	printf(receiverbuffer); // eventualmente manipolata
}
```