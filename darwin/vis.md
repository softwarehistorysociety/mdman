VIS(1) - General Commands Manual

# NAME

**vis** - display non-printable characters in a visual format

# SYNOPSIS

**vis**
\[**-cbflnostw**]
\[**-F**&nbsp;*foldwidth*]
\[*file&nbsp;...*]

# DESCRIPTION

The
**vis**
utility is a filter for converting non-printable characters
into a visual representation.
It differs from
'`cat -v`'
in that
the form is unique and invertible.
By default, all non-graphic
characters except space, tab, and newline are encoded.
A detailed description of the
various visual formats is given in
vis(3).

The options are as follows:

**-b**

	Turns off prepending of backslash before up-arrow control sequences
	and meta characters, and disables the doubling of backslashes.
	This
	produces output which is neither invertible or precise, but does
	represent a minimum of change to the input.
	It is similar to
	"`cat -v`".

**-c**

> Request a format which displays a small subset of the
> non-printable characters using C-style backslash sequences.

**-F**

> Causes
> **vis**
> to fold output lines to foldwidth columns (default 80), like
> fold(1),
> except
> that a hidden newline sequence is used, (which is removed
> when inverting the file back to its original form with
> unvis(1)).
> If the last character in the encoded file does not end in a newline,
> a hidden newline sequence is appended to the output.
> This makes
> the output usable with various editors and other utilities which
> typically do not work with partial lines.

**-f**

> Same as
> **-F**.

**-l**

> Mark newlines with the visible sequence
> '`&#92;$`',
> followed by the newline.

**-n**

	Turns off any encoding, except for the fact that backslashes are
	still doubled and hidden newline sequences inserted if
	**-f**
	or
	**-F**
	is selected.
	When combined with the
	**-f**
	flag,
	**vis**
	becomes like
	an invertible version of the
	fold(1)
	utility.
	That is, the output
	can be unfolded by running the output through
	unvis(1).

**-o**

	Request a format which displays non-printable characters as
	an octal number, \ddd.

**-s**

	Only characters considered unsafe to send to a terminal are encoded.
	This flag allows backspace, bell, and carriage return in addition
	to the default space, tab and newline.

**-t**

	Tabs are also encoded.

**-w**

	White space (space-tab-newline) is also encoded.

# SEE ALSO

unvis(1),
vis(3)

# HISTORY

The
**vis**
command appeared in
4.4BSD.

# BUGS

Due to limitations in the underlying
vis(3)
function, the
**vis**
utility
does not recognize multibyte characters, and thus may consider them to be
non-printable when they are in fact printable (and vice versa).

macOS 12.6 - June 25, 2004
