# Practical Common Lisp: Chapter 4

## Syntax and Semantics

&nbsp;

## About Lisp's Language Processor

Common Lisp defines two black boxes, one that translates text into Lisp objects and another that implements the semantics of the language in terms of those objects. The first box is called the _reader_, and the second is called the _evaluator_.

The **reader** defines how strings of characters can be translated into Lisp objects called [s-expressions](#s-expressions). This syntax allows for lists of arbitrary objects, which means they can represent arbitrary tree expressions.

The **evaluator** then defines a syntax of Lisp _forms_ that can be built out of s-expressions. Not all s-expressions are legal Lisp forms any more than all sequences of characters are legal s-expressions.

With this reader and evaluator approach, the major benefit is that you can generate code by manipulating existing data – which is also the basis for Lisp macros.

<br>

<a name=s-expressions></a>
## S-expressions

The basic elements of s-expressions are _lists_ and _atoms_. Lists are delimited by parentheses and can contain any number of whitespace-separated elements. Atoms are everything else.

The elements of lists are themselves s-expressions (in other words, atoms or nested lists).

Strings have predictable behavior, save that the **only two characters that must be escaped within a string are double quotes and the backslash itself**. Characters are escaped with the backslash (`\`).

### Symbols

Names used in Lisp programs, such as `FORMAT` and `hello-world`, and `*db*` are represented by objects called _symbols_.

Whitespace cannot appear in a name, but almost any other character can.

- Numbers can appear, as long as the name is not representative of a valid Lisp number
- Periods can appear, as long as the name isn't entirely composed of periods
- Characters that can't appear in a name:
	- `(` & `)` parentheses
	- `'` & `"` single and double quotes
	- ``` ` ``` backtick
	- `,` comma
	- `:` colon
	- `;` semicolon
	- `\` backslash
	- `|` vertical bar


The reader _interns_ symbols: after it has read the name and converted it to all uppercase, the reader looks in a table called a _package_ for an existing symbol with the same name; if it can’t find one, it creates a new symbol and adds it to the table.

<br>

<a name=s-expressions-as-lisp-forms></a>
## S-expressions As Lisp Forms

<br>

## Notes

- global variables' names start with `*`


- constants' names start with `+`