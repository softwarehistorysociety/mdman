db\_deadlock(1) - General Commands Manual

# NAME

**db\_deadlock**

# SYNOPSIS

**db\_deadlock**
\[**-Vv**]
\[**-a**&nbsp;*e*&nbsp;|&nbsp;*m*&nbsp;|&nbsp;*n*&nbsp;|&nbsp;*o*&nbsp;|&nbsp;*w*&nbsp;|&nbsp;*y*]
\[**-h**&nbsp;*home*]
\[**-L**&nbsp;*file*]
\[**-t**&nbsp;*sec.usec*]

# DESCRIPTION

The
**db\_deadlock**
utility traverses the database environment lock region, and aborts a lock request each time it detects a deadlock or a lock request that has timed out. By default, in the case of a deadlock, a random lock request is chosen to be aborted.

This utility should be run as a background daemon, or the underlying Berkeley DB deadlock detection interfaces should be called in some other way, whenever there are multiple threads or processes accessing a database and at least one of them is modifying it.

The options are as follows:

**-a**

> When a deadlock is detected, abort the locker:

> m

> > with the greatest number of locks

> n

> > with the fewest number of locks

> o

> > with the oldest locker ID

> w

> > with the fewest number of write locks

> y

> > with the youngest locker ID

> When lock or transaction timeouts have been specified:

> e

> > abort any lock request that has timed out

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-L**

> Log the execution of the db\_deadlock utility to the specified file in the following format, where ### is the process ID, and the date is the time the utility was started.

> > db\_deadlock: ### Wed Jun 15 01:23:45 EDT 1995

> This file will be removed if the db\_deadlock utility exits gracefully.

**-t**

> Check the database environment every sec seconds plus usec microseconds to see if a process has been forced to wait for a lock; if one has, review the database environment lock structures.

**-V**

> Write the library version number to the standard output, and exit.

**-v**

> Run in verbose mode, generating messages each time the detector runs.

If the -t option is not specified, db\_deadlock will run once and exit.

The db\_deadlock utility uses a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment, db\_deadlock should always be given the chance to detach from the environment and exit gracefully. To cause db\_deadlock to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The db\_deadlock utility does not attempt to create the Berkeley DB shared memory regions if they do not already exist. The application which creates the region should be started first, and then, once the region is created, the db\_deadlock utility should be started.

The DB\_ENV-&gt;lock\_detect method is the underlying method used by the db\_deadlock utility. See the db\_deadlock utility source code for an example of using DB\_ENV-&gt;lock\_detect in a IEEE/ANSI Std 1003.1 (POSIX) environment.

The
**db\_deadlock**
utility exits 0 on success, and &gt;0 if an error occurs.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SEE ALSO

db\_archive(1),
db\_checkpoint(1),
db\_dump(1),
db\_load(1),
db\_printlog(1),
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003