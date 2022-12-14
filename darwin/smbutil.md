SMBUTIL(1) - General Commands Manual

# NAME

**smbutil** - interface to the SMB requester

# SYNOPSIS

**smbutil**
\[**-hv**]
*command*
\[**-**&zwnj;*options*]
\[*args*]

# DESCRIPTION

The
**smbutil**
command is used to control SMB requester and issue various commands.

There are two types of options &#8212; global and local to the specified
*command*.

Global options are as follows:

**-h**

> Print a short help message.

**-v**

> Verbose output.

The commands and local options are:

**help** *command*

> Print usage information about
> *command*.

**lookup**
\[**-w** *host*]
\[**-t** *node\_type*]
\[**-e**]
*name*

> Resolve the given
> *name*
> to an IP address.
> The NetBIOS name server can be
> directly specified via the
> **-w**
> option. The NetBIOS name type can be specified via the
> **-t**,
> the default is to lookup file servers. For a complete list of name types please see "http://support.microsoft.com/kb/163409".
> The NetBIOS names will be unpercent escaped out if the
> **-e**
> option is specified.

**status**
\[**-ae**]
*hostname*

> Resolve given
> *hostname*
> (IP address or DNS name) to NetBIOS workgroup and system name. All
> NetBIOS names will be displayed if the
> **-a**
> option is specified. All NetBIOS names will be percent escaped out if the
> **-e**
> option is specified.

**view**
\[**-**&zwnj;*options*]
//\[*domain*;]\[*user*\[:*password*]@]*server*

> List resources available on the specified
> *server*
> for the
> *user*.

> The options are as follows:

> **-A**

> > authorize only.

> **-N**

> > don't prompt for a password.

> **-G**

> > allow guest access.

> **-g**

> > authorize with guest only.

> **-a**

> > authorize with anonymous only.

> **-f**

> > don't share session.

**identity**
\[**-N**]
//\[*domain*;]\[*user*\[:*password*]@]*server*

> Display the user's identity as known by the
> *server*
> for the authenticated session. Will not prompt for a password if the
> **-N**
> option is specified.

**dfs**
smb://\[*domain*;]\[*user*\[:*password*]@]*server/DfsRoot*\[/*DfsLink*]

> Display the Dfs referrals for this
> *URL*
> for the authenticated session.

**statshares**
\[**-m** *mount\_path*
|
**-a**]
\[**-f** *format*]

> If
> **-m**
> is specified, it prints the attributes of the share mounted at
> *mount\_path*.
> If
> **-a**
> is specified, it prints the attributes of all mounted shares. You can not specify both
> **-m**
> and
> **-a**
> together since they are mutually exclusive.
> **-f**
> controls the output
> *format*.
> If
> **-f**
> is not specified then human readable format is used. Supported formats are: Json.

**multichannel**
\[**-m** *mount\_path*
|
**-a**]
\[**-**&zwnj;*options*]
\[**-f** *format*]

> If
> **-m**
> is specified, it prints the multichannel attributes of the share mounted at
> *mount\_path*.
> If
> **-a**
> is specified, it prints the multichannel attributes of all mounted shares. You can not specify both
> **-m**
> and
> **-a**
> together since they are mutually exclusive.
> **-f**
> controls the output
> *format*.
> If
> **-f**
> is not specified then human readable format is used. Supported formats are: Json.

> The options are as follows:

> **-i**

> > print information about the session.

> **-c**

> > print information about the client's interfaces.

> **-s**

> > print information about the server's interfaces.

> **-x**

> > print information about the established connection.

> If no option is given, then all options will be shown.

**snapshot**
\[**-m** *mount\_path*
|
**-a**]
\[**-f** *format*]

> If
> **-m**
> is specified, it prints out a list of snapshots for the item at the path of
> *mount\_path*.
> If
> **-a**
> is specified, it prints the snapshots of all mounted shares. You can not specify both
> **-m**
> and
> **-a**
> together since they are mutually exclusive.
> **-f**
> controls the output
> *format*.
> If
> **-f**
> is not specified then human readable format is used. Supported formats are: Json.

# FILES

*nsmb.conf*

> Keeps static parameters for connections and other information.
> See
> *man nsmb.conf*
> for details.

# AUTHORS

Boris Popov &lt;bp@butya.kz&gt;,
&lt;bp@FreeBSD.org&gt;

# BUGS

Please report any bugs to Apple.

macOS 12.6 - February 14, 2000
