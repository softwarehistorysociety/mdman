UUENCODE(1) - General Commands Manual

# NAME

**uudecode**,
**uuencode** - encode/decode a binary file

# SYNOPSIS

**uuencode**
\[**-m**]
\[**-o**&nbsp;*output\_file*]
\[*file*]
*name*  
**uudecode**
\[**-cips**]
\[*file&nbsp;...*]  
**uudecode**
\[**-i**]
**-o**&nbsp;*output\_file*
\[*file*]

# DESCRIPTION

The
**uuencode**
and
**uudecode**
utilities are used to transmit binary files over transmission mediums
that do not support other than simple
`ASCII`
data.

The
**uuencode**
utility reads
*file*
(or by default the standard input) and writes an encoded version
to the standard output, or
*output\_file*
if one has been specified.
The encoding uses only printing
`ASCII`
characters and includes the
mode of the file and the operand
*name*
for use by
**uudecode**.

The
**uudecode**
utility transforms
*uuencoded*
files (or by default, the standard input) into the original form.
The resulting file is named either
*name*
or (depending on options passed to
**uudecode**)
*output\_file*
and will have the mode of the original file except that setuid
and execute bits are not retained.
The
**uudecode**
utility ignores any leading and trailing lines.

The following options are available for
**uuencode**:

**-m**

> Use the Base64 method of encoding, rather than the traditional
> **uuencode**
> algorithm.

**-o** *output\_file*

> Output to
> *output\_file*
> instead of standard output.

The following options are available for
**uudecode**:

**-c**

> Decode more than one uuencode'd file from
> *file*
> if possible.

**-i**

> Do not overwrite files.

**-o** *output\_file*

> Output to
> *output\_file*
> instead of any pathname contained in the input data.

**-p**

> Decode
> *file*
> and write output to standard output.

**-s**

> Do not strip output pathname to base filename.
> By default
> **uudecode**
> deletes any prefix ending with the last slash '/' for security
> purpose.

# EXAMPLES

The following example packages up a source tree, compresses it,
uuencodes it and mails it to a user on another system.
When
**uudecode**
is run on the target system, the file \`\`src\_tree.tar.Z'' will be
created which may then be uncompressed and extracted into the original
tree.

	tar cf - src_tree | compress |
	uuencode src_tree.tar.Z | mail sys1!sys2!user

The following example unpack all uuencode'd
files from your mailbox into your current working directory.

	uudecode -c < $MAIL

The following example extract a compress'ed tar
archive from your mailbox

	uudecode -o /dev/stdout < $MAIL | zcat | tar xfv -

# LEGACY DESCRIPTION

In legacy operation,
**uudecode**
masks file modes with 0666,
preventing the creation of executable files.

**uudecode**
cannot change the mode of a created file
which is not owned by the current user (unless that user is root).
In legacy operation,
fchmod(2)
allows the mode to be changed.

For more information about legacy mode, see
compat(5).

# SEE ALSO

basename(1),
compress(1),
mail(1),
uucp(1),
fchmod(2),
uuencode(5)

# BUGS

Files encoded using the traditional algorithm are expanded by 35%
(3 bytes become 4, plus control information).

# HISTORY

The
**uudecode**
and
**uuencode**
utilities appeared in
4\.0BSD.

macOS 12.6 - January 27, 2002
