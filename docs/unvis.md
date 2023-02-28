UNVIS(1) - General Commands Manual

# NAME

**unvis** - revert a visual representation of data back to original form

# SYNOPSIS

**unvis**
\[**-e**]
\[**-Hh**&nbsp;|&nbsp;**-m**]
\[*file&nbsp;...*]

# DESCRIPTION

**unvis**
is the inverse function of
vis(1).
It reverts
a visual representation of data back to its original form on standard output.

The options are as follows:

**-e**

> Don't decode &#92; escaped sequences.

**-H**

> Decode entity references and numeric character references from RFC 1866.
> (`VIS_HTTP1866`)

**-h**

> Decode using the URI encoding from RFC 1808.
> (`VIS_HTTP1808`)

**-m**

> Decode using mime style.
> (`VIS_MIMESTYLE`)

Mixing
**-h**
or
**-H**
with
**-m**
is not supported.

# SEE ALSO

vis(1),
unvis(3),
vis(3)

# HISTORY

The
**unvis**
command appears in
4\.4BSD.

macOS 12.6 - November 27, 2010
