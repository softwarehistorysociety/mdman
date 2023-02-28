KDESTROY(1) - General Commands Manual

# NAME

**kdestroy** - remove one credential or destroy the current ticket file

# SYNOPSIS

**kdestroy**
\[**-c**&nbsp;*cachefile*]
\[**--credential=**&zwnj;*principal*]
\[**--principal=**&zwnj;*principal*]
\[**--cache=**&zwnj;*type:name*]
\[**-A**&nbsp;|&nbsp;**-a**&nbsp;|&nbsp;**--all**]
\[**--no-unlog**]
\[**--no-delete-v4**]
\[**--version**]
\[**--help**]

# DESCRIPTION

**kdestroy**
removes one credential or the current set of tickets.

Supported options:

**-credential=**&zwnj;*principal*

> remove
> *principal*
> from the credential cache if it exists.

**-p** *principal*

**-principal=**&zwnj;*principal*

> The cache with client principal to remove.

**-c** *cachefile*

**-cache=**&zwnj;*type:name*

> The cache to remove. If the name is path-like, the cache type cache can be omitted.

**-A**

**-a**

**-&#45;all**

> remove all credential caches.

**-&#45;no-unlog**

> Do not remove AFS tokens.

**-&#45;no-delete-v4**

> Do not remove v4 tickets.

# SEE ALSO

kinit(1),
klist(1)

HEIMDAL - April 27, 2006
