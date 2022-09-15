LOGGER(1) - General Commands Manual

# NAME

**logger** - make entries in the system log

# SYNOPSIS

**logger**
\[**-is**]
\[**-f**&nbsp;*file*]
\[**-p**&nbsp;*pri*]
\[**-t**&nbsp;*tag*]
\[*message&nbsp;...*]

# DESCRIPTION

**Logger**
provides a shell command interface to the
syslog(3)
system log module.

Options:

**-i**

> Log the process id of the logger process
> with each line.

**-s**

> Log the message to standard error, as well as the system log.

**-f** *file*

> Log the specified file.

**-p** *pri*

> Enter the message with the specified priority.
> The priority may be specified numerically or as a \`\`facility.level''
> pair.
> For example, \`\`&#45;p local3.info'' logs the message(s) as
> *info*rmational
> level in the
> *local3*
> facility.
> The default is \`\`user.notice.''

**-t** *tag*

> Mark every line in the log with the specified
> *tag*.

*message*

> Write the message to log; if not specified, and the
> **-f**
> flag is not
> provided, standard input is logged.

The
**logger**
utility exits 0 on success, and &gt;0 if an error occurs.

# EXAMPLES

	logger System rebooted
	
	logger -p local0.notice -t HOSTIDM -f /dev/idmc

# SEE ALSO

syslog(3),
syslogd(8)

# STANDARDS

The
**logger**
utility conforms to
IEEE Std 1003.2-1992 (&#8220;POSIX.2&#8221;).

BSD 4.3 - June 6, 1993
