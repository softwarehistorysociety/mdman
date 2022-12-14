WHO(1) - General Commands Manual

# NAME

**who** - display who is logged in

# SYNOPSIS

**who**
\[**-abdHlmpqrsTtu**]
\[*file*]  
**who**
*am&nbsp;i*

# DESCRIPTION

The
**who**
utility displays a list of all users currently logged on, showing for
each user the login name, tty name, the date and time of login, and
hostname if not local.

Available options:

**-a**

> Same as
> **-bdlprTtu**.

**-b**

> Time of last system boot.

**-d**

> Print dead processes.

**-H**

> Write column headings above the regular output.

**-l**

> Print system login processes (unsupported).

**-m**

> Only print information about the current terminal.
> This is the POSIX way of saying
> **who**
> *am i*.

**-p**

> Print active processes spawned by
> launchd(8)
> (unsupported).

**-q**

> "Quick mode":
> List only the names and the number of users currently logged on.
> When this option is used, all other options are ignored.

**-r**

> Print the current runlevel.
> This is meaningless on Mac OS X.

**-s**

> List only the name, line and time fields.
> This is the default.

**-T**

> Print a character after the user name indicating the state of the
> terminal line:
> '+'
> if the terminal is writable;
> '-'
> if it is not;
> and
> '?'
> if a bad line is encountered.

**-t**

> Print last system clock change (unsupported).

**-u**

> Print the idle time for each user, and the associated process ID.

*am I*

> Returns the invoker's real user name.

*file*

> By default,
> **who**
> gathers information from the file
> */var/run/utmpx*.
> An alternative
> *file*
> may be specified.

# FILES

*/var/run/utmpx*

# SEE ALSO

last(1),
mesg(1),
users(1),
getuid(2),
utmpx(5)

# STANDARDS

The
**who**
utility conforms to
IEEE Std 1003.1-2001 (&#8220;POSIX.1&#8221;).

# HISTORY

A
**who**
utility appeared in
Version&#160;1 AT&T UNIX:
[https://www.bell-labs.com/usr/dmr/www/man14.pdf](https://www.bell-labs.com/usr/dmr/www/man14.pdf)

macOS 12.6 - September 1, 2019
