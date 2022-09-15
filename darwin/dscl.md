dscl(1) - General Commands Manual

# NAME

**dscl** - Directory Service command line utility

# SYNOPSIS

**dscl**
\[options]
\[*datasource*&nbsp;\[command]]

options:

**-p**

> prompt for password

**-u**&nbsp;*user*

> authenticate as user

**-P**&nbsp;*password*

> authentication password

**-f**&nbsp;*filepath*

> targeted local node database file path

**-raw**

> don't strip off prefix from DirectoryService API constants

**-plist**

> print out record(s) or attribute(s) in XML plist format

**-url**

> print record attribute values in URL-style encoding

**-q**

> quiet - no interactive prompt

commands:

**-read**&nbsp;\[*path*&nbsp;\[*key*&nbsp;`...`]]  
**-readall**&nbsp;\[*path*&nbsp;\[*key*&nbsp;`...`]]  
**-readpl**&nbsp;*path*&nbsp;*key*&nbsp;*plist\_path*  
**-readpli**&nbsp;*path*&nbsp;*key*&nbsp;*value\_index*&nbsp;*plist\_path*  
**-list**&nbsp;*path*&nbsp;\[key]  
**-search**&nbsp;*path&nbsp;key&nbsp;val*  
**-create**&nbsp;*record\_path*
\[*key*
\[*val*&nbsp;`...`]]  
**-createpl**&nbsp;*record\_path*&nbsp;*key*&nbsp;*plist\_path*&nbsp;*val1*&nbsp;\[*val2*&nbsp;`...`]  
**-createpli**&nbsp;*record\_path*&nbsp;*key*&nbsp;*value\_index*&nbsp;*plist\_path*&nbsp;*val1*&nbsp;\[*val2*&nbsp;`...`]  
**-append**&nbsp;*record\_path&nbsp;key&nbsp;val*&nbsp;`...`  
**-merge**&nbsp;*record\_path&nbsp;key&nbsp;val*&nbsp;`...`  
**-delete**&nbsp;*path*
\[*key*&nbsp;\[*val*&nbsp;`...`]]  
**-deletepl**&nbsp;*record\_path*&nbsp;*key*&nbsp;*plist\_path*&nbsp;\[val&nbsp;`...`]  
**-deletepli**&nbsp;*record\_path*&nbsp;*key*&nbsp;*value\_index*&nbsp;*plist\_path*&nbsp;\[val&nbsp;`...`]  
**-change**&nbsp;*record\_path&nbsp;key&nbsp;old\_val&nbsp;new\_val*  
**-changei**&nbsp;*record\_path&nbsp;key&nbsp;val\_index&nbsp;new\_val*  
**-diff**&nbsp;*path1*&nbsp;*path2*&nbsp;\[*key*&nbsp;`...`]  
**-passwd**&nbsp;*user\_path*
\[*new\_password*&nbsp;|&nbsp;*old\_password&nbsp;new\_password*]

available only in interactive mode:

**-cd**&nbsp;*dir*  
**-pushd**&nbsp;\[*dir*]  
**-popd**  
**-auth**&nbsp;\[*user*&nbsp;\[*password*]]  
**-authonly**&nbsp;\[*user*&nbsp;\[*password*]]  
**-quit**

# DESCRIPTION

**dscl**
is a general-purpose utility for operating on Directory Service directory nodes.  Its commands allow one to create, read, and manage Directory Service data.  If invoked without any commands,
**dscl**
runs in an interactive mode, reading commands from standard input.  Interactive processing is terminated by the
*quit*
command.  Leading dashes ("-") are optional for all commands.

**dscl**
operates on a datasource specified on the command line.  This may be a node name or a Mac OS X Server (10.2 or later) host specified by DNS hostname or IP address.  Node names may be absolute paths beginning with a slash ("/"), or relative domain paths beginning with a dot (".") character, which specifies the local domain, or "..", specifying the local domain's parent.  If the hostname or IP address form is used then the user must specify the
**-u**
option and either the
**-P**
or
**-p**
options to specify an administrative user and password on the remote host to authenticate with to the remote host. The exception to this is if "localhost" is specified.  Passing passwords on the command line is inherently insecure and can cause password exposure.  For better security do not provide the password as part of the command and you will be securely prompted.

The datasource may also be specified as "localonly" in which case a separate DirectoryService daemon process is activated which contains only the Local plugin for use by dscl.  If no file path is provided then access goes only to the registered local nodes on the system. However, if the
**-f**
option is specified then access is added to the local node "/Local/Target" which points to the database located at the provided filepath. One example is to provide the filepath of "/Volumes/Build100/var/db/dslocal/nodes/Default" and then access to that database is provided via the nodename "/Local/Target".

# PATH SPECIFICATION

There are two modes of operation when specifying paths to operate on. The two modes correspond to whether the datasource is a node or a host. In the case of specifying a node, the top level of paths will be record types. Example top level paths would be:

	/Users/alice

	/Groups/admin

In the case of specifying a host as a data source, the top level of paths correspond to Open Directory plug-ins and Search Paths. One can specify the plug-in to traverse to a node name, after which the paths are equivalent to the former usage. The following might be the equivalent paths as the above paths:

	/NetInfo/root/Users/alice

	/LDAPv3/10.0.1.42/Groups/admin

If path components contain keys or values with embedded slash characters, the slash characters must be escaped with a leading backslash character.  Since the shell also processes escape characters, an extra backslash is required to correctly specify an escape.  For example, to read a mount record with the name "ldapserver:/Users" in the "/Mounts" path, the following path would be used:

	**dscl** ` .` **-read** `/Mounts/ldaphost:\/Users`

All pathnames are case-sensitive.

# COMMANDS

The action of each command is described below.  Some commands have aliases.  For example, "cat" and "." are aliases for "read".  Command aliases are listed in parentheses.

## read (cat .)

Usage: read
\[*path* \[*key* `...`]]

Prints a directory.  The property key is followed by colon, then a space-separated list of the values for that property. If any value contains embedded spaces, the list will instead be displayed one entry per line, starting on the line after the key.

If The
**-raw**
flag for raw output has been given, then
*read*
prints the full DirectoryService API constant for record and attribute types.

If the
**-url**
flag has been specified then printed record path attribute values are encoded in the style of URLs. This is useful if a script or program is trying to process the output since values will not have any spaces or other control characters.

## readall

Usage: readall
\[*path* \[*key* `...`]]

*readall*
prints all the records of a given type.  The output of readall is formatted in the same way as
*read*
with a "-" on a line as a delimeter between records.

## readpl

Usage: readpl
*path* *key* *plist\_path*

Prints the contents of
*plist\_path*.
The
*plist\_path*
is followed by a colon, then a whitespace, and then the value for the path.

If the
*plist\_path*
is the key for a dictionary or array, the contents of it are displayed in plist form after the
*plist\_path*.
If
*plist\_path*
is the key for a string, number, bool, date, or data object, only the value is printed out after the
*plist\_path*.

## readpli

Usage: readpli
*path* *key* *value\_index* *plist\_path*

Prints the contents of
*plist\_path*
for the plist at
*value\_index*
of the key.
The
*plist\_path*
is followed by a colon, then a whitespace, and then the value for the path.

If the
*plist\_path*
is the key for a dictionary or array, the contents of it are displayed in plist form after the
*plist\_path*.
If
*plist\_path*
is the key for a string, number, bool, date, or data object, only the value is printed out after the
*plist\_path*.

## list (ls)

Usage: list
*path*

Lists the subdirectories of the given directory.  Subdirectories are listed one per line.  In the case of listing a search path, the names are preceded by an index number that can act as a shortcut and used in place of the name when specifying a path.

When used in interactive mode, the path is optional.  With no path given, the current directory will be used.

## search

*path key val*

Searches for records that match a pattern.  The search is rooted at the given path.  The path may be a node path or a record type path.  Valid keys are Directory Service record attribute types.

## create (mk)

Usage: create
*record\_path*
\[*key*
\[*val* `...`]]

Creates a record, property, or value.  If only a record path is given, the
*create*
command will create the record if it does not exist.  If a key is given, then a property with that key will be created.

WARNING - If a property with the given key already exists, it will be destroyed and a new property will be created in its place.  To add values to an existing property, use the
*append*
or
*merge*
commands.

If values are included in the command, these values will be set for the given key.

NOTE - Not all directory nodes support a property without a value. An error will be given if you attempt to create a property with no value in such a directory node.

## createpl

Usage: createpl
*record\_path* *key* *plist\_path* *val1* \[*val2* `...`]

Creates a string, or array of strings at
*plist\_path*.

If you are creating a value at the root of a plist that is an array, simply use "0" as the
*plist\_path*.

If only
*val1*
is specified, a string will be created at
*plist\_path*.
If
*val1 val2* `...`
are specified, an array of strings will be created at
*plist\_path*.

WARNING - If a value with the given
*plist\_path*
already exists, it will be destroyed and a new value will be created in its place.

## createpli

Usage: createpli
*record\_path* *key* *value\_index* *plist\_path* *val1* \[*val2* `...`]

Creates a string, or array of strings at
*plist\_path*
for the plist at
*value\_index*
of the key.

If you are creating a value at the root of a plist that is an array, simply use "0" as the
*plist\_path*.

If only
*val1*
is specified, a string will be created at
*plist\_path*.
If
*val1 val2* `...`
are specified, an array of strings will be created at
*plist\_path*.

WARNING - If a value with the given
*plist\_path*
already exists, it will be destroyed and a new value will be created in its place.

## append

Usage: append
*record\_path key val* `...`

Appends one or more values to a property in a given record.  The property is created if it does not exist.

## merge

Usage: merge
*record\_path key val* `...`

Appends one or more values to a property in a given directory if the property does not already have those values.  The property is created if it does not exist.

## change

Usage: change
*record\_path key old\_val new\_val*

Replaces the given old value in the list of values of the given key with the new value in the specified record.

## changei

Usage: changei
*path key index val*

Replaces the value at the given index in the list of values of the given key with the new value in the specified record.
*index*
is an integer value.  An index of 1 specifies the first value.  An index greater than the number of values in the list will result in an error.

## diff

Usage: diff
*path1 path2 key* `...`

Compares the data from path1 and path2 looking at the specified keys (or all if no keys are specified).

## delete (rm)

Usage: delete
*path*
\[*key* \[*val* `...`]]

Delete a directory, property, or value.  If a directory path is given, the
*delete*
command will delete the directory.  This can only be used on record type and record paths.  If a key is given, then a property with that key will be deleted.  If one or more values are given, those values will be removed from the property with the given key.

## deletepl

Usage: deletepl
*record\_path* *key* *plist\_path* \[val `...`]

Deletes a value in a plist.  If no values are given
*deletepl*
deletes the
*plist\_path*.
If one or more values are given,
*deletepl*
deletes the values within
*plist\_path*.

## deletepli

Usage: deletepli
*record\_path* *key* *value\_index* *plist\_path* \[val `...`]

Deletes a value for the plist at
*value\_index*
of the key.  If no values are given
*deletepli*
deletes the
*plist\_path*.
If one or more values are given,
*deletepli*
deletes the values within
*plist\_path*.

## passwd

Usage: passwd
*user\_path*
\[*new\_password* | *old\_password new\_password*]

Changes a password for a user. The user must be specified by full path, not just a username.  If you are authenticated to the node (either by specifying the
**-u**
and
**-P**
flags or by using the auth command when in interactive node) then you can simply specify a new password.  If you are not authenticated or if FileVault is enabled then the user's old password must be specified.  If passwords are not specified while in interactive mode, you will be prompted for them.  Passing these passwords on the command line is inherently insecure and can cause password exposure.  For better security do not provide the password as part of the command and you will be securely prompted.

# INTERACTIVE COMMANDS

## cd

Usage: cd dir

Sets the current directory.  Path names for other
**dscl**
commands may be relative to the current directory.

## pushd (pd)

Usage: pushd path

Similar to the pushd command commonly found in Unix shells.  When a path is specified it sets the current directory while pushing the previous directory on to the directory stack.  If no path is specified it exchanges the top two elements of the directory stack.  It will also print the final directory stack.

## popd

Usage: popd

Pops the directory stack and returns to the new top directory.  It will also print the final directory stack.

## auth (su)

Usage: auth
\[*user* \[*password*]]

Authenticate as the named user, or as "root" if no user is specified.  If a password is supplied, then that password is used for authentication, otherwise the command prompts for a password.

If
**dscl**
is run in host mode, then when this command is run the current directory must be in the subdirectories of a node.

## authonly

Usage: authonly
\[*user* \[*password*]]

Used to verify the password of a named user, or of "root" if no user is specified.  If a password is supplied, then that password is used for authentication, otherwise the command prompts for a password.

If
**dscl**
is run in host mode, then when this command is run the current directory must be in the subdirectories of a node.

## quit (q)

Usage: quit

Ends processing of interactive commands and terminates the program.

## command history

The up and down arrow keys will scan through the command history.

## tab completion

When pathnames are being typed, pressing the tab key will result in a search to auto-complete the typed partial subdirectory name. It will also attempt to correct capitilization in the process.

# EXAMPLES

**-view a record in the local directory node**

> dscl . -read /Users/www

**-create or replace the UserShell attribute value for the www user record**

> dscl . -create /Users/www UserShell /usr/bin/false

**-create or replace the test key of the mcx\_application\_data:loginwindow plist value for the MCXSettings attribute of the user1 user record**

> dscl . -createpl /Users/user1 MCXSettings mcx\_application\_data:loginwindow:test value

**-list the uniqueID values for all user records on a given node**

> dscl /LDAPv3/ldap.company.com -list /Users UniqueID

**-append a value that has spaces in it**

> dscl . -append /Users/www Comment "This is a comment"

# DIAGNOSTICS

**dscl**
will return -1 (255) on error.

# SEE ALSO

DirectoryService(8),
DirectoryServiceAttributes(7)

MacOSX - August 25, 2003
