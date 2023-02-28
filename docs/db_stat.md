db\_stat(1) - General Commands Manual

# NAME

**db\_stat**

# SYNOPSIS

**db\_stat&nbsp;**-d**&nbsp;*file*&zwnj;**
\[**-fN**]
\[**-h**&nbsp;*home*]
\[**-P**&nbsp;*password*]
\[**-s**&nbsp;*database*]  
**db\_stat**
\[**-celmNrtVZ**]
\[**-C**&nbsp;*Aclmop*]
\[**-h**&nbsp;*home*]
\[**-M**&nbsp;*Ahm*]
\[**-P**&nbsp;*password*]

# DESCRIPTION

The
**db\_stat**
utility utility displays statistics for Berkeley DB environments.

The options are as follows:

**-C**

> Display internal information about the lock region. (The output from this option is often both voluminous and meaningless, and is intended only for debugging.)

> A

> > Display all information.

> c

> > Display lock conflict matrix.

> l

> > Display lockers within hash chains.

> m

> > Display region memory information.

> o

> > Display objects within hash chains.

> p

> > Display lock region parameters.

**-c**

> Display lock region statistics, as described in DB\_ENV-&gt;lock\_stat.

**-d**

> Display database statistics for the specified file, as described in DB-&gt;stat.

> If the database contains multiple databases and the -s flag is not specified, the statistics are for the internal database that describes the other databases the file contains, and not for the file as a whole.

**-e**

> Display current environment statistics.

**-f**

> Display only those database statistics that can be acquired without traversing the database.

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-l**

> Display log region statistics, as described in DB\_ENV-&gt;log\_stat.

**-M**

> Display internal information about the shared memory buffer pool. (The output from this option is often both voluminous and meaningless, and is intended only for debugging.)

> A

> > Display all information.

> h

> > Display buffers within hash chains.

> m

> > Display region memory information.

**-m**

> Display shared memory buffer pool statistics, as described in DB\_ENV-&gt;memp\_stat.

**-N**

> Do not acquire shared region mutexes while running. Other problems, such as potentially fatal errors in Berkeley DB, will be ignored as well. This option is intended only for debugging errors, and should not be used under any other circumstances.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-r**

> Display replication statistics, as described in DB\_ENV-&gt;rep\_stat.

**-s**

> Display statistics for the specified database contained in the file specified with the -d flag.

**-t**

> Display transaction region statistics, as described in DB\_ENV-&gt;txn\_stat.

**-V**

> Write the library version number to the standard output, and exit.

**-Z**

> Reset the statistics after reporting them; valid only with the -c, -e, -l, -m, and -t options.

Values normally displayed in quantities of bytes are displayed as a combination of gigabytes (GB), megabytes (MB), kilobytes (KB), and bytes (B). Otherwise, values smaller than 10 million are displayed without any special notation, and values larger than 10 million are displayed as a number followed by "M".

The
**db\_stat**
utility may be used with a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment,
**db\_stat**
should always be given the chance to detach from the environment and exit gracefully. To cause
**db\_stat**
to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The
**db\_stat**
utility exits 0 on success, and &gt;0 if an error occurs.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SEE ALSO

db\_archive(1),
db\_checkpoint(1),
db\_deadlock(1),
db\_dump(1),
db\_load(1),
db\_printlog(1),
db\_recover(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
