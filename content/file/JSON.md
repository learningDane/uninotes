#uni 
for scheme syntax checking: [www.jsonschema.net](www.jsonschema.net)
other useful link: [jsoneditoronline.org](https://jsoneditoronline.org) 

**JSON** (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language Standard ECMA-262 3rd Edition - December 1999. JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.

JSON is built on two structures:
- A collection of name/value pairs. In various languages, this is realized as an _object_, record, struct, dictionary, hash table, keyed list, or associative array.
- An ordered list of values. In most languages, this is realized as an _array_, vector, list, or sequence.

These are universal data structures. Virtually all modern programming languages support them in one form or another. It makes sense that a data format that is interchangeable with programming languages also be based on these structures.
# Objects
In JSON, they take on these forms:
An _object_ is an unordered set of name/value pairs. An object begins with {left brace and ends with }right brace. Each name is followed by :colon and the name/value pairs are separated by ,comma.
# Arrays
An _array_ is an ordered collection of values. An array begins with [left bracket and ends with ]right bracket. Values are separated by ,comma.
# Values
A _value_ can be a _string_ in double quotes, or a _number_, or true or false or null, or an _obj
ect_ or an _array_. These structures can be nested.
## Strings
A _string_ is a sequence of zero or more Unicode characters, wrapped in double quotes, using backslash escapes. A character is represented as a single character string. A string is very much like a C or Java string.
# Schema
```json
{
	"$id": "URI",
	"$schema": "link",
	"title": "Titolo",
	"type": "tipo",
	"properties": {
	 "proprietà1": {
	  "type": "tipo",
	  "description": "descrizione"
	  },
	   "proprietà2": {
	   "type": "tipo",
	   "description": "descrizione"
	   }
	  }
}
```