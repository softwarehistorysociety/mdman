db\_checkpoint(1) - General Commands Manual

# NAME

**db\_checkpoint**

# SYNOPSIS

**db\_checkpoint**
\[**-1Vv**]
\[**-h**&nbsp;*home*]
\[**-k**&nbsp;*kbytes*]
\[**-L**&nbsp;*file*]
\[**-P**&nbsp;*password*]
\[**-p**&nbsp;*min*]

# DESCRIPTION

The
**db\_checkpoint**
utility is a daemon process that monitors the database log, and periodically calls DB\_ENV-&gt;txn\_checkpoint to checkpoint it.

The options are as follows:

**-1**

> Checkpoint the log once, regardless of whether or not there has been activity since the last checkpoint and then exit.

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-k**

> Checkpoint the database at least as often as every kbytes of log file are written.

**-L**

> Log the execution of the db\_checkpoint utility to the specified file in the following format, where ### is the process ID, and the date is the time the utility was started.

> > db\_checkpoint: ### Wed Jun 15 01:23:45 EDT 1995

> This file will be removed if the db\_checkpoint utility exits gracefully.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-p**

> Checkpoint the database at least every min minutes if there has been any activity since the last checkpoint.

**-V**

> Write the library version number to the standard output, and exit.

**-v**

> Write the time of each checkpoint attempt to the standard output.

At least one of the -1, -k, and -p options must be specified.

The db\_checkpoint utility uses a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment, db\_checkpoint should always be given the chance to detach from the environment and exit gracefully. To cause db\_checkpoint to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The db\_checkpoint utility does not attempt to create the Berkeley DB shared memory regions if they do not already exist. The application that creates the region should be started first, and once the region is created, the db\_checkpoint utility should be started.

The DB\_ENV-&gt;txn\_checkpoint method is the underlying method used by the db\_checkpoint utility. See the db\_checkpoint utility source code for an example of using DB\_ENV-&gt;txn\_checkpoint in a IEEE/ANSI Std 1003.1 (POSIX) environment.

The
**db\_checkpoint**
utility exits 0 on success, and &gt;0 if an error occurs.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SEE ALSO

db\_archive(1),
db\_deadlock(1),
db\_dump(1),
db\_load(1),
db\_printlog(1),
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
