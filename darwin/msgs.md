MSGS(1) - General Commands Manual

# NAME

**msgs** - system messages and junk mail program

# SYNOPSIS

**msgs**
\[**-fhlpq**]
\[*number*]
\[*&#45;number*]  
**msgs**
\[**-s**]  
**msgs**
\[**-c**]
\[&#45;days]

# DESCRIPTION

The
**msgs**
utility is used to read system messages.
These messages are
sent by mailing to the login \`msgs' and should be short
pieces of information which are suitable to be read once by most users
of the system.

The
**msgs**
utility is normally invoked each time you login, by placing it in the file
*.login*
(or
*.profile*
if you use
sh(1)).
It will then prompt you with the source and subject of each new message.
If there is no subject line, the first few non-blank lines of the
message will be displayed.
If there is more to the message, you will be told how
long it is and asked whether you wish to see the rest of the message.
The possible responses are:

**-y**

> Type the rest of the message.

**RETURN**

> Synonym for y.

**-n**

> Skip this message
> and go on to the next message.

**-**

> Redisplay the last message.

**-q**

> Drop out of
> **msgs**;
> the next time
> **msgs**
> will pick up where it last left off.

**-s**

> Append the current message to the file \`\`Messages'' in the current directory;
> \`s&#45;' will save the previously displayed message.
> A \`s' or \`s&#45;' may
> be followed by a space and a file name to receive the message replacing
> the default \`\`Messages''.

**-m**

> A copy of the specified message is placed in a temporary
> mailbox and
> mail(1)
> is invoked on that mailbox.
> Both \`m' and \`s' accept a numeric argument in place of the \`&#45;'.

The
**msgs**
utility keeps track of the next message you will see by a number in the file
*.msgsrc*
in your home directory.
In the directory
*/var/msgs*
it keeps a set of files whose names are the (sequential) numbers
of the messages they represent.
The file
*/var/msgs/bounds*
shows the low and high number of the messages in the directory
so that
**msgs**
can quickly determine if there are no messages for you.
If the contents of
*bounds*
is incorrect it can be fixed by removing it;
**msgs**
will make a new
*bounds*
file the next time it is run with the
**-s**
option.
If
**msgs**
is run with any option other than
**-s**,
an error will be displayed if
*/var/msgs/bounds*
does not exist.

The
**-s**
option is used for setting up the posting of messages.
The line

	msgs: "| /usr/bin/msgs -s"

should be included in
*/etc/mail/aliases*
(see
newaliases(1))
to enable posting of messages.

The
**-c**
option is used for performing cleanup on
*/var/msgs*.
A shell script entry to run
**msgs**
with the
**-c**
option should be placed in
*/etc/periodic/daily*
(see
periodic(8))
to run every night.
This will remove all messages over 21 days old.
A different expiration may be specified on the command line to override
the default.
You must be the superuser to use this option.

Options when reading messages include:

**-f**

> Do not say \`\`No new messages.''.
> This is useful in a
> *.login*
> file since this is often the case here.

**-q**

> Queries whether there are messages, printing
> \`\`There are new messages.'' if there are.
> The command \`\`msgs &#45;q'' is often used in login scripts.

**-h**

> Print the first part of messages only.

**-l**

> Cause only locally originated messages to be reported.

*num*

> A message number can be given
> on the command line, causing
> **msgs**
> to start at the specified message rather than at the next message
> indicated by your
> *.msgsrc*
> file.
> Thus

> > msgs &#45;h 1

> prints the first part of all messages.

*&#45;number*

> Start
> *number*
> messages back from the one indicated in the
> *.msgsrc*
> file, useful for reviews of recent messages.

**-p**

> Pipe long messages through
> less(1).

Within
**msgs**
you can also go to any specific message by typing its number when
**msgs**
requests input as to what to do.

# ENVIRONMENT

The
**msgs**
utility uses the
`HOME`
and
`TERM`
environment variables for the default home directory and
terminal type.

# FILES

*/var/msgs/\*&zwnj;*

> database

*~/.msgsrc*

> number of next message to be presented

# SEE ALSO

mail(1),
less(1),
aliases(5),
periodic(8)

# HISTORY

The
**msgs**
command appeared in
3\.0BSD.

macOS 12.6 - August 8, 2018
