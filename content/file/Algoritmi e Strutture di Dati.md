#uni 
Antonio Virdis, 6 cfu, Virtual Box/UTM
[[Informazioni sul corso di Algoritmi e Strutture Dati]] 
[[Algoritmi]] 
[[Complessità]] 
[[Algoritmi di Ordinamento Array]]
[[Algoritmi di Ricerca Array]] 
[[Albero di Ricerca Binario]] 
pretest:
dijkstra [[Algoritmo di Dijkstra]] 
kruskal [[Algoritmo di Kruskal]]

random:
[[Torre di Hanoi]] 





comandi esame:
```bash
# compilare con standard C++03
g++ -std=c++03 -pedantic -Wall -Wextra -Werror main.cpp

./compilato ‹ inputo. txt | diff - outputo. txt
```
.vimrc
```.vimrc
set number
set relativenumber

syntax on
filetype plugin indent on

set autoindent
set smartindent
set cindent
set tabstop=4
set shiftwidth=4
set expandtab

set showmatch

set foldmethod=syntax
set foldlevel=99
# toggle fold with 'za'

set makeprg=g++\ -std=c++03\ -Wall\ -Wextra\ -pedantic\ %
# compile with ':make'
# passa agli errori con ':cnext' e ':cprev'

nnoremap R <Nop>
nnoremap gR <Nop>
```
comandi per vim utili:
```vim
yyp # duplica (sotto) la linea corrente
yyP # sopra
3yyp # duplica (sotto-sopra) 3 linee
```
.nanorc
```
set autoindent
set tabsize 4

set linenumbers
```