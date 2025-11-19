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