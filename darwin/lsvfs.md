LSVFS(1) - General Commands Manual

# NAME

**lsvfs** - list known virtual file systems

# SYNOPSIS

**lsvfs**
\[*vfsname*&nbsp;*...*]

# DESCRIPTION

The
**lsvfs**
command lists information about the currently loaded virtual filesystem
modules.
When
*vfsname*
arguments are given,
**lsvfs**
lists information about the specified VFS modules.
Otherwise,
**lsvfs**
lists all currently loaded modules.
The information is as follows:

Filesystem

> the name of the filesystem, as would be used in the
> *type*
> parameter to
> mount(2)
> and the
> **-t**
> option to
> mount(8)

Refs

> the number of references to this VFS; i.e., the number of currently
> mounted filesystems of this type

Flags

> flag bits

# SEE ALSO

mount(2),
mount(8)

# HISTORY

The command from which this tool was derived, as well as this manual,
originally appeared in
FreeBSD 2.0.

macOS 12.6 - January 4, 2003
