malloc\_history(1) - General Commands Manual

# NAME

**malloc\_history** - Show the malloc and anonymous VM allocations that the process has performed

# SYNOPSIS

**malloc\_history**
*process*
\[**-highWaterMark**]
*address*
\[*address&nbsp;...*]

**malloc\_history**
*process*
**-allBySize**
\[**-highWaterMark**]
\[*address&nbsp;...*]

**malloc\_history**
*process*
**-allByCount**
\[**-highWaterMark**]
\[*address&nbsp;...*]

**malloc\_history**
*process*
**-allEvents**
\[**-highWaterMark**]
\[**-showContent**]

**malloc\_history**
*process*
**-callTree**
\[**-highWaterMark**]
\[**-showContent**]
\[**-invert**]
\[**-ignoreThreads**]
\[**-collapseRecursion**]
\[**-chargeSystemLibraries**]
\[**-virtual**]
\[*address&nbsp;...*&nbsp;|&nbsp;*&lt;classes-pattern&gt;*]

*process*
is a pid, executable-name, or memory-graph-file

# DESCRIPTION

**malloc\_history**
inspects a given process and lists the malloc and anonymous VM allocations performed by it.
Anonymous VM allocations are from calls such as mach\_vm\_allocate that allocate raw Virtual Memory
that is not backed by a file.  Allocations of the VM regions underlying the malloc heaps are ignored.
**malloc\_history**
relies on information provided by the standard malloc
library when malloc stack logging has been enabled for the target process.
See below for further information.

The target process may be specified by pid or by full or partial name,
or it can be the path of a memory graph file generated by
**leaks**
or the Xcode Memory Graph Debugger.

If the
**-highWaterMark**
option is passed,
**malloc\_history**
first scans through the all malloc stack log records to calculate the "high water mark" of allocated memory --
i.e., the highest amount of allocated memory used at any one time by the target process.  It then shows information
about the malloc allocations and anonymous VM regions that were live at that time, rather than currently alive
in the target program.

The
**-highWaterMark**
option does not work with memory graph files since they only contain stack logs for active allocations, not full history.

By specifying one or more addresses,
**malloc\_history**
lists all allocations and deallocations of any malloc blocks or VM regions that started at
or contained those addresses.
For each allocation, a stack trace describing who called malloc or free, or mach\_vm\_allocate, mmap, or mach\_vm\_deallocate is listed.  If you do
only wish to see events for malloc blocks and VM regions that started at the specified address, you can grep
the output for that address.  If
**-highWaterMark**
is passed, it only shows allocations and deallocations up to the high water mark.

Alternatively, the
**-allBySize**
and
**-allByCount**
options list all allocations that are currently live in the target process, or were live at the high water mark.  Frequent allocations from the same
point in the program (that is, the same call stack) are grouped together, and output presented either from
largest allocations to smallest, or most allocations to least.  If you also specify one or more addresses, this output
is filtered to only show information for malloc blocks containing those addresses.

The
**-allEvents**
option lists all allocation and free events, for all addresses, up to the current time or to the high water mark.  This output can be voluminous. If the
**-showContent**
option is passed, live allocations will have additional details as described for that option below.

The
**-callTree**
option generates a call tree of the backtraces of malloc calls and anonymous VM regions for live allocations in the target process, or
for allocations that were live at the high water mark.  The call tree can be filtered to backtraces of specific allocations or classes,
by passing one or more addresses or a &lt;classes-pattern&gt;.

The &lt;classes-pattern&gt; regular expression is interpreted as an extended
(modern) regular expression as described by the re\_format(7) manual page.
"malloc" or "non-object" can be used to refer to blocks that are not of
any specific type. Examples of valid classes-patterns include:

CFString

'NS.\*'

'\_\_NSCFString|\_\_NSCFArray'

'.\*(String|Array)'

'VM:.\*'

malloc

non-object

malloc|.\*String

The &lt;classes-pattern&gt; pattern can be followed by an optional allocation size specifier, which can be
one of the following forms. The square brackets are required. The size can include
a 'k' suffix for kilobytes, or an 'm' suffix for megabytes:

\[size]

\[lowerBound-upperBound]

\[lowerBound+]

\[-upperBound]

Examples of &lt;classes-pattern&gt; with size specifications include:

malloc\[2048]

> all malloc blocks of size 2048

malloc\[1k-8k]

> all malloc blocks between 1k and 8k

'(NS|CF).\*\[10k+]'

> all NS or CF objects 10k or larger

\[-1024]

> all allocations 1024 bytes or less

VM.\*\[1m+]

> all Virtual Memory regions of size 1m or larger; by default this is dirty+swapped-volative size, unless the -virtual flag is passed

The call tree format is similar to the output from
sample(1).
The resulting call tree can be filtered or pruned with the
filtercalltree(1)
tool for further analysis.  Additional options for the
**-callTree**
mode include:

**-showContent**

> Show the content of malloc blocks of various types, including C strings, Pascal strings (with a length
> byte at the start), and various objects including NSString, NSDate, and NSNumber.

**-invert**

> Invert the call tree, so that malloc (and the allocated content, if the
> **-showContent**
> option was given) show at the top of the call trees.

**-ignoreThreads**

> Combine the call trees for all threads into a single call tree.

**-collapseRecursion**

> Collapse recursion within the call trees.

**-chargeSystemLibraries**

> Remove stack frames from all libraries in /System and /usr, while still charging
> their cost (number of calls, allocation size, and content) to the callers.

**-virtual**

> Display the size of VM regions as the virtual size, rather than the default
> dirty + swapped/compressed - purgableVolatile.

All modes require the standard malloc library's debugging facility to be turned on.  To do this, set either the
MallocStackLogging or MallocStackLoggingNoCompact environment variable to 1 in the shell that will run the program.
If MallocStackLogging is used, then when recording events, if an allocation event for an address is immediately
followed by a free event for the same address, both events are removed from the event log.  If MallocStackLoggingNoCompact
is used, then all such immediate allocation/free pairs are kept in the event log, which can be useful when examining all events
for a specific address, or when using the -allEvents option.

If both MallocStackLogging and MallocStackLoggingNoCompact are set, then MallocStackLogging takes precedence and
MallocStackLoggingNoCompact is ignored.

**malloc\_history**
is particularly useful for tracking down memory
smashers.  Run the program to be inspected with MallocStackLogging or MallocStackLoggingNoCompact
defined.  Also set the environment variable MallocScribble; this causes the malloc library to overwrite freed
memory with a well-known value (0x55), and occasionally checks freed malloc blocks to make sure the memory has not
been overwritten since it was cleared.  When malloc detects the memory has been written, it will print out a warning that the buffer
was modified after being freed.  You can then use
**malloc\_history**
to find who
allocated and freed memory at that address, and thus deduce
what parts of the code might still have a pointer to the freed structure.

# EXAMPLE

To see backtraces of allocations by class type or malloc size, run this command:

	% malloc_history <process> -callTree -invert -showContent

# SEE ALSO

malloc(3),
heap(1),
leaks(1),
stringdups(1),
vmmap(1),
filtercalltree(1),
DevToolsSecurity(1)

The Xcode developer tools also include Instruments, a graphical application that can give information similar to that provided by
**malloc\_history.**
The Allocations instrument graphically displays dynamic, real-time
information about the object and memory use in an application, including backtraces
of where the allocations occured.

macOS 12.6 - Oct. 7, 2019