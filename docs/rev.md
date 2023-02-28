REV(1) - General Commands Manual

# NAME

**rev** - reverse lines of a file

# SYNOPSIS

**rev**
\[*file&nbsp;...*]

# DESCRIPTION

The
**rev**
utility copies the specified files to the standard output, reversing the
order of characters in every line.
If no files are specified, the standard input is read.

# EXAMPLES

Reverse the text from stdin:

	$ echo -e "reverse \t these\ntwo lines" | rev
	eseht    esrever
	senil owt

macOS 12.6 - June 27, 2020
