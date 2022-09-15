db\_archive(1) - General Commands Manual

# NAME

**db\_archive**

# SYNOPSIS

**db\_archive**
\[**-adlsVv**]
\[**-h**&nbsp;*home*]
\[**-P**&nbsp;*password*]

# DESCRIPTION

The
**db\_archive**
utility writes the pathnames of log files that are no longer in use (for example, no longer involved in active transactions), to the standard output, one pathname per line. These log files should be written to backup media to provide for recovery in the case of catastrophic failure (which also requires a snapshot of the database files), but they may then be deleted from the system to reclaim disk space.

The options are as follows:

**-a**

> Write all pathnames as absolute pathnames, instead of relative to the database home directories.

**-d**

> Remove log files that are no longer needed; no filenames are written. Automatic log file removal is likely to make catastrophic recovery impossible.

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-l**

> Write out the pathnames of all the database log files, whether or not they are involved in active transactions.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-s**

> Write the pathnames of all the database files that need to be archived in order to recover the database from catastrophic failure. If any of the database files have not been accessed during the lifetime of the current log files, db\_archive will not include them in this output.

> It is possible that some of the files to which the log refers have since been deleted from the system. In this case, db\_archive will ignore them. When db\_recover is run, any files to which the log refers that are not present during recovery are assumed to have been deleted and will not be recovered.

**-V**

> Write the library version number to the standard output, and exit.

**-v**

> Run in verbose mode, listing the checkpoints in the log files as they are reviewed.

Log cursor handles (returned by the DB\_ENV-&gt;log\_cursor method) may have open file descriptors for log files in the database environment. Also, the Berkeley DB interfaces to the database environment logging subsystem (for example, DB\_ENV-&gt;log\_put and DB\_TXN-&gt;abort) may allocate log cursors and have open file descriptors for log files as well. On operating systems where filesystem related system calls (for example, rename and unlink on Windows/NT) can fail if a process has an open file descriptor for the affected file, attempting to move or remove the log files listed by db\_archive may fail. All Berkeley DB internal use of log cursors operates on active log files only and furthermore, is short-lived in nature. So, an application seeing such a failure should be restructured to close any open log cursors it may have, and otherwise to retry the operation until it succeeds. (Although the latter is not likely to be necessary; it is hard to imagine a reason to move or rename a log file in which transactions are being logged or aborted.)

The db\_archive utility uses a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment, db\_archive should always be given the chance to detach from the environment and exit gracefully. To cause db\_archive to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The DB\_ENV-&gt;log\_archive method is the underlying method used by the db\_archive utility. See the db\_archive utility source code for an example of using DB\_ENV-&gt;log\_archive in a IEEE/ANSI Std 1003.1 (POSIX) environment.

The
**db\_archive**
utility exits 0 on success, and &gt;0 if an error occurs.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SEE ALSO

db\_checkpoint(1),
db\_deadlock(1),
db\_dump(1),
db\_load(1),
db\_printlog(1),
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
