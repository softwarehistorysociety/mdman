GZIP(1) - General Commands Manual

# NAME

**gzip**,
**gunzip**,
**zcat** - compression/decompression tool using Lempel-Ziv coding (LZ77)

# SYNOPSIS

**gzip**
\[**-cdfhkLlNnqrtVv**]
\[**-S**&nbsp;*suffix*]
*file*
\[*file*&nbsp;\[...]]  
**gunzip**
\[**-cfhkLNqrtVv**]
\[**-S**&nbsp;*suffix*]
*file*
\[*file*&nbsp;\[...]]  
**zcat**
\[**-fhV**]
*file*
\[*file*&nbsp;\[...]]

# DESCRIPTION

The
**gzip**
program compresses and decompresses files using Lempel-Ziv coding
(LZ77).
If no
*files*
are specified,
**gzip**
will compress from standard input, or decompress to standard output.
When in compression mode, each
*file*
will be replaced with another file with the suffix, set by the
**-S** *suffix*
option, added, if possible.

In decompression mode, each
*file*
will be checked for existence, as will the file with the suffix
added.
Each
*file*
argument must contain a separate complete archive;
when multiple
*files*
are indicated, each is decompressed in turn.

In the case of
**gzcat**
the resulting data is then concatenated in the manner of
cat(1).

If invoked as
**gunzip**
then the
**-d**
option is enabled.
If invoked as
**zcat**
or
**gzcat**
then both the
**-c**
and
**-d**
options are enabled.

This version of
**gzip**
is also capable of decompressing files compressed using
compress(1),
bzip2(1),
*lzip*,
or
xz(1).

# OPTIONS

The following options are available:

**-1**, **-&#45;fast**

**-2**, **-3**, **-4**, **-5**, **-6**, **-7**, **-8**

**-9**, **-&#45;best**

> These options change the compression level used, with the
> **-1**
> option being the fastest, with less compression, and the
> **-9**
> option being the slowest, with optimal compression.
> The default compression level is 6.

**-c**, **-&#45;stdout**, **-&#45;to-stdout**

> This option specifies that output will go to the standard output
> stream, leaving files intact.

**-d**, **-&#45;decompress**, **-&#45;uncompress**

> This option selects decompression rather than compression.

**-f**, **-&#45;force**

> This option turns on force mode.
> This allows files with multiple links, symbolic links to regular files,
> overwriting of pre-existing files, reading from or writing to a terminal,
> and when combined with the
> **-c**
> option, allowing non-compressed data to pass through unchanged.

**-h**, **-&#45;help**

> This option prints a usage summary and exits.

**-k**, **-&#45;keep**

> This option prevents
> **gzip**
> from deleting input files after (de)compression.

**-L**, **--license**

> This option prints
> **gzip**
> license.

**-l**, **-&#45;list**

> This option displays information about the file's compressed and
> uncompressed size, ratio, uncompressed name.
> With the
> **-v**
> option, it also displays the compression method, CRC, date and time
> embedded in the file.

**-N**, **-&#45;name**

> This option causes the stored filename in the input file to be used
> as the output file.

**-n**, **-&#45;no-name**

> This option stops the filename and timestamp from being stored in
> the output file.

**-q**, **-&#45;quiet**

> With this option, no warnings or errors are printed.

**-r**, **-&#45;recursive**

> This option is used to
> **gzip**
> the files in a directory tree individually, using the
> fts(3)
> library.

**-S** *suffix*, **-&#45;suffix** *suffix*

> This option changes the default suffix from .gz to
> *suffix*.

**-t**, **-&#45;test**

> This option will test compressed files for integrity.

**-V**, **-&#45;version**

> This option prints the version of the
> **gzip**
> program.

**-v**, **-&#45;verbose**

> This option turns on verbose mode, which prints the compression
> ratio for each file compressed.

# ENVIRONMENT

If the environment variable
`GZIP`
is set, it is parsed as a white-space separated list of options
handled before any options on the command line.
Options on the command line will override anything in
`GZIP`.

# EXIT STATUS

The
**gzip**
utility exits&#160;0 on success,
1 on errors,
and 2 if a warning occurs.

# SIGNALS

**gzip**
responds to the following signals:

`SIGINFO`

> Report progress to standard error.

# SEE ALSO

bzip2(1),
compress(1),
xz(1),
fts(3),
zlib(3)

# HISTORY

The
**gzip**
program was originally written by Jean-loup Gailly, licensed under
the GNU Public Licence.
Matthew R. Green wrote a simple front end for
NetBSD 1.3
distribution media, based on the freely re-distributable zlib library.
It was enhanced to be mostly feature-compatible with the original
GNU
**gzip**
program for
NetBSD 2.0.

This implementation of
**gzip**
was ported based on the
NetBSD
**gzip**
version 20181111,
and first appeared in
FreeBSD 7.0.

# AUTHORS

This implementation of
**gzip**
was written by
Matthew R. Green &lt;[mrg@eterna.com.au](mailto:mrg@eterna.com.au)&gt;
with unpack support written by
Xin LI &lt;[delphij@FreeBSD.org](mailto:delphij@FreeBSD.org)&gt;.

# BUGS

According to RFC 1952, the recorded file size is stored in a 32-bit
integer, therefore, it cannot represent files larger than 4GB.
This limitation also applies to
**-l**
option of
**gzip**
utility.

macOS 12.6 - January 7, 2019
