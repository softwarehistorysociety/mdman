db\_printlog(1) - General Commands Manual

# NAME

**db\_printlog**

# SYNOPSIS

**db\_printlog**
\[**-NrV**]
\[**-h**&nbsp;*home*]
\[**-P**&nbsp;*password*]

# DESCRIPTION

The
**db\_printlog**
utility is a debugging utility that dumps Berkeley DB log files in a human-readable format.

The options are as follows:

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-N**

> Do not acquire shared region mutexes while running. Other problems, such as potentially fatal errors in Berkeley DB, will be ignored as well. This option is intended only for debugging errors, and should not be used under any other circumstances.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-r**

> Read the log files in reverse order.

**-V**

> Write the library version number to the standard output, and exit.

For more information on the
**db\_printlog**
output and using it to debug applications, see Reviewing Berkeley DB log files.

The
**db\_printlog**
utility uses a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment,
**db\_printlog**
should always be given the chance to detach from the environment and exit gracefully. To cause
**db\_printlog**
to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The
**db\_printlog**
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
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
