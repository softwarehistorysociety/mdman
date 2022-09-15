DOT\_CLEAN(1) - General Commands Manual

# NAME

**dot\_clean** - Merge .\_\* files with corresponding native files.

# SYNOPSIS

**dot\_clean**
\[**-fmnsv**]
\[**-&#45;keep=\[mostrecent|dotbar|native]**]
\[*dir*&nbsp;*...*]

# DESCRIPTION

For each
dir
,
**dot\_clean**
recursively merges all .\_\* files with their corresponding native files according to the rules specified with the given arguments.  By default, if there is an attribute on the native file that is also present in the .\_ file, the most recent attribute will be used.

If no operands are given, a usage message is output.
If more than one directory is given, directories are merged in the order in which they are specified.

# OPTIONS

**-f**

> Flat merge.  Do not recursively merge all directories in the given
> *dir*.
> This is off by default.

**-h**

> Help. Prints verbose usage message.

**-m**

> Always delete dot underbar files.

**-n**

> Delete dot underbar file if there is no matching native file.

**-s**

> Follow symbolic links.  This will follow symbolic dot underbar files when they are found.

**-v**

> Print verbose output.

**-&#45;keep=mostrecent**

> The default option.  If an attribute is associated with a data fork, use that.  Otherwise, use information stored in the AppleDouble file.  Note that the native fork's data is preferred even if the data in the AppleDouble file is newer.

**-&#45;keep=dotbar**

> Always use information stored in the AppleDouble file, replacing any extended attributes associated with the native file.

**-&#45;keep=native**

> Always use the information associated with the data fork, ignoring any AppleDouble files.

# EXAMPLES

The following is how to do an
**dot\_clean**
merge on the mounted volume test, always using the dot underbar information.

	dot_clean --keep=dotbar /Volumes/test

# DIAGNOSTICS

The **dot\_clean** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# BUGS

None known.

macOS 12.6 - Sept 27, 2012
