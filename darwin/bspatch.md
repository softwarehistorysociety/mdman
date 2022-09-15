BSPATCH(1) - General Commands Manual

# NAME

**bspatch** - apply a patch built with
bsdiff(1)

# SYNOPSIS

**bspatch**
*oldfile&nbsp;newfile&nbsp;patchfile*

# DESCRIPTION

The
**bspatch**
utility
generates
*newfile*
from
*oldfile*
and
*patchfile*
where
*patchfile*
is a binary patch built by
bsdiff(1).

The
**bspatch**
utility
uses memory equal to the size of
*oldfile*
plus the size of
*newfile*,
but can tolerate a very small working set without a dramatic loss
of performance.

# SEE ALSO

bsdiff(1)

# AUTHORS

Colin Percival &lt;[cperciva@FreeBSD.org](mailto:cperciva@FreeBSD.org)&gt;

# BUGS

The
**bspatch**
utility does not verify that
*oldfile*
is the correct source file for
*patchfile*.
Attempting to apply a patch to the wrong file will usually produce
garbage; consequently it is strongly recommended that users of
**bspatch**
verify that
*oldfile*
matches the source file from which
*patchfile*
was built, by comparing cryptographic hashes, for example.
Users may also wish to verify after running
**bspatch**
that
*newfile*
matches the target file from which
*was built.*

macOS 12.6 - May 18, 2003
