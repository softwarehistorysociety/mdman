SC\_USAGE(1) - General Commands Manual

# NAME

**sc\_usage** - show system call usage statistics

# SYNOPSIS

**sc\_usage**
\[**-c**&nbsp;*codefile*]
\[**-e**]
\[**-l**]
\[**-s**&nbsp;*interval*]
pid | cmd |
**-E**
execute

# DESCRIPTION

**sc\_usage**
displays an ongoing sample of system call and page fault usage statistics for
a given process in a
"`top-like`"
fashion.
It requires root privileges due to the kernel tracing facility it uses to
operate.

Page faults can be of the following types:

PAGE\_IN

> page had to read from disk

ZERO\_FILL

> page was created and zero filled

COW

> page was copied from another page

CACHE\_HIT

> page was found in the cache

The arguments are as follows:

**-c**

> When the
> **-c**
> option is specified, it expects a path to a
> *codefile*
> that
> contains the mappings for the system calls.
> This option overrides the default location of the system call codefile which
> is found in /usr/share/misc/trace.codes.

**-e**

> Specifying the
> **-e**
> option generates output that is sorted by call count.
> This overrides the default sort by time.

**-l**

> The
> **-l**
> option causes
> **sc\_usage**
> to turn off its continuous window updating style of output and instead output
> as a continuous scrolling of data.

**-s**

> By default,
> **sc\_usage**
> updates its output at one second intervals.
> This sampling interval may be changed by specifying the
> **-s**
> option.
> Enter the
> *interval*
> in seconds.

pid | cmd | -E execute

> The last argument must be a process id, a running command name, or using the
> **-E**
> option, an execution path followed by optional arguments.
> The system call usage data for the process or command is displayed.
> If the
> **-E**
> flag is used, sc\_usage will launch the executable, pass along any optional
> arguments and display system call usage date for that executable.

The data columns displayed are as follows:

TYPE

> the system call type

NUMBER

> the system call count

CPU\_TIME

> the amount of cpu time consumed

WAIT\_TIME

> the absolute time the process is waiting

CURRENT\_TYPE

> the current system call type

LAST\_PATHNAME\_WAITED\_FOR

> for each active thread, the last pathname
> that was referenced by a system call that blocked

CUR\_WAIT\_TIME

> the cumulative time that a thread has been blocked

THRD#

> the thread number

PRI

> current scheduling priority

The
**sc\_usage**
command also displays some global state in the first few lines of output,
including the number of preemptions, context switches, threads, faults and
system calls, found during the sampling period.
The current time and the elapsed time that the command has been running is also
displayed here.
The
**sc\_usage**
command is also SIGWINCH savvy, so adjusting your window geometry may change
the list of system calls being displayed.
Typing a
'`q`'
will cause sc\_usage to exit immediately.
Typing any other character will cause sc\_usage to reset its counters and the
display.

# SAMPLE USAGE

sc\_usage Finder -e -s2

**sc\_usage**
will sort the Finder process usage data according to system call count and
update the output at 2 second intervals.

# SEE ALSO

fs\_usage(1),
latency(1),
top(1)

macOS - October 28, 2002
