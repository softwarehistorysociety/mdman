FROM(1) - General Commands Manual

# NAME

**from** - print names of those who have sent mail

# SYNOPSIS

**from**
\[**-c**]
\[**-s**&nbsp;*sender*]
\[**-f**&nbsp;*file*]
\[*user*]

# DESCRIPTION

The
**from**
utility prints
out the mail header lines from the invoker's mailbox.

The following options are available:

**-c**

> Just print a count of messages and exit.

**-f** *file*

> The supplied file
> is examined instead of the invoker's mailbox.
> If the
> **-f**
> option is used, the
> *user*
> argument should not be used.
> Read from standard input if file name
> *-*
> is given.

**-s** *sender*

> Only mail from addresses containing
> the
> supplied string are printed.

If
*user*
is given, the
*user*'s
mailbox is examined instead of the invoker's own mailbox.
(Privileges are required.)

# ENVIRONMENT

`MAIL`

> If set, the location of the invoker's mailbox.
> Otherwise, the default in
> */var/mail*
> is used.

# FILES

*/var/mail/\*&zwnj;*

# SEE ALSO

biff(1),
mail(1)

# HISTORY

The
**from**
command appeared in
3\.0BSD.

macOS 12.6 - December 30, 1993
