APPLESINGLE(1) - General Commands Manual

# NAME

**applesingle**,
**binhex**,
**macbinary** - encode and decode files

# SYNOPSIS

**&lt;tool&gt;**
probe
*file&nbsp;...*  
**&lt;tool&gt;**
\[decode]
\[**-c**]
\[**-fv**]
\[**-C**&nbsp;*dir*]
\[**-o**&nbsp;*outfile*]
\[*file&nbsp;...*]  
**&lt;tool&gt;**
**-h**&nbsp;|&nbsp;**-V**

**applesingle**
encode
\[**-cfv**]
\[**-s**&nbsp;*suf*]
\[**-C**&nbsp;*dir*]
\[**-o**&nbsp;*outfile*]
*file&nbsp;...*  
**binhex**
encode
\[**-R**]
\[**-cfv**]
\[**-s**&nbsp;*suf*]
\[**-C**&nbsp;*dir*]
\[**-o**&nbsp;*outfile*]
*file&nbsp;...*  
**macbinary**
encode
\[**-t**&nbsp;*1-3*]
\[**-cfv**]
\[**-s**&nbsp;*suf*]
\[**-C**&nbsp;*dir*]
\[**-o**&nbsp;*outfile*]
*file&nbsp;...*

# DESCRIPTION

**applesingle**,
**binhex**,
**macbinary**
are implemented as a single tool with multiple names.  All invocations
support the three verbs
**encode**,
**decode**,
and
**probe**.

If multiple files are passed to
**probe**,
the exit status will be non-zero only if
**all**
files contain data in the specified encoding.

# OPTIONS

**-f**, **--force**

> perform the operation even if the output file already exists

**-h**, **--help**

> display version and usage, then quit

**-v**, **--verbose**

> be verbose

**-V**, **--version**

> display version, then quit

**-c**, **--pipe**, **--from-stdin**, **--to-stdout**

> For
> **decode**,
> read encoded data from the standand input.  For
> **encode**,
> write encoded data to the standard output.  Currently, "plain" data must
> be written to and from specified filenames (see also
> mount\_fdesc(8)).

**-C**, **--directory** *dir*

> create output files in
> *dir*

**-o**, **--rename** *name*

> Use
> *name*
> for output, overriding any stored or default name.  For
> **encode**,
> the appropriate suffix will be added to
> *name*.
> **-o**
> implies only one file to be encoded or decoded.

**-s**, **--suffix** *.suf*

> override the default suffix for the given encoding

**-R**, **--no-runlength-encoding**

> don't use BinHex runlength compression when encoding

**-t**, **--type** *1-3*

> Specify MacBinary encoding type.  Type 1 is undesirable because it has
> neither a checksum nor a signature and is thus difficult to recognize.

# DIAGNOSTICS

In general, the tool returns a non-zero exit status if it fails.

Darwin - 14 November 2005
