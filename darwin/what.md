WHAT(1) - General Commands Manual

# NAME

**what** - show what versions of object modules were used to construct a file

# SYNOPSIS

**what**
*name*&nbsp;*...*

# DESCRIPTION

**what**
reads each file
*name*
and searches for sequences of the form
"@(#)",
as inserted by the source code control system.  It prints the remainder
of the string following this marker, up to a null character, newline, double
quote, or
"&gt; character."

# BUGS

As
BSD
is not licensed to distribute
`SCCS`.
This is a rewrite of the
**what**
command which is part of
`SCCS`;
it may not behave in exactly the same manner as that
command does.

# HISTORY

The
**what**
command appeared in
4\.0BSD.

BSD 4 - June 6, 1993
