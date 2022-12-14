BIFF(1) - General Commands Manual

# NAME

**biff** - be notified if mail arrives and who it is from

# SYNOPSIS

**biff**
\[**n**&nbsp;|&nbsp;**y**&nbsp;|&nbsp;**b**]

# DESCRIPTION

The
**biff**
utility informs the system whether you want to be notified on your terminal
when mail arrives.

Affected is the first terminal associated with the standard input,
standard output or standard error file descriptor, in that order.
Thus, it is possible to use the redirection facilities of a shell to
toggle the notification for other terminals than the one
**biff**
runs on.

The following options are available:

**n**

> Disable notification.

**y**

> Enable header notification.

**b**

> Enable bell notification.

When header notification is enabled, the header and first few lines of
the message will be printed on your terminal whenever mail arrives.
A
"`biff y`"
command is often included in the file
*.login*
or
*.profile*
to be executed at each login.

When bell notification is enabled, only two bell characters
(`ASCII`
&#92;007)
will be printed on your terminal whenever mail arrives.

If no arguments are given,
**biff**
displays the present notification status of the terminal to the
standard output.

The
**biff**
utility operates asynchronously.
For synchronous notification use the
`MAIL`
variable of
sh(1)
or the
`mail`
variable of
csh(1).

# DIAGNOSTICS

The
**biff**
utility exits with one of the following values:

0

> Notification is enabled.

1

> Notification is disabled.

&gt;1

> An error occurred.

# COMPATIBILITY

Previous versions of the
**biff**
utility affected the terminal attached to standard error without first
trying the standard input or output devices.

# SEE ALSO

csh(1),
mail(1),
sh(1),
comsat(8)

# HISTORY

The
**biff**
command appeared in
4\.0BSD.
It was named after the dog of Heidi Stettner.
He died
in August 1993, at 15.

macOS 12.6 - July 9, 2002
