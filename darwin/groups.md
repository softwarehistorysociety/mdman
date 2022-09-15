GROUPS(1) - General Commands Manual

# NAME

**groups** - show group memberships

# SYNOPSIS

**groups**
\[*user*]

# DESCRIPTION

The
**groups**
utility has been obsoleted by the
id(1)
utility, and is equivalent to
"**id** **-Gn** \[*user*]".
The command
"**id** **-p**"
is suggested for normal interactive use.

The
**groups**
utility displays the groups to which you (or the optionally specified
*user*)
belong.

# EXIT STATUS

The **groups** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# EXAMPLES

Show groups the root user belongs to:

	$ groups root
	wheel operator

# SEE ALSO

id(1)

macOS 12.6 - June 6, 1993
