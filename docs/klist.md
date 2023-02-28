KLIST(1) - General Commands Manual

# NAME

**klist** - list Kerberos credentials

# SYNOPSIS

**klist**
\[**-c**&nbsp;*cache*&nbsp;|&nbsp;**-&#45;cache=**&zwnj;*cache*]
\[**-s**&nbsp;|&nbsp;**-t**&nbsp;|&nbsp;**-&#45;test**]
\[**-T**&nbsp;|&nbsp;**-&#45;tokens**]
\[**-5**&nbsp;|&nbsp;**-&#45;v5**]
\[**-v**&nbsp;|&nbsp;**-&#45;verbose**]
\[**-l**&nbsp;|&nbsp;**-&#45;list-caches**]
\[**-f**]
\[**-&#45;version**]
\[**-&#45;help**]

# DESCRIPTION

**klist**
reads and displays the current tickets in the credential cache (also
known as the ticket file).

Options supported:

**-c** *cache*, **-&#45;cache=**&zwnj;*cache*

> credential cache to list

**-s**, **-t**, **-&#45;test**

> Test for there being an active and valid TGT for the local realm of
> the user in the credential cache.

**-T**, **-&#45;tokens**

> display AFS tokens

**-5**, **-&#45;v5**

> display v5 cred cache (this is the default)

**-f**

> Include ticket flags in short form, each character stands for a
> specific flag, as follows:

> F

> > forwardable

> f

> > forwarded

> P

> > proxiable

> p

> > proxied

> D

> > postdate-able

> d

> > postdated

> R

> > renewable

> I

> > initial

> i

> > invalid

> A

> > pre-authenticated

> H

> > hardware authenticated

> This information is also output with the **-&#45;verbose**
> option, but in a more verbose way.

**-v**, **-&#45;verbose**

> Verbose output. Include all possible information:

> Server

> > the principal the ticket is for

> Ticket etype

> > the encryption type used in the ticket, followed by the key version of
> > the ticket, if it is available

> Session key

> > the encryption type of the session key, if it's different from the
> > encryption type of the ticket

> Auth time

> > the time the authentication exchange took place

> Start time

> > the time that this ticket is valid from (only printed if it's
> > different from the auth time)

> End time

> > when the ticket expires, if it has already expired this is also noted

> Renew till

> > the maximum possible end time of any ticket derived from this one

> Ticket flags

> > the flags set on the ticket

> Addresses

> > the set of addresses from which this ticket is valid

**-l**, **-&#45;list-caches**

> List the credential caches for the current users, not all cache types
> supports listing multiple caches.

# SEE ALSO

kdestroy(1),
kinit(1)

HEIMDAL - October 6, 2005
