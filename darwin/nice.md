NICE(1) - General Commands Manual

# NAME

**nice** - execute a utility with an altered scheduling priority

# SYNOPSIS

**nice**
\[**-n**&nbsp;*increment*]
*utility*
\[*argument&nbsp;...*]

# DESCRIPTION

**nice**
runs
*utility*
at an altered scheduling priority.
If an
*increment*
is given, it is used; otherwise
an increment of 10 is assumed.
The super-user can run utilities with priorities higher than normal by using
a negative
*increment*.
The priority can be adjusted over a
range of -20 (the highest) to 20 (the lowest).

Available options:

**-n** *increment*

> A positive or negative decimal integer used to modify the system scheduling
> priority of
> *utility.*

# DIAGNOSTICS

The
**nice**
utility shall exit with one of the following values:

1-125

> An error occurred in the
> **nice**
> utility.

126

> The
> *utility*
> was found but could not be invoked.

127

> The
> *utility*
> could not be found.

Otherwise, the exit status of
**nice**
shall be that of
*utility*.

# COMPATIBILITY

The historic
**-**&zwnj;*increment*
option has been deprecated but is still supported in this implementation.

# SEE ALSO

csh(1),
getpriority(2),
setpriority(2),
renice(8)

# STANDARDS

The
**nice**
utility conforms to
IEEE Std 1003.2-1992 (&#8220;POSIX.2&#8221;).

# HISTORY

A
**nice**
utility appeared in
Version&#160;6 AT&T UNIX.

# BUGS

**nice**
is built into
csh(1)
with a slightly different syntax than described here.  The form
'`nice +10`'
nices to positive nice, and
'`nice -10`'
can be used
by the super-user to give a process more of the processor.

macOS 12.6 - June 6, 1993
