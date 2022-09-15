DITTO(1) - General Commands Manual

# NAME

**ditto** - copy directory hierarchies, create and extract archives

# SYNOPSIS

**ditto**
\[**-v**]
\[**-V**]
\[**-X**]
\[&lt;options&gt;]
*src&nbsp;...&nbsp;dst\_directory*  
**ditto**
\[**-v**]
\[**-V**]
\[&lt;options&gt;]
*src\_file&nbsp;dst\_file*  
**ditto**
**-c**
\[**-z**&nbsp;|&nbsp;**-j**&nbsp;|&nbsp;**-k**]
\[**-v**]
\[**-V**]
\[**-X**]
\[&lt;options&gt;]
*src&nbsp;dst\_archive*  
**ditto**
**-x**
\[**-z**&nbsp;|&nbsp;**-j**&nbsp;|&nbsp;**-k**]
\[**-v**]
\[**-V**]
\[&lt;options&gt;]
*src\_archive&nbsp;...&nbsp;dst\_directory*  
**ditto**
**-h**&nbsp;|&nbsp;**-&#45;help**

# DESCRIPTION

In its first form,
**ditto**
copies one or more source files or directories to a destination
directory.  If the destination directory does not exist it will be
created before the first source is copied.  If the destination
directory already exists then the source directories are merged
with the previous contents of the destination.

In its second form,
**ditto**
copies a file to the supplied
*dst\_file*
pathname.

The next two forms reflect
**ditto**'s
ability to create and extract
archives.  These archives can be either CPIO format (preferred for unix
content) or PKZip (for Windows compatibility).
*src\_archive*
(and
*dst\_archive*)
can be the single character '-', causing ditto to read (write) archive data
from stdin (or to stdout, respectively).

**ditto**
follows symbolic links provided as arguments but does not follow any links
as it traverses the source or destination hierarchies.
**ditto**
overwrites existing files, symbolic links, and devices in the destination
when these are copied from a source.  The resulting files, links, and
devices will have the same mode, access time, modification time, owner,
and group as the source items from which they are copied.  Pipes, sockets,
and files with names beginning with .nfs or .afpDeleted will be ignored.
**ditto**
does not modify the mode, owner, group, extended attributes, or ACLs of existing
directories in the
destination.  Files and symbolic links cannot overwrite directories or
vice-versa.

**ditto**
can be used to "thin" Universal Mach-O binaries during a copy.
**ditto**
can also copy files selectively based on the contents of a BOM
("Bill of Materials") file.
**ditto**
preserves file hard links (but not directory hard links) present in the source directories and preserves
setuid and setgid modes when run as the superuser.

**ditto**
will preserve resource forks and HFS meta-data information
when copying unless instructed otherwise using **-&#45;norsrc**
. **-&#45;norsrc**
will disable copy of resource forks, extended attributes, Access Control Lists (ACLs), as well as quarantine bits.
`DITTONORSRC`
can be set in the environment as an alias to **-&#45;norsrc** **-&#45;noextattr** **-&#45;noacl** **-&#45;noqtn**
on the command line. However, each option can be individually turned on or off, see the OPTIONS section for more details.

# OPTIONS

**-h**

> Print full usage.

**-v**

> Print a line of output to stderr for each source directory copied.

**-V**

> Print a line of output to stderr for every file, symbolic link, and device copied.

**-X**

> When copying one or more source directories, do not descend into directories
> that have a different device ID.

**-c**

> Create an archive at the destination path.  The default format is CPIO, unless
> **-k**
> is given.
> CPIO archives should be stored in files with names ending in .cpio.
> Compressed CPIO archives should be stored in files with names ending in
> .cpgz.

**-z**

> Create compressed CPIO archives, using
> gzip(1)
> compression.

**-j**

> Create compressed CPIO archives, using
> bzip2(1)
> compression.

**-x**

> Extract the archives given as source arguments. The format is assumed to
> be CPIO, unless
> **-k**
> is given.  Compressed CPIO is automatically handled.

**-k**

> Create or extract from a PKZip archive instead of the default CPIO.
> PKZip archives should be stored in filenames ending in .zip.

**-&#45;keepParent**

> When creating an archive, embed the parent directory name
> *src*
> in
> *dst\_archive*.

**-&#45;arch** *arch*

> Thin Universal binaries to the specified
> architecture.  If multiple **-&#45;arch**
> options are specified then the resulting destination file will contain
> each of the specified architectures (if they are present in the source
> file).
> *arch*
> should be specified as "i386", "x86\_64", etc.

**-&#45;bom** *bom*

> Copy only files, links, devices, and directories that are present in the
> specified BOM.

**-&#45;rsrc**

> Preserve resource forks and HFS meta-data.
> **ditto**
> will store this data in Carbon-compatible .\_ AppleDouble files on
> filesystems that do not natively support resource forks.  As of Mac OS X 10.4, **-&#45;rsrc**
> is default behavior.

**-&#45;norsrc**

> Do not preserve resource forks and HFS meta-data.  If both **-&#45;norsrc**
> and **-&#45;rsrc**
> are passed, whichever is passed last will take precedence.  Both options
> override
> `DITTONORSRC`. Unless explicitly specified, **-&#45;norsrc**
> also implies **-&#45;noextattr**
> and **-&#45;noacl**
> to match the behavior of Mac OS X 10.4.

**-&#45;extattr**

> Preserve extended attributes (requires **-&#45;rsrc**).
> As of Mac OS X 10.5, **-&#45;extattr**
> is the default.

**-&#45;noextattr**

> Do not preserve extended attributes (requires **-&#45;norsrc**).

**-&#45;qtn**

> Preserve quarantine information.
> As of Mac OS X 10.5, **-&#45;qtn**
> is the default.

**-&#45;noqtn**

> Do not preserve quarantine information.

**-&#45;acl**

> Preserve Access Control Lists (ACLs).
> As of Mac OS X 10.5, **-&#45;acl**
> is the default.

**-&#45;noacl**

> Do not preserve ACLs.

**-&#45;nocache**

> Do not perform copies using the Mac OS X Unified Buffer Cache. Files read
> and written will not be cached, although if the file is already present
> in the cache, the cached information will be used.

**-&#45;hfsCompression**

> When copying files or extracting content from an archive, if the destination
> is an HFS+ volume that supports compression, all the content will be compressed
> if appropriate. This is only supported on Mac OS X 10.6 or later, and is only
> intended to be used in installation and backup scenarios that involve system
> files. Since files using HFS+ compression are not readable on versions of
> Mac OS X earlier than 10.6, this flag should not be used when dealing with
> non-system files or other user-generated content that will be used on a
> version of Mac OS X earlier than 10.6.

**-&#45;nohfsCompression**

> Do not compress files with HFS+ compression when copying or extracting content
> from an archive unless the content is already compressed with HFS+ compression.
> This flag is only supported on Mac OS X 10.6 or later. **-&#45;nohfsCompression**
> is the default.

**-&#45;preserveHFSCompression**

> When copying files to an HFS+ volume that supports compression, ditto will
> preserve the compression of any source files that were using HFS+ compression.
> This flag is only supported on Mac OS X 10.6 or later. **-&#45;preserveHFSCompression**
> is the default.

**-&#45;nopreserveHFSCompression**

> Do not preserve HFS+ compression when copying files that are already compressed with
> HFS+ compression. This is only supported on Mac OS X 10.6 or later.

**-&#45;sequesterRsrc**

> When creating a PKZip archive, preserve resource forks and HFS meta-data
> in the subdirectory \_\_MACOSX.  PKZip extraction will automatically find
> these resources.

**-&#45;zlibCompressionLevel** *num*

> Sets the compression level to use when creating a PKZip archive. The compression
> level can be set from 0 to 9, where 0 represents no compression, and 9
> represents optimal (slowest) compression. By default, ditto will use the default compression
> level as defined by zlib.

**-&#45;password**

> When extracting a password-encrypted ZIP archive, you must specify --password to allow ditto
> to prompt for a password to use to extract the contents of the file. If this option is not
> provided, and a password-encrypted file is encountered, ditto will emit an error message.

# EXAMPLES

The command:

	ditto src_directory dst_directory

copies the contents of src\_directory into dst\_directory, creating
dst\_directory if it does not already exist.

The command:

	ditto src_directory dir/dst_directory

copies the contents of src\_directory into dir/dst\_directory, creating
dir and dst\_directory if they don't already exist.

The command:

	ditto src-1 ... src-n dst_directory

copies the contents of all of the src directories into dst\_directory,
creating dst\_directory if it does not already exist.

The command:

	ditto --arch ppc universal_file thin_file

copies the contents of universal\_file into thin\_file, thinning executable
code to ppc-only on the fly.

The command:

	ditto -c --norsrc Scripts -|ssh rhost ditto -x --norsrc - ./Scripts

copies Scripts, skipping any resources or meta-data, to rhost.

The command:

	pax -f archive.cpio

will list the files in the CPIO archive archive.cpio.

The command:

	pax -zf archive.cpgz

will list the files in the compressed CPIO archive archive.cpgz.

The command:

	ditto -c -k --sequesterRsrc --keepParent src_directory archive.zip

will create a PKZip archive similarly to the Finder's Compress functionality.

The command:

	unzip -l archive.zip

will list the files in the PKZip archive archive.zip.

# ERRORS

**ditto**
returns 0 if everything is copied, otherwise non-zero.
**ditto**
almost never gives up, preferring to report errors along the way.
Diagnostic messages will be printed to standard error.

# ENVIRONMENT

`DITTOABORT`

> If the environment variable
> `DITTOABORT`
> is set,
> **ditto**
> will call
> abort(3)
> if it encounters a fatal error.

`DITTONORSRC`

> If
> `DITTONORSRC`
> is set but **-&#45;rsrc**, **-&#45;extattr**,
> and **-&#45;acl**
> are not specified,
> **ditto**
> will not preserve those additional types of metadata.

# BUGS

**ditto**
doesn't copy directories into directories in the same way as
cp(1).
In particular,

	ditto foo bar

will copy the contents of foo into bar, whereas

	cp -r foo bar

copies foo itself into bar. Though this is not a bug, some may
consider this bug-like behavior. **-&#45;keepParent**
for non-archive copies will eventually alleviate this problem.

# SEE ALSO

bom(5),
lsbom(8),
mkbom(8),
cpio(1),
zip(1),
gzip(1),
bzip2(1),
tar(1).

Mac OS X - December 19, 2008
