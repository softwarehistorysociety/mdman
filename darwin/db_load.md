db\_load(1) - General Commands Manual

# NAME

**db\_load**

# SYNOPSIS

**db\_load**
\[**-nTV**]
\[**-c**&nbsp;*name=value*]
\[**-f**&nbsp;*file*]
\[**-h**&nbsp;*home*]
\[**-P**&nbsp;*password*]
\[**-t**&nbsp;*btree*&nbsp;|&nbsp;*hash*&nbsp;|&nbsp;*queue*&nbsp;|&nbsp;*recno*]
file

# DESCRIPTION

The
**db\_load**
utility reads from the standard input and loads it into the database file. The database file is created if it does not already exist.

The input to
**db\_load**
must be in the output format specified by the db\_dump utility, utilities, or as specified for the -T below.

The options are as follows:

**-c**

> Specify configuration options ignoring any value they may have based on the input. The command-line format is name=value. See the Supported Keywords section below for a list of keywords supported by the -c option.

**-f**

> Read from the specified input file instead of from the standard input.

**-h**

> Specify a home directory for the database environment.

> If a home directory is specified, the database environment is opened using the Db.DB\_INIT\_LOCK, Db.DB\_INIT\_LOG, Db.DB\_INIT\_MPOOL, Db.DB\_INIT\_TXN, and Db.DB\_USE\_ENVIRON flags to DB\_ENV-&gt;open. (This means that db\_load can be used to load data into databases while they are in use by other processes.) If the DB\_ENV-&gt;open call fails, or if no home directory is specified, the database is still updated, but the environment is ignored; for example, no locking is done.

**-n**

> Do not overwrite existing keys in the database when loading into an already existing database. If a key/data pair cannot be loaded into the database for this reason, a warning message is displayed on the standard error output, and the key/data pair are skipped.

**-P**

> Specify an environment password. Although Berkeley DB utilities overwrite password strings as soon as possible, be aware there may be a window of vulnerability on systems where unprivileged users can see command-line arguments or where utilities are not able to overwrite the memory containing the command-line arguments.

**-T**

> The -T option allows non-Berkeley DB applications to easily load text files into databases.

> If the database to be created is of type Btree or Hash, or the keyword keys is specified as set, the input must be paired lines of text, where the first line of the pair is the key item, and the second line of the pair is its corresponding data item. If the database to be created is of type Queue or Recno and the keyword keys is not set, the input must be lines of text, where each line is a new data item for the database.

> A simple escape mechanism, where newline and backslash ( characters are special, is applied to the text input. Newline characters are interpreted as record separators. Backslash characters in the text will be interpreted in one of two ways: If the backslash character precedes another backslash character, the pair will be interpreted as a literal backslash. If the backslash character precedes any other character, the two characters following the backslash will be interpreted as a hexadecimal specification of a single character; for example, &#160;a is a newline character in the ASCII character set.

> For this reason, any backslash or newline characters that naturally occur in the text input must be escaped to avoid misinterpretation by db\_load.

> If the -T option is specified, the underlying access method type must be specified using the -t option.

**-t**

> Specify the underlying access method. If no -t option is specified, the database will be loaded into a database of the same type as was dumped; for example, a Hash database will be created if a Hash database was dumped.

> Btree and Hash databases may be converted from one to the other. Queue and Recno databases may be converted from one to the other. If the -k option was specified on the call to db\_dump then Queue and Recno databases may be converted to Btree or Hash, with the key being the integer record number.

**-V**

> Write the library version number to the standard output, and exit.

The db\_load utility may be used with a Berkeley DB environment (as described for the -h option, the environment variable DB\_HOME, or because the utility was run in a directory containing a Berkeley DB environment). In order to avoid environment corruption when using a Berkeley DB environment, db\_load should always be given the chance to detach from the environment and exit gracefully. To cause db\_load to release all environment resources and exit cleanly, send it an interrupt signal (SIGINT).

The db\_load utility exits 0 on success, 1 if one or more key/data pairs were not loaded into the database because the key already existed, and &gt;1 if an error occurs.

# EXAMPLES

The
**db\_load**
utility can be used to load text files into databases. For example, the following command loads the standard UNIX /etc/passwd file into a database, with the login name as the key item and the entire password entry as the data item:

> awk -F: '{print $1; print $0}' &lt; /etc/passwd |
>     sed 's/&#92;/&#92;&#92;/g' | db\_load -T -t hash passwd.db

Note that backslash characters naturally occurring in the text are escaped to avoid interpretation as escape characters by db\_load.

# ENVIRONMENT

`DB_HOME`

> If the -h option is not specified and the environment variable DB\_HOME is set, it is used as the path of the database home, as described in DB\_ENV-&gt;open.

# SUPPORTED KEYWORDS

The following keywords are supported for the -c command-line option to the
**db\_load**
utility. See DB-&gt;open for further discussion of these keywords and what values should be specified.

The parenthetical listing specifies how the value part of the name=value pair is interpreted. Items listed as (boolean) expect value to be 1 (set) or 0 (unset). Items listed as (number) convert value to a number. Items listed as (string) use the string value without modification.

bt\_minkey (number)

> The minimum number of keys per page.

chksum (boolean)

> Enable page checksums.

database (string)

> The database to load.

db\_lorder (number)

> The byte order for integers in the stored database metadata.

db\_pagesize (number)

> The size of database pages, in bytes.

duplicates (boolean)

> The value of the Db.DB\_DUP flag.

dupsort (boolean)

> The value of the Db.DB\_DUPSORT flag.

extentsize (number)

> The size of database extents, in pages, for Queue databases configured to use extents.

h\_ffactor (number)

> The density within the Hash database.

h\_nelem (number)

> The size of the Hash database.

keys (boolean)

> Specify whether keys are present for Queue or Recno databases.

re\_len (number)

> Specify fixed-length records of the specified length.

re\_pad (string)

> Specify the fixed-length record pad character.

recnum (boolean)

> The value of the Db.DB\_RECNUM flag.

renumber (boolean)

> The value of the Db.DB\_RENUMBER flag.

subdatabase (string)

> The subdatabase to load.

# SEE ALSO

db\_archive(1),
db\_checkpoint(1),
db\_deadlock(1),
db\_dump(1),
db\_printlog(1),
db\_recover(1),
db\_stat(1),
db\_upgrade(1),
db\_verify(1)

Darwin - December 3, 2003
