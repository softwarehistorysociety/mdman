LOGNAME(1) - General Commands Manual

# NAME

**logname** - display user's login name

# SYNOPSIS

**logname**

# DESCRIPTION

The
**logname**
utility writes the user's login name to standard output followed by
a newline.

The
**logname**
utility explicitly ignores the
`LOGNAME`
and
`USER`
environment variables
because the environment cannot be trusted.

The
**logname**
utility exits 0 on success, and &gt;0 if an error occurs.

# SEE ALSO

who(1),
whoami(1),
getlogin(2)

# STANDARDS

The
**logname**
utility conforms to
IEEE Std 1003.2-1992 (&#8220;POSIX.2&#8221;).

# HISTORY

The
**logname**
command appeared in
4\.4BSD.

BSD 4.4 - June 9, 1993
