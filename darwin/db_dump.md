db\_dump(1) - General Commands Manual

# NAME

**db\_dump**

# SYNOPSIS

**db\_dump**
\[**-klNpRrV**]
\[**-d**&nbsp;*ahr*]
\[**-f**&nbsp;*output*]
\[**-h**&nbsp;*home*]
\[**-P**&nbsp;*password*]
\[**-s**&nbsp;*database*]
file

# DESCRIPTION

The
**db\_dump**
utility reads the database file file and writes it to the standard output using a portable flat-text format understood by the db\_load utility. The file argument must be a file produced using the Berkeley DB library functions.

The options are as follows:

**-d**

> Dump the specified database in a format helpful for debugging the Berkeley DB library routines.

> a

> > Display all information.

> h

> > Display only page headers.

> r

> > Do not display the free-list or pages on the free list. This mode is used by the recovery tests.

> *The output format of the -d option is not standard and may change, without notice, between releases of the Berkeley DB library.*

**-f**

> Write to the specified file instead of to the standard output.

**-h**

> Specify a home directory for the database environment; by default, the current working directory is used.

**-k**

> Dump record numbers from Queue and Recno databases as keys.

**-l**

> List the databases stored in the file.

**-N**

> Do not acquire shared region mutexes while running. Other problems, such as potentially fatal errors in Berkeley DB, will be ignored as well. This option is intended only for debugging errors, and should not be used under any other circumstances.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-p**

> If characters in either the key or data items are printing characters (as defined by isprint(3)), use printing characters in file to represent them. This option permits users to use standard text editors and tools to modify the contents of databases.

> Note: different systems may have different notions about what characters are considered
> *printing characters,*
> and databases dumped in this manner may be less portable to external systems.

**-R**

> Aggressively salvage data from a possibly corrupt file. The -R flag differs from the -r option in that it will return all possible data from the file at the risk of also returning already deleted or otherwise nonsensical items. Data dumped in this fashion will almost certainly have to be edited by hand or other means before the data is ready for reload into another database

**-r**

> Salvage data from a possibly corrupt file. When used on a uncorrupted database, this option should return equivalent data to a normal dump, but most likely in a different order.

**-s**

> Specify a single database to dump. If no database is specified, all databases in the database file are dumped.

**-V**

> Write the library version number to the standard output, and exit.

Dumping and reloading Hash databases that use user-defined hash functions will result in new databases that use the default hash function. Although using the default hash function may not be optimal for the new database, it will continue to work correctly.

Dumping and reloading Btree databases that use user-defined prefix or comparison functions will result in new databases that use the default prefix and comparison functions.
*In this case, it is quite likely that the database will be damaged beyond repair permitting neither record storage or retrieval.*

The only available workaround for either case is to modify the sources for the db\_load utility to load the database using the correct hash, prefix, and comparison functions.

The
**db\_dump**
utility output format is documented in the Dump Output Formats section of the Berkeley DB Reference Guide.

The
**db\_dump**
utility may be used with a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment,
**db\_dump**
should always be given the chance to detach from the environment and exit gracefully. To cause
**db\_dump**
to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

Even when using a Berkeley DB database environment, the
**db\_dump**
utility does not use any kind of database locking if it is invoked with the -d, -R, or -r arguments. If used with one of these arguments, the
**db\_dump**
utility may only be safely run on databases that are not being modified by any other process; otherwise, the output may be corrupt.

The
**db\_dump**
utility exits 0 on success, and &gt;0 if an error occurs.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SEE ALSO

db\_archive(1),
db\_checkpoint(1),
db\_deadlock(1),
db\_load(1),
db\_printlog(1),
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
