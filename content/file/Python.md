#uni 
Python è un linguaggio ad alto livello, interpretato e dinamico, il cui obiettivo è facilitare la produzione di codice.

Dal 2020 è il linguaggio più utilizzato al mondo.

È il linguaggio perfetto per lo scripting.
# Filosofia
Quanto segue è lo **zen di Python**:
```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.[c]
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than right now.[d]
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea – let's do more of those!
```
# Generale

```bash
# per avviare la shell di interpretazione
python3

# per usare la shell con IN e OUT espliciti
ipython3
```
In python l'indentazione definisce lo scope delle variabili e delle funzioni, la PEP 8 dice che è meglio usare gli spazi per fare un tab (4 spazi).

Commenti con gli hashtag `#`.
# Oggetti
Ogni oggetto ha un tipo:
- scalare
- non-scalare
# Variabili
I nomi di variabili non possono partire con un numero.
Python è strongly-typed: devo specificare cambiare il tipo di una variabile.
Python è dynamically-typed: gli oggetti hanno un tipo, non le variabili.
Python è case-sensitive.
Everything is an object.
# Tipi
```python
type(x)
# restituisce il tipo di x
```
- numeri
	- interi
	- float
	- complessi
	- ottavi
	- decimali
- stringhe
- liste: `[]`
- dizionari
- tuple
- file
- set
# Scalari
- int
	- divisione intera si fa con `//`, solo `/` è divisione float
- float
- bool
- noneType
Elevamento a potenza: `**` 
## Stringhe
Delimitate da `''` o `""`.
Concatenazione con `+`.
Ripetizione con `*`.
Per escape usare `\`
# Booleani
`True` o `False` con lettera maiuscola.
Nottabili con `not`.
## Casting
```
tipo(x)
```
Restituisce la conversione di `x` in `tipo`.
## Assegnamento
Si fa con `=`.
## Comparison
`x==y` Controlla:
- se scalare controlla il valore
- se non-scalare controlla il valore tramite le chiavi `x` e `y`, ovvero controlla se puntano alla stessa memoria
# Sequenze
Collezioni ordinate, posizionali, le stringhe sono sequenze.
```python
len(x)
# restitusice la lunghezza della sequenza x
# da errore se x è scalare (da TypeError)

min(x)
max(x)
# su stringhe viene applicato l'ordine lessicografico

x[y]
# indicizzazione della sequenza x, indice y

# slicing:
y = x[a:b] # from element a to element b-1
y = x[a:-1]

# stride
y = [start:end:stride]

# Formattazione
name = 'mike'
age = 18
print('{} is {} years old'.format(name,age))

# f-strings
val = 'Geeks'
print(f'{val}for{val} is a portal fort{var}.')

# """ tripla virgolette
print(f""" ciao il mio nome è "davide", il tuo?""")
# può contenere anche INVIO (a capo)

# input
text = input("scrivi qualcosa...")
```
# Liste
Le liste sono sequenze di elementi di tipo diverso
```python
>>> 1 = [1, 3, "aka", 19]
>>> 1
[1, 3, "aka", 19]

# posso fare slicing ecc

x = [1, 2, 3]
y = [7, x.copy(), 5]
# copia x e mette la reference alla copia in y, così se modifico x y non viene cambiato

# concatenazione
x = [1, 2, 3]
y = [1, 2, 3]
z = x + y
# crea una nuova lista che contiene una copia degli elementi 

list.append(obj)
list.count(obj)
list.extend(seq)
list.index(obj)
list.pop..
list.remove(obj)
list.reverse()
list.sort([func])
```
### ZIP
La zip() prende iterables e ritorna un iteratore di tuple, facendo packing dell'i-esimo elemento di ogni iterable
```python
numbers = [1,2,3]
letters = ['a','b','c']
z = zip(letters, numbers)

for i in z:
	print('i: {}, number: {}, letter: {}'.format(i,i[0],i[1]))
	
for i,j in z:
	print(number: {}, letter: {}'.format(i,j))
```
Se un iterable è più corto, si tagliano tutti alla sua lunghezza
# Mutability vs Immutability
Le stringhe sono immutabili, le liste sono mutabili.
# Flow Control
```python
# mutuamente esclusivi valutati in ordine
if a > b:
	ecc
elif c > d:
	ecc
else:
	ecc

lista = [1, 2, 3]
for i in lista:
	print(i) # stampa elemento NON INDICE

# range
range(end) # parte da 0
range(start, end)
range(stard, end, step)
for i in range(1,7,2):
	print(i) # stampa indice
```
## Iterables
Tutto quello che può essere usato con for loops è un **iterable**.
Iterables possono non essere indicizzabili, potrebbero non avere una lunghezza e potrebbero non essere nemmeno finiti.

Un oggetto iterable può essere passato a `iter()`.
```python
>>> r = range(4)
>>> iteratore = iter(r)
>>> next(interator)
0
>>> next(iterator)
1
ecc

# tramutare un iterable in lista
lista = list(iteratore)
```

enumerate:
```python
for i, r in enumerate(range(3,10)):
	print('a indice {} ho {}'.format(i,r))
```
## Controllo
```python
while i < 10:
	ecc
	if i == 5:
		break
	if i == 3:
		continue
	# else
	ecc
```
# List Comprehensions
```python
r1 = [1, 3, 5, 9]
r2 = [1, 3, 5, 9]
r3 = [1, 3, 5, 9]

m = [r1, r2, r3]

i = 0 # parto dalla prima colonna
i = [r[0] for r in m]

output = [(number-1) for number in reference if ...]
output = [c for i, c in enumerate(string) if i %2 == 0]
```
# Tuple
Le tuple sono un tipo immutabile, sono come liste ma immutabili.
```python
# 'packing'
tupla = ('a', 3, 5)
tupla = 'a', 3, 5
>>>type(tupla)
<class 'tuple'>

# 'unpacking'
>>>(a,b,c) = tupla
>>>print(b)
3
```
Ci posso eseguire su le stesse operazioni che posso fare su liste, purché siano immutabili.