MKFIFO(1) - General Commands Manual

# NAME

**mkfifo** - make fifos

# SYNOPSIS

**mkfifo**
\[**-m**&nbsp;*mode*]
*fifo\_name&nbsp;...*

# DESCRIPTION

**mkfifo**
creates the fifos requested, in the order specified.
By default,
the resulting fifos have mode
`0666`
(rw-rw-rw-), limited by the current
umask(2).

The options are as follows:

**-m**

> Set the file permission bits of newly-created fifos to
> *mode*,
> without respect to the current umask.

> The mode is specified as in
> chmod(1).
> In symbolic mode strings, the
> "+"
> and
> "-"
> operators are interpreted relative to an assumed initial mode of
> "a=rw"

**mkfifo**
requires write permission in the parent directory.

**mkfifo**
exits with 0 if successful, and with &gt;0 if an error occurred.

# LEGACY DESCRIPTION

In legacy mode, the fifo's file permission bits
are always limited by the current umask.

For more information about legacy mode, see
compat(5).

# SEE ALSO

mkdir(1),
rm(1),
umask(1),
mkfifo(2),
umask(2),
compat(5),
mknod(8)

# STANDARDS

The
**mkfifo**
utility is expected to be
IEEE Std 1003.2-1992 (&#8220;POSIX.2&#8221;)
compliant.

# HISTORY

**mkfifo**
command appeared in
4\.4BSD.

BSD 4.4 - January 5, 1994
