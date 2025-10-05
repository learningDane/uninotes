#uni 
HTML (___HyperText Markup Language___) is a _markup_ language. Markup is a way of specifing information about the content.

In the last decade a strong consensus has grown around the belief that HTML documents should only focus on structure and content of the document, and not how this document is visualized, which is left to [[CSS]]. 

This way of operating ensures: maintainability, speed, accessibility, better instructions for search engines -> SEO.

An HTML document is split into **Head** and **Body**, the head contains descriptive elements about the document, the body instead contains what should be displayed.
# HTML Syntax
HTML documents are composed of textual content and HTML elements.
HTML elements contain:
- the element name, within angle brackets, aka the **tag**
- attributes
- the content within the tag
An empty elements doesn't display anything, it just tells the browser to do something.
### Nesting HTML elements
In HTML is is possible to put elements inside of other elements, in such a case, the containing element is said to be the *parent* of the contained (*child*) element.
Any elements contained in the child are said to be *descendants* of the parent element, which to the descendants is *ancestor*.
# Simplest HTML document
```HTML
<!DOCTYPE html>
<title>titolo</title>
<p>paragraph</p>
```
where:
- *doctype* tells the browser what kind of document it is about to process
- the *title* element is used to provide a broad description of the content; the title is not displayed in the rendered page, it is instead displayed in the browsers tabs.
# Complete HTML document
```HTML
<!DOCTYPE html>
<html>
<head lang="en">
	<meta charset = "utf-8">
	<title> titolo </title>
	<script src="fileJS.js"></script>
	<link rel="stylesheet" href="fileCSS.css">
</head>
<body>
	<h1> Main heading </h1>
</body>
</html>
```
where:
- `script` specifies the [[JavaScript]] file
- `link rel="stylesheet href="..."` specifies the [[CSS]] file
- the `<html>` elements is called the **root** element since it contains all the other HTML elements in the document
- `<head>` contains descriptive elements about the document
- `<body>` contains content that will be displayed by the browser
# Elements
- `<h></h>` heading
- `<p><p/>` paragraph, **notice:** the `<p>` tag is a container and as such it can contains HTML and other inline HTML elements.
- `<div>` is a container, not displayed by the browser, does nothing, used to separate the code
- `<a>` anchor, has attribute `href="link/image"></a>` used for [[#Link]].
- `<!-- commentooo -->` comment
### Inline HTML elements
Inline HTML elements do not cause a paragraph break but are part of the "regular" flow of the text.
### Elementi a chiusura autonoma
`<br>` serve per andare a capo
`<hr>` una linea separatrice
### Links
Links can be to external sites, resources within the current site, resources within the same page, particular locations on other page, instructions for user's email program, instructions to execute javascript function.
Links are split in two main parts: the **destination**(link) and the **label**.
```HTML
<a href="link"> Label </a>
<!-- or -->
<a href="link"> <img src="link"/> </>
```
Links can be **global** (`http:/external link`) or **relative** (`/internal link`).

>The `target="_blank"` attribute opens the link in a new page
##### Types of link:
- to external sites (or individual external resources)
- to other pages or resources within the current site
- to particular locations on this (or another) page
	- location on same page: `<a href=#top> to top </a>`
	- location on another page: `<a href="link#PLACE> to PLACE </a>`
- instructions to the browser (execute [[JavaScript]] or open the user's email program etc)
	- mail: `<a href="mailto:EMAILADDRESS"> send the email! </a>`
	- javascript: `<a href="javascript: JSFUNCTION();"> call function </a>`
	- phone: `<a href="tel:NUMBER"> call this number </a>`
### Images
If the image is "content", the semantically appropriate approach is to include it in the HTML. If it instead is purely for decoration, it belongs in the [[CSS]].
```HTML
<img src="linkToImage" alt="altText" title="title" width="80" height="40" />
```
- the text in the **alt** field provides a brief description for people that are unable to see.
- the text in **title** will be displayed in a pop-up tool tip when the user hovers over the image.
- **width** and **height** specify the dimensions in pixels.
# Formattazione
`<b> </b>` __bold__.
`<strong> </strong>` __bold__.
`<em> </em>` $\sim$ _italic_.
`<i> </i>` _italic_.
`<mark> </mark>` highlights text.
`<del> </del>` delete
`<ins> </ins>` underline
`<small> </small>` small
`<sub> </sub>` $aaa_{this is sub}$ 
`<sup> </sup>` $a^{lol}$ 
## Attributi
`<p style="attributo; altro attributo"> </p>` 
`style="Color: colore"` 
`style="border: il bordo che vuoi (oppure none)"` 
`background-color` 
`height="pixel di altezza"` 
`width="pixel di larghezza"` 




# Tabelle
```
<table>
	<tr> //tr sono le righe
		<th> </th>
		<th> ecc //th  sono le colonne (table-heading)
	</tr>
	
	<tr>
		<td> dsrfgerg </td> //table data
		<td> ecc
	</tr>
	
	<tr> ecc
</table>
```
# Lists
`<ul>` *unordered list*: se lista deve essere non-ordinata
`<ol>` *ordered list*: se lista deve essere ordinata
`<dl>` *definition list*: collection of name and definition pairs.
```HTML
<ul>
	<li> sfwf </li>
	<li> 
		<ul>
			<li> first item, first subitem </li>
		</ul>
	</li>
</ul>

<dl>
	<dt> blah blah </dt>
	<dd> descrizione </dd>
	<dt> ecc
</dl>
```
## Elementi in Blocco
Un elemento in blocco aggiunge spazi prima e dopo di se
`<div>` 
`<hr>` 
`<pre>` 
`<tutte le liste>` 
# Character Entities

| entity    | description                  |
| --------- | ---------------------------- |
| `&nbsp;`  | nonbreakable space           |
| `&lt;`    | <                            |
| `&gt;`    | >                            |
| `&copy;`  | &copy                        |
| `&trade;` | trade mark registered symbol |

## I Form
```
<form>
	<label for="per cosa è l'imput"> La label </label>
	<br>
	<input type="tipo ti input (eg: text, number, checkbox)" name="il nome" id="l'id">
</form>
```
