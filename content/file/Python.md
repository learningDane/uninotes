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

>>>tupla = (1,2,3,4,5)
a,b,*c = tupla
print(c) = (3,4,5)
```
Ci posso eseguire su le stesse operazioni che posso fare su liste, purché siano immutabili.
# Set (insiemi)
Gli insiemi sono strutture dati che contengono oggetti immutabili, senza ripetizione e senza ordine.
Gli insiemi sono iterabili, ma in ordine casuale.
Gli insiemi sono hashable, poiché sotto c'è una mappa hash.
```python
a = {1,2,'b',4.3}
>>>type(a)
<class 'set'>
>>>print(a)
{'b',1,2,4.3}

>>>a[0]
Traceback (most recente call last):
	File ...
	a[0]
TypeError: 'set' objects does not support indexing
```

operazioni:
```python
s1.union(s2)
s1.intersection(s2)
s1.difference(s2)
s1.symmetric_difference(s2) # equivale a (s1 UNITO s2) SOTTRATTO (S1 INTERSEZIONE S2)
A|B # union
A|=B # update
A&B # intersezione
A<=B # A.issubset(B)
A>=B # A.issuperset(B)
```

Comprehension su insiemi:
```python
>>>{s for s in [1,2,1,0]}
set([0,1,2])

>>>{(m,n) for n in range(2) for m in range(3,5)}
set([(3,0),(3,1),(4,0),(4,1)])
```

Castando a SET rimuovo i duplicati. Non posso castare a SET oggetti che contengono elementi mutabili (liste).
# Dizionari
I dizionari sono una estensione dei set dove per ogni elemento di un set viene associato un valore: {chiave, valore}.
```python
'key':value
d = {'a':12, 'c':7, ecc}
>>>type(d)
<class 'dict'>
>>>print(d['c'])
7

# se indicizzo un elemento che non esiste, da errore
```
I dizionari sono anche detti **array associativi**.

Le chiavi devono essere uniche, i valori no.
```python
d.get('a')
12

# se l'elemento non esiste (la chiave non ha valore associato), get() restituisce None

# è possibile istituire un valore di default:
# Using get() with a default value for non-existing key:
print(d.get('b',"non disponibile"))

d.keys()
# Restituisce tutte le chiavi disponibili
# Da python 3.7 le chiavi sono in ordine di creazione
# dict_keys()

d.values()
# restitusice tutti i valori (anche duplicati)
# dict_values()

d.items()
# crea una lista di tuple <chiave,valore>
# dict.items()

d.pop('key')
# restituisce il valore associato alla chiave, e rimuove <chiave,valore> dal dizionario
```

Comprehension sui dizionari:
```python
>>>{k: v for k,v in [(1,2),(3,4)]}
{1: 2, 3:4}
```
# File
```python
f = open("file_name", mode) # 'w' 'r' 'a' 'x' 't' 'b' '+'
f.write("ciao")
f.close()

f = open ("filename", 'r')
contenuto = f.read()
conte = f.readlines()
for line in conte:
	print(line)
f.close()

# questo permette di non fare chiusura
# chiusura automatica alla fine del blocco:
with open(..) as f:
	content = f.readlines()
	...
# f è stato chiuso qua
# chiama automaticamente __exit__() alla fine del blocco
```
# Funzioni
Ci sono due tipi di funzioni:
- built-in
- user defined
Le funzioni sono trattate come oggetti, possono essere assegnate ad oggetti, contenute in collezioni (come liste) e passate come argomenti ad altre funzioni.

```python
def funzione(param1,params..):
	corpo..
	return valore
```

Le variabili definite in una funzione sono dette variabili locali e appartengono alla funzione stessa.

> In python tutti i passaggi di funzione sono fatti per reference.

## Argomenti
- argomenti posizionali: TUTTI gli argomenti vanno passati alla funzione in ordine
- argomenti keyword: va esplicita l'associazione nome argomento=argomento: `funzione(param1=..., param2=...)`
- argomenti di default: `def sum(param1=0, param2=0):...`
- argomenti a lunghezza variabile: questi parametri devono essere passati dopo gli argomenti posizionali e sono packed in tupla, la tupla contenente questi argomenti può essere acceduta con `*nomeargomento`: `def funzione(*param):...` 
- gli argomenti per nome vanno messi dopo quelli per posizione

per passare un dizionario:
```python
def funzione(**diz):...

# oppure

def funzione(fargs, *args, **kwargs)
```
## Ricorsione
Una funzione può chiamare se stessa.
## Docstrings (PEP 257)
```python
def funzione():
	"""
	descrizione
	"""
	...
	return ..

# access docstring
print(funzione.__doc__)
help(funzione)
```
## Funzioni Anonime (LAMBDA)
Sono funzioni definite senza nome:
```python
lambda arg1,arg2: expression

>>>times_two = lambda x: x*2
>>>print(times_two(4))
8


def times_n(n):
	return lambda a : a*n
```
devono essere una sola riga.
### map()
Map prende come argomento una funzione e una lista di argomenti, poi applica la funzioni a tutti gli argomenti:
```python
lista = [1,5,4,6,8,11,3,12]
nuova_lista = list(map(lambda x: x*2, lista))
```
### filter()
Filter() prende come argomento una funzione e una lista di argomenti. Applica la funzione a tutti gli elementi: restituisce una nuova lista contente solo gli elementi per la quale la funzione restituisce `True`:
```python
lista = [1,5,4,6,8,11,3,12]
nuova_lista = list(filter(lambda x: (x%2==0), lista))
```
### any()
Questa funzione ritorna True se almeno uno degli elementi in un iterable è True. Se è vuoto ritorna false.
```python
nums = [2, 5, 8, 12, 7]
print(any(num>10 for num in nums)) # stampa True
```
# Modules
Un modulo è un file contenente codice python con definizioni di funzioni, classi e variabili.
```python
import nome_modulo
nome_modulo.nome_funzione()
```
Python cerca i moduli in `PYTHONPATH` e nella cartella corrente.
```python
dir(module_name)
# da una lista python di tutti gli oggetti in un modulo
```
Altri modi per importare roba:
```python
from nome_modulo import nome_funzione
nome_funzione() # non serve nome_modulo.nome_funzione()


from nome_modulo import *
# stessa cosa ma importa tutte le funzioni

import nome_modulo as m
m.funzione()
```

Se cambi un modulo e lo vuoi reimportare nel codice usa `reload(nome_modulo)`.
# Package
Invece di avare moduli in file singoli possiamo avere cartelle, dette `package`:
```python
import package_name.module_name
package_name.module_name.function_name()

import package_name.module_name as m
m.function_name()
```

Per segnare un package ci mettiamo dentro un file `__init__.py`, qui dentro possiamo metterci per esempio variabili a livello di package.
```python
# my_package/__init__.py
print("initializing my_package")
__all__ = ["module1"]


# altro file
import my_package 
# oppure
from my_package import *
# entrambi stampano ed importano solo module1
```

```python
# __init__.py
from .module1 import *
__all__ = ["public_func"]
# oppure
from .module1 import public_func

# mypackage/module1.py
def public_func():
	...
def _private_func():
	...

```
# Librerie
Praticamente collezioni di moduli.
## Libreria Standard
### os
```python
os.getcwd() # return current working directory
os.chdir("/aesfasfe/asefaefs) # cambia cwd
```
### shutil
```python
shutil.copyfile("asfasef","asfe")
shutil.move("asefasef","asf")
```
### glob
```python
>>>glob.glob("*.py")
['myfile.py', 'script.py', 'exercise.py']
```
### math
```python
math.cos(math.pi/4)
math.log(1024,2)
```
### random
```python
random.choice(['ss','ss','ss'..])
random.sample(range(100),10) # sampling without replacenemt
# sceglie 10 valori
random.random() # random float
random.randrange(6) #random int from range(6)
```
### statistics
```python
statistics.mean(data)
mediam
variance
```
### time
```python
t = time.time()
print('{} seconds'.format(time.time()-t))
```
### sys
```python
sys.exit()
```
## PyPI
Python package index serve ad installare librerie extra, si usa il comando `pip`.
```bash
python -m pip install package_name
# oppure
pip install package_name

# questi prendono l'ultima versione compatibile con la vostra versione di python installata
```
# Eccezioni
Le eccezioni sono oggetti che rappresentano errori, questi oggetti se non `handled`, causano la terminazione dell'errore con un traceback message.
```python
try:
	# codice che può causare errore
except nomeEccezione1:
	# gestione
except nomeEccezione2 as e:
	print(f"Error details: {e}")
	# gestione
except nomeEccezione3 as b:
	if ..:
		raise ValureError("blah") from b
except nomeEccezione4:
	try:
		...
	except ValueError as c:
		# e.__context__ contiene nomeEccezione4
		print(f"Caused during handling of: {e.__context__}")
except errore:
	pass
else:
	# questo va solo se non ci sono eccezioni
finally:
	# questo va sempre
# normale codice


def funzioe():
	...
	if ...:
		raise xxxError("errore")
```
## Eccezioni più comuni
```python
IndexError
KeyError
TypeError
ValueError
FileNotFoundError
```
# Oggetti
In python tutto è un oggetto e ha un tipo, gli oggetti possono essere creati, manipolati e distrutti (con `del`).
Il **garbage collector** tiene traccia delle reference fatte ad un oggetto e lo distrugge se non serve più.

Possono essere definiti nuovi tipi di oggetto tramite `Class`:
```python
Class Cat:
	def __init__(self,name):
		self.name = name
	def meow(self):
		print("meow")

mycat = Cat("bob")
mycat.meow()


print(dir(Cat)) # stampa tutti gli attributi e metodi di un oggetto
```
# Classi
PEP8 per le classi è PascalCase.

È possible definire un attributo di una classe come **privato**: può essere acceduto e modificato solo da dentro la classe.

Quando un attributo è privato dobbiamo definire delle funzioni per interagirci:
- una funzione **getter** è usata per prendere il valore da un certo campo
- una funzione **setter** è usata per cambiare il valore di un certo campo
```python
class Cat:
	def __ini__(self,name,color):
		self.public_name = name
		self.__private_name = name
		self.color = color
	
	print(bob.__private_name)
	# da errore "non esiste attributo"
```
## Ereditarietà - Inheritance
Una classe esistente può essere riusata. Parent-children.
Child Class = subclass.
Parent Class = superclass.
```python
class Animal:
	def __init__(self, name, color):
		self.name - name
		self.color = color
	...
	
class Cat(Animal):
	def __init__(sex):
		super().__init__(name,color)
		self.sex = sex
	...
```
### funzioni built-in
```python
isinstance(obj, __class__)
# vero solo se obj.__class__ è int o qualche class derivata da int

issubclass(__class__, __class__)
# 
```
### Multiple inheritance
```python
class Derivata(classe1,classe2..):
	...
```
## Custom Exceptions
```python
class NetworkError(Exception):
	""Eccezione per errori di rete""
	pass
	
class DatabaseError(Exception):
	def __init__(self, message, error_code):
		self.message = message
		self.errpr_code = error_code
		super().__init__(f"Error{error_code}:{message}")
		
try:
	raise DatabaseError("Connection timeout",4004)
except DatabaseError as e:
	...
```
# Scope e namespace
scope:
- `local`
- `nonlocal`: quello precedente alla funzione
- `global`
# Operator Overloading
```python
class Cat:
	def __add__(self, other_cat):
		print("a cat is born!")
		...
		
	def __repr__(self):
		...
```
# Type Hints
Servono per specificare il tipo di variabile aspettato.
Non influiscono sul comportamento a runtime, servono per:
- better code documentation
- enhanced IDE support
- static type checking with tools like mypy
- improved code maintainability
```python
# vuole una stringa e restituisce una stringa
def greeting(name: str) -> str:
```

Ci sono:
- int
- float
- bool
- str
- bytes
- None

```python
# 3.10+
number: list[int]
user_info: dict[str,str]
coordinates: tuple[float,float]
record: tuple[str, int, float]
unique_ids: set[int]

# 3.9
from typing import List, Dict, Tuple, Set
numbers: List[int]
ecc
```
## Union types
```python
from typing import Union, Optional
user_id: Union[int,str]

result: Optional[str]=get_result()

# 3.12+
int | str |range
# equivale a Union[int,str,range]
int | None
```
## Type Aliases
```python
# 3.10+
Url = str
def retry(url: Url, retry_count: int) -> None:
	...
	
from typing import TypeAlias
Url: TypeAlias = str
...

from typing import Dict, List, Tuple, Union, TypeAlias
JSON = Union[Dictr[str, "JSON"], List["JSON"], str, int, float, bool, None]
```
## Match-case statement
```python
# 3.12+
def process_data(data: int | str | list):
	match data:
		case int():
			return data+1
		case str():
			...
```
## Callable types
```python
from typing import Callable
OperationFunc = Callable[[int, int], float]

def apply_operation(x: int, y: int, operation: OperationFunc) -> float:
	return operationFunc(x,y)
```
## Generic Types
```python
from typing import TypeVar, Generic, List
T = TypeVar('T') 
class Stack(Generic[T]):
	def __init__(self) -> None:
		self.items: List[T] = []
	
	def push(self, item: T) -> None:
		self.items.append(item)
```
# Decorators
Sono una funzione in grado di manipolare altre funzioni, tipo wrapper
```python
def greet():
	return "Hello!"

def uppercase_decorator(func):
	def wrapper():
		original_result = func()
		modified_result: original_result.upper()
		return modified_result
	return wrapper

# applicazione manuale del decorator
greet = uppercase_decorator(greet)
```
Un decorate può essere applicato usato `@`:
```python
def uppercase_decorator(func):
	def wrapper():
		original_result = func()
		modified_result: original_result.upper()
		return modified_result
	return wrapper
	
@uppercase_decorator
def greet():
	return "Hello!"
```

Decoratori per funzioni con argomenti:
```python
def uppercase_decorator(func):
	def wrapper(*args, **kwargs):
		original_result = func(*args, **kwargs)
		return original_result.upper()
	return wrapper
	
@uppercase_decorator
def greet(name):
	return f"Hello, {name}!"
	
print(greet("Alice"))
```

## Preservare i metadati
Quando applichi un decoratore si perdono i metadati originali e si applicano quelli del decoratore.

Per preservarli:
```python
import functools

def uppercase_decorator(func):
	@functools.wraps(func) # preserva i metadati
	def wrapper(*args, **kwargs):
		...
```
## Parametri per decoratori
```python
def repeat(n=1):
	def decorator(func):
		@functools.wraps(func)
		def wrapper(...):
			result = None
			for _ in range(n):
				result = func(*args,
			return result
		return wrapper
	return decorator

	
@repeat(n=3)
def say_hello():
	print("Hello!")
	return "done"
```
## Decoratori per classi
```python
def add_greeting(cls): # oggetto Classe, non oggetto istanza
	cls.greet = lambda self: f"Hello, I'm {self.name}"
	return cls

@add_greeting
class Person:
	def __init__(self, name):
		self.name = name

p = Person("Alice")
print(p.greet()) # Output: Hello, I'm Alice
```
## Class-based decorators
I decoratori possono essere implementati come classi con il metodo `__call__`
```python
class CountCalls:
	def __init__(self, func):
	functools.update_wrapper(self, func)
	self.func = func
	self.num_calls = 0

	def __call__(self, *args,**kwargs):
		self.num_calls += 1
		print(f"Call {self.num_calls} of {self.func.__name__!r}")
		return self.func(*args,**kwargs)

@CountCalls
def say_hi():
	print("Hi!")

say_hi() # Output: Call 1 of 'say_hi'
	# Hi!

say_hi() # Output: Call 2 of 'say_hi'
	# Hi!
```
## Decoratori built-in
- @property: converte un metodo in una proprietà
	- @nomefunz.setter
	- @nomefunz.deleter
- @classmethod: crea un metodo che riceve la class come primo argomento, e si lega alla classe, non all'istanza
	- utile per i Singleton e le Factory
- @staticmethod: crea un metodo che non riceve il primo argomento implicito: non accede a self o a class
- @abstractmethod: indica un metodo astratto in un classi astratte
# Iterators
Un iterator è un oggetto che rappresenta uno stream di dati, usato per accedere agli elementi dello stream uno alla volta.
```python
# Manual iteration using iterators
my_list = [1, 2, 3]

# Get iterator from the iterable
iterator = iter(my_list)

# Get elements one by one
print(next(iterator)) # Output: 1
print(next(iterator)) # Output: 2
print(next(iterator)) # Output: 3

# StopIteration exception is raised when no more items
try:
	print(next(iterator))
except StopIteration:
	print("No more elements!")
```
## Iterator Protocol
Gli oggetti che implementano il protocollo iteratore devono avere:
- `__iter__()` ritorna l'oggetto iteratore stesso
- `__next__()` ritorna il prossimo item oppure fa eccezione `StopIteration` se non ci sono altri item
```python
class CountUp:
	def __init__(self, start, stop):
		self.current = start
		self.stop = stop

def __iter__(self):
	return self

def __next__(self):
	if self.current > self.stop:
		raise StopIteration
	else:
		self.current += 1
		return self.current - 1

# Using the iterator
for num in CountUp(1, 5):
	print(num) # Output: 1, 2, 3, 4, 5
```
## Creazione di iteratori custom
Un iterable non deve essere per forza un iteratore, ma `__iter__()` deve restituirne l'iteratore.
```python
class EvenNumbers:
	def __init__(self, max_num):
		self.max_num = max_num
	def __iter__(self):
		return EvenNumbersIterator(self.max_num)

class EvenNumbersIterator:
	def __init__(self, max_num):
		self.current = 0
		self.max_num = max_num
	def __iter__(self):
		return self
	def __next__(self):
		if self.current > self.max_num:
			raise StopIteration
		else:
			self.current += 2
			return self.current - 2

# Using the iterable
for num in EvenNumbers(10):
print(num) # Output: 0, 2, 4, 6, 8, 10
```
## Generators
I generatori offrono un modo facile di creare iteratori senza implementare tutto il protocollo iteratore.
Usano il `yield` statement per ritornare i valori uno alla volta: come return ma salva lo stato attuale (serve per `next`).
```python
# Generator function
def count_up(start, stop):
	current = start
	while current <= stop:
		yield current
		current += 1

# Using the generator
for num in count_up(1, 5):
	print(num) # Output: 1, 2, 3, 4, 5

# Creating a list from a generator
numbers = list(count_up(1, 5)) # [1, 2, 3, 4, 5]
```