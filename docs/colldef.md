COLLDEF(1) - General Commands Manual

# NAME

**colldef** - convert collation sequence source definition

# SYNOPSIS

**colldef**
\[**-I**&nbsp;*map\_dir*]
\[**-o**&nbsp;*out\_file*]
\[*filename*]

# DESCRIPTION

The
**colldef**
utility converts a collation sequence source definition
into a format usable by the
**strxfrm**()
and
**strcoll**()
functions.
It is used to define the many ways in which
strings can be ordered and collated.
The
**strxfrm**()
function transforms
its first argument and places the result in its second
argument.
The transformed string is such that it can be
correctly ordered with other transformed strings by using
**strcmp**(),
**strncmp**(),
or
**memcmp**().
The
**strcoll**()
function transforms its arguments and does a
comparison.

The
**colldef**
utility reads the collation sequence source definition
from the standard input and stores the converted definition in filename.
The output file produced contains the
database with collating sequence information in a form
usable by system commands and routines.

The following options are available:

**-I** *map\_dir*

> Set directory name where
> *charmap*
> files can be found, current directory by default.

**-o** *out\_file*

> Set output file name,
> *LC\_COLLATE*
> by default.

The collation sequence definition specifies a set of collating elements and
the rules defining how strings containing these should be ordered.
This is most useful for different language definitions.

The specification file can consist of three statements:
*charmap*,
*substitute*
and
*order*.

Of these, only the
*order*
statement is required.
When
*charmap*
or
*substitute*
is
supplied, these statements must be ordered as above.
Any
statements after the order statement are ignored.

Lines in the specification file beginning with a
'`#`'
are
treated as comments and are ignored.
Blank lines are also
ignored.

	charmap charmapfile

*Charmap*
defines where a mapping of the character
and collating element symbols to the actual
character encoding can be found.

The format of
*charmapfile*
is shown below.
Symbol
names are separated from their values by TAB or
SPACE characters.
Symbol-value can be specified in
a hexadecimal (&#92;x*??*) or octal (&#92;*???*)
representation, and can be only one character in length.

> symbol-name1 symbol-value1
> symbol-name2 symbol-value2
> ...

Symbol names cannot be specified in
*substitute*
fields.

The
*charmap*
statement is optional.

> substitute "symbol" with "repl\_string"

The
*substitute*
statement substitutes the character
*symbol*
with the string
*repl\_string*.
Symbol names cannot be specified in
*repl\_string*
field.
The
*substitute*
statement is optional.

> order order\_list

*Order\_list*
is a list of symbols, separated by semi colons, that defines the
collating sequence.
The
special symbol
*...*
specifies, in a short-hand
form, symbols that are sequential in machine code
order.

An order list element
can be represented in any one of the following
ways:

*	The symbol itself (for example,
	*a*
	for the lower-case letter
	*a*).

*	The symbol in octal representation (for example,
	*&#92;141*
	for the letter
	*a*).

*	The symbol in hexadecimal representation (for example,
	*&#92;x61*
	for the letter
	*a*).

*	The symbol name as defined in the
	*charmap*
	file (for example,
	*&lt;letterA&gt;*
	for
	*letterA &#92;023*
	record in
	*charmapfile*).
	If character map name have
	*&gt;*
	character, it must be escaped as
	*/&gt;*,
	single
	*/*
	must be escaped as
	*//*.

*	Symbols
	*&#92;a*,
	*&#92;b*,
	*&#92;f*,
	*&#92;n*,
	*&#92;r*,
	*&#92;v*
	are permitted in its usual C-language meaning.

*	The symbol chain (for example:
	*abc*,
	*&lt;letterA&gt;&lt;letterB&gt;c*,
	*&#92;xf1b&#92;xf2*)

*	The symbol range (for example,
	*a;...;z*).

*	Comma-separated symbols, ranges and chains enclosed in parenthesis (for example
	*(*
	*sym1*,
	*sym2*,
	*...*
	*)*)
	are assigned the
	same primary ordering but different secondary
	ordering.

*	Comma-separated symbols, ranges and chains enclosed in curly brackets (for example
	*{*
	*sym1*,
	*sym2*,
	*...*
	*}*)
	are assigned the same primary ordering only.

The backslash character
*&#92;*
is used for continuation.
In this case, no characters are permitted
after the backslash character.

# DIAGNOSTICS

The
**colldef**
utility exits with the following values:

`0`

> No errors were found and the output was successfully created.

`!=0`

> Errors were found.

# FILES

*/usr/share/locale/*&lt;*language*&gt;*/LC\_COLLATE*

> The standard shared location for collation orders
> under the locale
> &lt;*language*&gt;.

# SEE ALSO

mklocale(1),
setlocale(3),
strcoll(3),
strxfrm(3)

macOS 12.6 - January 27, 1995
