WHICH(1) - General Commands Manual

# NAME

**which** - locate a program file in the user's path

# SYNOPSIS

**which**
\[**-as**]
*program&nbsp;...*

# DESCRIPTION

The
**which**
utility
takes a list of command names and searches the path for each executable
file that would be run had these commands actually been invoked.

The following options are available:

**-a**

> List all instances of executables found (instead of just the first one
> of each).

**-s**

> No output, just return 0 if all of the executables are found, or 1 if
> some were not found.

Some shells may provide a builtin
**which**
command which is similar or identical to this utility.
Consult the
builtin(1)
manual page.

# SEE ALSO

builtin(1),
csh(1),
find(1),
locate(1),
whereis(1)

# HISTORY

The
**which**
command first appeared in
FreeBSD 2.1.

# AUTHORS

The
**which**
utility was originally written in Perl and was contributed by
Wolfram Schneider &lt;[wosch@FreeBSD.org](mailto:wosch@FreeBSD.org)&gt;.
The current version of
**which**
was rewritten in C by
Daniel Papasian &lt;[dpapasia@andrew.cmu.edu](mailto:dpapasia@andrew.cmu.edu)&gt;.

macOS 12.6 - December 13, 2006
