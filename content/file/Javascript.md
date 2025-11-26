#uni 
**JavaScript** (**JS**) is a programming language ([[Linguaggio di Programmazione]]) and core technology of the Web, alongside [[HTML]] and [[CSS]]. It was created by Brendan Eich in 1995. Ninety-nine percent of websites use JavaScript on the client side for webpage behavior ([[Network Applications#2.1 Web and HTTP (2.2)]]).

Web browsers have a dedicated JavaScript engine that executes the client code. These engines are also utilized in some servers and a variety of apps. The most popular runtime system for non-browser usage is [[Node.js]].

JavaScript is a high-level, often just-in-time–compiled language that conforms to the ECMAScript standard. It has dynamic typing, prototype-based object-orientation, and first-class functions. It is **multi-paradigm**, supporting *event-driven, functional, and imperative programming styles*. It has application programming interfaces ([[API]]s) for working with text, dates, regular expressions, standard data structures, and the Document Object Model (DOM).

The ECMAScript standard does not include any input/output (I/O), such as networking, storage, or graphics facilities. In practice, the web browser or other runtime system provides JavaScript APIs for I/O.

Although [[Java]] and JavaScript are similar in name and syntax, the two languages are distinct and differ greatly in design.

"JavaScript" is a trademark of [[Oracle]] Corporation in the United States.[37][38] The trademark was originally issued to [[Sun Microsystems]] on 6 May 1997, and was transferred to Oracle when they acquired Sun in 2009.
# Libraries and Frameworks
Over 80% of websites use a third-party JavaScript library or web framework as part of their client-side scripting.

[[jQuery]] is by far the most-used. Other notable ones include [[Angular]], Bootstrap, [[Lodash]], [[Modernizr]], [[React]], [[Underscore]], and [[Vue]]. *Multiple options can be used in conjunction*, such as jQuery and Bootstrap.

However, the term "**Vanilla JS**" was coined for websites not using any libraries or frameworks at all, instead relying entirely on standard JavaScript functionality.
# Objects
## Primitive Types
JavaScript is **weakly typed**, which means certain types are implicitly cast depending on the operation used.

- The binary `+` operator casts both operands to a string unless both operands are numbers. This is because the addition operator doubles as a concatenation operator
- The binary - operator always casts both operands to a number
- Both unary operators (`+`, `-`) always cast the operand to a number. However, `+` always casts to Number (binary64) while `-` preserves `BigInt` (integer)

Values are cast to strings like the following:
- Strings are left as-is
- Numbers are converted to their string representation
- Arrays have their elements cast to strings after which they are joined by commas (`,`)
- Other objects are converted to the string `[object Object]` where `Object` is the name of the constructor of the object
Values are cast to numbers by casting to strings and then casting the strings to numbers. These processes can be modified by defining `toString` and `valueOf` functions on the prototype for string and number casting respectively.

<table class="wikitable">
<caption>JavaScript type conversions
</caption>
<tbody><tr>
<th>left operand
</th>
<th>operator
</th>
<th>right operand
</th>
<th>result
</th></tr>
<tr>
<td><code>[]</code> (empty array)
</td>
<td><code>+</code>
</td>
<td><code>[]</code> (empty array)
</td>
<td><code>""</code> (empty string)
</td></tr>
<tr>
<td><code>[]</code> (empty array)
</td>
<td><code>+</code>
</td>
<td><code>{}</code> (empty object)
</td>
<td><code>"[object Object]"</code> (string)
</td></tr>
<tr>
<td><code>false</code> (boolean)
</td>
<td><code>+</code>
</td>
<td><code>[]</code> (empty array)
</td>
<td><code>"false"</code> (string)
</td></tr>
<tr>
<td><code>"123"</code>(string)
</td>
<td><code>+</code>
</td>
<td><code>1</code> (number)
</td>
<td><code>"1231"</code> (string)
</td></tr>
<tr>
<td><code>"123"</code> (string)
</td>
<td><code>-</code>
</td>
<td><code>1</code> (number)
</td>
<td><code>122</code> (number)
</td></tr>
<tr>
<td><code>"123"</code> (string)
</td>
<td><code>-</code>
</td>
<td><code>"abc"</code> (string)
</td>
<td><code><a href="/wiki/NaN" title="NaN">NaN</a></code> (number)
</td></tr></tbody></table>
### Variable Types
- string
- number
- boolean
### Parsing
```javascript
var numero = parseInt(valore);
```
### Operators
- assignment operators
	- `+=`
	- `=`
	- `-=`
	- `*=`
	- `/=`
	- `%=`
	- `var++` `++var`
	- `var--` `--var`
- arithmetic operators
	- `+`
	- `-`
	- `*`
	- `/`
	- `%`
	- `**`
- comparison operators
	- 
- logical operators
### Array
```javascript
var vettore = [ "ciao" , "come" , "stai" ];
var vettoreDiVettori = [ ["hello" , "ciao" ] , ["prova" , "hello" ] , [ecc] ];
```
#### Array Destructuring
```javascript

var vettore = [ "ciao" , "come" , "stai" ];
// option 1
var elem1 = vettore[0];
var elem2 = vettore[1];
var elem3 = vettore[2];
// option 2
var [elem1, elem2, elem3] = vettore;
```
## Custom Objects
In javascript objects are a collection of **named values**, called **properties**.
**Object Literal Notation**:
```javascript
const objName = {
	name1 : value1,
	name2 : value2,
	... : ,
	nameN : valueN
};
```
another way is to use the **Object Constructor**:
```javascript
const objName = new object;
objName.name1 = value1;
ecc
```
Referencing this object's properties:
```Javascript
// option 1
let value = onjName.name1;
// option 2
let value = objName["name1"];
```
### Functions in objects
In a functional programming language like javascript, we say objects have properties that are functions (note the use of the keyword *this*):
```javascript
const objName : {
	name1 : value1,
	name2 : value2,
	name3: function() {
		return this.value1 * this.value2;
	}
}
```
### Function Constructors
```javascript
function constrF(name,address,city) {
	this.name = name;
	this.address = address;
	this.city = city;
}

const obj1 = new constrF("Aldo","Picadilly route","London");
```
### Objects in Objects
Objects can contain other objects and other content.
### Object Destructuring
```javascript
const objName = {
	name1 : value1,
	arr1 : ["val1" , "val2"],
	obj1 : {
		country: "canada",
		city: "calgary"
	}
};

// referencing:

let countryy = objName.obj1.country;
let val22 = objName.arr1[1];
// or
let {name1,arr1,obj1:{country,city}} = objName;
```
# Functions
Functions in javascript do not need a return type and can have a variable number of parameters.
```javascript
function funcName(parameters) {
	funcBody;
}

funcName(params);
```
example with a variable number of parameters (using the **rest** operator `...`):
```javascript
function func(...args) {
	for (let a of args) {
		//every iteration of this for loop has a different argument, in order
	}
}
```
## Arrow Syntax
```javascript
function (arg1) {
	// body
}
//can be written as:
(arg1) => {
	//body
}
```
## Callback Functions
Since functions in JavaScript are objects, they can be passed as arguments to other functions.
A callback function is a function that is passed to another function.
```javascript
function callBK() {
	//ecc
}

function func(paramF) {
	// ...
	let a = paramF();
	// ...
}

func(callBK);
```

When can even define a function definition directly inside the invocation:
```javascript
function func(argF) {
	// ...
}

func( function calc(){
	// callback function body
})
```
# Scope
Javascript has four scopes:
- function (local) scope
- block scope: variables defined using let or const inside `{}`
- module scope
- global scope: attention to namespace conflict problem: it the javascript compiler encounters another identifier with the same name at the same scope, there is no error, instead *the new identifier replaces the old one*!
# Hoisting
Declarations in javascript (of functions or objects) are *hoisted* to the beginning of the scope (computed at the beginning of the scope), although assignments are not.
# DOM
The **document object model** (**DOM**) is a bridge between JavaScript and the HTML document. The document gets presented to JavaScript as a tree, where each node is an element.

> add the `refer` attribute to the `<script src="ecc" defer></script>` tag, so that the JS gets executed after the loading of the web page.
 
```javascript
document.body.style.background = "blue";
document.body.innerText = "ciao";
document.body.innerHTML = "<h1>Hi everyone </h1>";
document.body.innerHTML = document.body.innerHTML + "<h1>Hi everyone </h1>";

document.body.style.backGroundColor = "lightblue";
```
# Event Driven
# Random
```javascript
alert("ciao");
console.log("ciao");
console.dir(document.body);
prompt("inserire numero","5"); // 5 è il default
```
# Errors
```javascript
try {
	nonexistentfunction("hello");
}
catch(err) {
	alert("An exception was caught: " + err);
}
```
# Including JS in HTML
```HTML
<script src="path/link" defer></script>
```