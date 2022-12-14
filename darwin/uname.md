UNAME(1) - General Commands Manual

# NAME

**uname** - Print operating system name

# SYNOPSIS

**uname**
\[**-amnprsv**]

# DESCRIPTION

The
**uname**
utility writes symbols representing one or more system characteristics
to the standard output.

The following options are available:

**-a**

> Behave as though all of the options
> **-mnrsv**
> were specified.

**-m**

> print the machine hardware name.

**-n**

> print the nodename (the nodename may be a name
> that the system is known by to a communications
> network).

**-p**

> print the machine processor architecture name.

**-r**

> print the operating system release.

**-s**

> print the operating system name.

**-v**

> print the operating system version.

If no options are specified,
**uname**
prints the operating system name as if the
**-s**
option had been specified.

# SEE ALSO

hostname(1),
machine(1),
sw\_vers(1),
uname(3)

# STANDARDS

The
**uname**
utility conforms to
IEEE Std 1003.2-1992 (&#8220;POSIX.2&#8221;).
The
**-p**
option is an extension to the standard.

macOS 12.6 - November 9, 1998
