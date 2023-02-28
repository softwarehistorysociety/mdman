KILL(1) - General Commands Manual

# NAME

**kill** - terminate or signal a process

# SYNOPSIS

**kill**
\[**-s**&nbsp;*signal\_name*]
*pid&nbsp;...*  
**kill**
**-l**
\[*exit\_status*]  
**kill**
**-**&zwnj;*signal\_name*
*pid&nbsp;...*  
**kill**
**-**&zwnj;*signal\_number*
*pid&nbsp;...*

# DESCRIPTION

The
**kill**
utility sends a signal to the processes specified by the
*pid*
operands.

Only the super-user may send signals to other users' processes.

The options are as follows:

**-s** *signal\_name*

> A symbolic signal name specifying the signal to be sent instead of the
> default
> `TERM`.

**-l** \[*exit\_status*]

> If no operand is given, list the signal names; otherwise, write
> the signal name corresponding to
> *exit\_status*.

**-**&zwnj;*signal\_name*

> A symbolic signal name specifying the signal to be sent instead of the
> default
> `TERM`.

**-**&zwnj;*signal\_number*

> A non-negative decimal integer, specifying the signal to be sent instead
> of the default
> `TERM`.

The following PIDs have special meanings:

\-1

> If superuser, broadcast the signal to all processes; otherwise broadcast
> to all processes belonging to the user.

Some of the more commonly used signals:

1

> HUP (hang up)

2

> INT (interrupt)

3

> QUIT (quit)

6

> ABRT (abort)

9

> KILL (non-catchable, non-ignorable kill)

14

> ALRM (alarm clock)

15

> TERM (software termination signal)

Some shells may provide a builtin
**kill**
command which is similar or identical to this utility.
Consult the
builtin(1)
manual page.

# EXIT STATUS

The **kill** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# EXAMPLES

Terminate
the processes with PIDs 142 and 157:

	kill 142 157

Send the hangup signal
(`SIGHUP`)
to the process with PID 507:

	kill -s HUP 507

Terminate the process group with PGID 117:

	kill -- -117

# SEE ALSO

builtin(1),
csh(1),
killall(1),
ps(1),
sh(1),
kill(2),
sigaction(2)

# STANDARDS

The
**kill**
utility is expected to be
IEEE Std 1003.2 (&#8220;POSIX.2&#8221;)
compatible.

# HISTORY

A
**kill**
command appeared in
Version&#160;3 AT&T UNIX
in section 8 of the manual.

# BUGS

A replacement for the command
"`kill 0`"
for
csh(1)
users should be provided.

macOS 12.6 - October 3, 2016
