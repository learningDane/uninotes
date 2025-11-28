#uni 
CSS (*Cascading Style Sheet*)
```CSS
selector {
	attribute: value;
	otherAttribute: value
}
```
# Selectors
```css
tag
.class 
tag.class
#id
Selector, Selector (Or)
Selector  Selector  (Descendant) /* every descendant */
Selector > Selector  (Child) /* only the child */
Selector + Selector (Next to) /* every thing right after the other one */
Selector ~ Selector (Subsequent sibling) /* every thing after the other one */
selector:action
* /* means everything*/
```
## Select By Attribute
```css
[attribute]  /* elemento con attributo di nome attribute [attribute = value] elemento con attributo di nome attribute con un valore esattamente uguale a value */
[attribute $= value]  /* elemento con attributo di nome attribute con un valore che termina con value */
[attribute ^= value]  /* elemento con attributo di nome attribute con un valore che comincia con value */
[attribute ~= value]  /* elemento con attributo di nome attribute con un valore che che contiene  la parola value */
[attribute *= value]  /* elemento con attributo di nome attribute con un valore che contiene la sottostringa value */
```
## Pseudo Classes
```CSS
Selector:hover
Selector:active
Selector:visited
Selector:link
Selector:checked
```
### Pseudo Classes for Tables and Lists
```CSS
selector:nth-child(n) /* seleziona l’ennesimo figlio, indipendentemente dal tipo */
selectr:nth-of-type(n) /* indica l’ennesimo elemento dello stesso tipo */
/*
n può essere un numero, una formula o una keyword 
   Esempi: 3n+1, odd, even, 5, ...
Il primo elemento ha indice 1, n parte da 0
*/
```
# Attributes
```css
background-
	color: colorName
	image: url("ilLink")
	position: right top

opacity: 0.4

margin-
	left: 20px/50%(della pagina?);
	top: ... ;
	bottom: ... ;
margin: 50px 50px 50px 50px; /* top right bottom left */
margin: 50px; /* every margin is 50px */

border-
	style: solid
	style: dotted solid dotted solid; /* top right bottom left */
	width: 10px/medium/thick;
	width: 10px 5px 10px 5px; /* top right bottom left */
	width: 10px 5px; /* top-bottom right-left */
	color: colorName;
	top-style: ecc ;
	bottom: SIZE STYLE COLOR;
	bottom: 10px dashed purple;
	radius: 20px;

padding-
	top: 40px;
padding: 12px 123px 12px 32px;

height: 100px
width: 100px/100%

outline-
	style: solid/dashed/ecc; /* outline is outside the border */
	offset: 10px /* offset between border and outline */

display: none; /* non c'è */
visibility: hidden; /* c'è ma non si vede */
```
## Text
Alignment is an attribute:
```css
text-align: right/center/left(default)
text-alignment: justify /* makes every line of the same width */
text-justify: inter-word/inter-character/none
text-align-last: center; /* aligns only the last line to the center */
vertical-align: center;

text-decoration-line: underline/line-through/overline;
text-decoration-line: overline underline;
text-decoration-color: colore;
text-decoration-style: stile;
text-decoration-thickness: 10px;
text-decoration: overline purple style 6px;
text-decoration: none;

text-transform: lowercase/uppercase/capitalize;

text-indent: 30px;
text-line-height: 150%;

letter-spacing: 30px;
```
### Font
```css
font-family: Arial, Helvetica, sans-serif
font-family: "Lucida Console" , "Courier New" , monospace;

font-style: italic/oblique/normal;

font-weight: bold/normal;

font-size: 15px;
font-size: 1em; /* 1em = 16px , but depends on parent font size*/
```
# Tables
```html
<table>
	<tr>
		<th> Name </th>
		<th> Age </th>
	</tr>
	<tr>
		<td> John </td>
		<td> 44 </td>
	</tr>
	<tr>
		<td> Tim </td>
		<td> 12 </td>
	</tr>
</table>
```
:
```css
table, th, td {
	border: 2px solid;
	width: 100%;
	border-collapse; /* collapses the double lines */
}

th {
	height: 50px
}

td {
	text-align: center;
}

th, td {
	padding: 10px;
}

tr:hover {
	background-color: blue;
}
```
# Drop down menu
```html
<button class="dropwdown-menu"> Dropdown </button>
<div class="dropdown-menu">
	<a href="#">List</a>
	<a href="#">List</a>
	<a href="#">List</a>
	<a href="#">List</a>
</div>
```
:
```css
button.dropdown-menu {
	background-color: blue;
	text: white 16px;
	padding: 13px;
	border: none;
	cursor: pointer;
}

a.dropdown-menu {
	display=none;
	position: absolute;
	background-color: lightblue;
	min-width: 150px;
	padding: 11px 15px;
	text-decoration: none;
	display: block;
}

a.dropdown-menu:hover {
	background-color: white;
}

a.dropdown-menu:hover {
	display: block;
}
```
# Values
```html
<b>
	<p>
		ciao
	</p>
</b>
```
:
```css
b {
	margin-top: 50px
}

p {
	margin-top: inherit /* takes the value of the parent */
}
```
## Color
```css
colorname:
	red
	...
hex:
	#xxxxxx
```
## Style
```css
dashed
solid
dotted
groove
double
ridge
outset
inset
none
hidden /* present but hidden */
```
# Animations
The `animation` property applies an animation between styles.
```css
button{ 
	transition: 150ms ease;
}
button:hover {
	scale:2;
}
```
## Animation with Keyframes
```css
.element{
	animation-duration: 3s;
	animation-name: spin;
	animation-timing-function: ease-in-out;
	animation-delay: 1s;
	animation-iteration-count: infinite;
	animation-direction: reverse/alternate/normal;
	animation-fill-mode: forwards;
	animation-play-state: running;
}
.element:hover{
	animation-play-state: pause;
}
@keyframes spin{
	0%{
	
	}
	50%{
		scale: 2;
	}
	100%{
		transform: rotate(360deg);
		border-radius: 50%
	}
}
```
# CSS Animation examples
## Loading animation
```css
<!DOCTYPE html>
<head>
    <title>loading</title>
    <style>
        body {
            background-color: black;
        }
        .animation {
            height: 100px;
            width: 100px;
            border: solid red 6px;

            position:absolute;
            top: 50%;
            left: 50%;
            translate: -50% -50%;
            box-shadow: 0 0 16px red, 0 0 16px red inset;
            z-index: 10;
            animation: rotation 2.5s ease infinite;
        }
        @keyframes rotation{
            0%{
                transform: rotateX(0) rotateY(0) rotateZ(0);
            }
            33%{
                transform: rotateX(180deg) rotateY(0) rotateZ(0);
            }
            67%{
                transform: rotateX(180deg) rotateY(180deg) rotateZ(0);
            }
            100%{
                transform: rotateX(180deg) rotateY(180deg) rotateZ(180deg);
            }
        }
    </style>
</head>
<body>
    <div class="animation"></div>
</body>
```
# Flexbox
Every element that can include other elements can be a flexbox
```html
<body>
	<div>1</div>
	<div>1</div>
</body>
```

```css
body {
	display: flex;
	justify-content: flex-start / flex-end / center / space-between / space-around / stretch / spcae-evenly; /* x axis */
	align-items: flex-start / flex-end / center / space-between / space-around / stretch; /* y axis */
	flex-direction: row / row-reverse / column / column-reverse;
	flex-wrap: wrap / nowrap;
}

div {
	flex-basis: auto / 200px;
	flex-grow: 2;
	flex-shrink: 2; /* by what factor grow or shrink relative to other items*/
}
```
# Grid
```css
.container {
	display: grid;
	gap: 10px; /* gap between items */
	grid-template-columns: 1fr 1fr 1fr; /* every column is one equal fraction */
	grid-template-rows: 80px auto 50px / 10% 40% 50%;
	grid-template-rows: repeat(3, 1fr);
	grid-template-rows: repeat(4, 20px 50px) 60px;
	grid-template-columns: repeat(auto-fill , minmax(40px, 1fr));
	grid-template-columns: repeat(auto-fit , minmax(40px, 1fr)); /* stretches columns to fit*/
}
```