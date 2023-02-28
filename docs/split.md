SPLIT(1) - General Commands Manual

# NAME

**split** - split a file into pieces

# SYNOPSIS

**split**
**-d**
\[**-l**&nbsp;*line\_count*]
\[**-a**&nbsp;*suffix\_length*]
\[*file*&nbsp;\[*prefix*]]  
**split**
**-d**
**-b**&nbsp;*byte\_count*\[**K**|**k**|**M**|**m**|**G**|**g**]
\[**-a**&nbsp;*suffix\_length*]
\[*file*&nbsp;\[*prefix*]]  
**split**
**-d**
**-n**&nbsp;*chunk\_count*
\[**-a**&nbsp;*suffix\_length*]
\[*file*&nbsp;\[*prefix*]]  
**split**
**-d**
**-p**&nbsp;*pattern*
\[**-a**&nbsp;*suffix\_length*]
\[*file*&nbsp;\[*prefix*]]

# DESCRIPTION

The
**split**
utility reads the given
*file*
and breaks it up into files of 1000 lines each
(if no options are specified), leaving the
*file*
unchanged.
If
*file*
is a single dash
('**-**')
or absent,
**split**
reads from the standard input.

The options are as follows:

**-a** *suffix\_length*

> Use
> *suffix\_length*
> letters to form the suffix of the file name.

**-b** *byte\_count*\[**K**|**k**|**M**|**m**|**G**|**g**]

> Create split files
> *byte\_count*
> bytes in length.
> If
> **k**
> or
> **K**
> is appended to the number, the file is split into
> *byte\_count*
> kilobyte pieces.
> If
> **m**
> or
> **M**
> is appended to the number, the file is split into
> *byte\_count*
> megabyte pieces.
> If
> **g**
> or
> **G**
> is appended to the number, the file is split into
> *byte\_count*
> gigabyte pieces.

**-d**

> Use a numeric suffix instead of a alphabetic suffix.

**-l** *line\_count*

> Create split files
> *line\_count*
> lines in length.

**-n** *chunk\_count*

> Split file into
> *chunk\_count*
> smaller files.
> The first n - 1 files will be of size (size of
> *file*
> /
> *chunk\_count*
> )
> and the last file will contain the remaining bytes.

**-p** *pattern*

> The file is split whenever an input line matches
> *pattern*,
> which is interpreted as an extended regular expression.
> The matching line will be the first line of the next output file.
> This option is incompatible with the
> **-b**
> and
> **-l**
> options.

If additional arguments are specified, the first is used as the name
of the input file which is to be split.
If a second additional argument is specified, it is used as a prefix
for the names of the files into which the file is split.
In this case, each file into which the file is split is named by the
prefix followed by a lexically ordered suffix using
*suffix\_length*
characters in the range
"`a`-`z`".
If
**-a**
is not specified, two letters are used as the suffix.

If the
*prefix*
argument is not specified, the file is split into lexically ordered
files named with the prefix
"`x`"
and with suffixes as above.

# ENVIRONMENT

The
`LANG`, `LC_ALL`, `LC_CTYPE`
and
`LC_COLLATE`
environment variables affect the execution of
**split**
as described in
environ(7).

# EXIT STATUS

The **split** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# EXAMPLES

Split input into as many files as needed, so that each file contains at most 2
lines:

	$ echo -e "first line\nsecond line\nthird line\nforth line" | split -l2

Split input in chunks of 10 bytes using numeric prefixes for file names.
This generates two files of 10 bytes (x00 and x01) and a third file (x02) with the
remaining 2 bytes:

	$ echo -e "This is 22 bytes long" | split -d -b10

Split input generating 6 files:

	echo -e "This is 22 bytes long" | split -n 6

Split input creating a new file every time a line matches the regular expression
for a
"t"
followed by either
"a"
or
"u"
thus creating two files:

	$ echo -e "stack\nstock\nstuck\nanother line" | split -p 't[au]'

# SEE ALSO

csplit(1),
re\_format(7)

# STANDARDS

The
**split**
utility conforms to
IEEE Std 1003.1-2001 (&#8220;POSIX.1&#8221;).

# HISTORY

A
**split**
command appeared in
Version&#160;3 AT&T UNIX.

# BUGS

The maximum line length for matching patterns is 65536.

macOS 12.6 - May 9, 2013
