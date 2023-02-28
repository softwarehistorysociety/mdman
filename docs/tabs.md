TABS(1) - General Commands Manual

# NAME

**tabs** - set terminal tabs

# SYNOPSIS

**tabs**
\[**-**&zwnj;*n*&nbsp;|&nbsp;**-a**&nbsp;|&nbsp;**-a2**&nbsp;|&nbsp;**-c**&nbsp;|&nbsp;**-c2**&nbsp;|&nbsp;**-c3**&nbsp;|&nbsp;**-f**&nbsp;|&nbsp;**-p**&nbsp;|&nbsp;**-s**&nbsp;|&nbsp;**-u**]
\[**+m**\[*n*]]
\[**-T**&nbsp;*type*]  
**tabs**
\[**-T**&nbsp;*type*]
\[**+**\[*n*]]
*n1*\[,*n2*,...]

# DESCRIPTION

The
**tabs**
utility displays a series of characters that clear the hardware terminal
tab settings then initialises tab stops at specified positions, and
optionally adjusts the margin.

In the first synopsis form, the tab stops set depend on the command line
options used, and may be one of the predefined formats or at regular
intervals.

In the second synopsis form, tab stops are set at positions
*n1*, *n2*,
etc.
If a position is preceded by a
'`+`',
it is relative to the previous position set.
No more than 20 positions may be specified.

If no tab stops are specified, the
"standard"
UNIX
tab width of 8 is used.

The options are as follows:

**-***n*

	Set a tab stop every
	*n*
	columns.
	If
	*n*
	is 0, the tab stops are cleared but no new ones are set.

**-a**

> Assembler format (columns 1, 10, 16, 36, 72).

**-a2**

> Assembler format (columns 1, 10, 16, 40, 72).

**-c**

> `COBOL`
> normal format (columns 1, 8, 12, 16, 20, 55)

**-c2**

> `COBOL`
> compact format (columns 1, 6, 10, 14, 49)

**-c3**

> `COBOL`
> compact format (columns 1, 6, 10, 14, 18, 22, 26, 30, 34, 38, 42, 46,
> 50, 54, 58, 62, 67).

**-f**

> `FORTRAN`
> format (columns 1, 7, 11, 15, 19, 23).

**-p**

> `PL/1`
> format (columns 1, 5, 9, 13, 17, 21, 25, 29, 33, 37, 41, 45, 49, 53,
> 57, 61).

**-s**

> `SNOBOL`
> format (columns 1, 10, 55).

**-u**

> Assembler format (columns 1, 12, 20, 44).

**+m**\[*n*],
**+**\[*n*]

> Set an
> *n*
> character left margin, or 10 if
> *n*
> is omitted.

**-T** *type*

> Output escape sequence for the terminal type
> *type*.

# ENVIRONMENT

The
`LANG`, `LC_ALL`, `LC_CTYPE`
and
`TERM`
environment variables affect the execution of
**tabs**
as described in
environ(7).

The
**-T**
option overrides the setting of the
`TERM`
environment variable.
If neither
`TERM`
nor the
**-T**
option are present,
**tabs**
will fail.

# EXIT STATUS

The **tabs** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# SEE ALSO

expand(1),
stty(1),
tput(1),
unexpand(1),
termcap(5)

# STANDARDS

The
**tabs**
utility conforms to
IEEE Std 1003.1-2001 (&#8220;POSIX.1&#8221;).

# HISTORY

A
**tabs**
utility appeared in PWB UNIX.
This implementation was introduced in
FreeBSD 5.0.

# BUGS

The current
termcap(5)
database does not define the
'`ML`'
(set left soft margin) capability for any terminals.

macOS 12.6 - May 20, 2002
