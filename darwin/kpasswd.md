KPASSWD(1) - General Commands Manual

# NAME

**kpasswd** - Kerberos 5 password changing program

# SYNOPSIS

**kpasswd**
\[**-&#45;admin-principal=**&zwnj;*principal*]
\[**-c**&nbsp;*cache*&nbsp;|&nbsp;**-&#45;cache=**&zwnj;*cache*]
\[*principal&nbsp;...*]

# DESCRIPTION

**kpasswd**
is the client for changing passwords.

If administrator principal is given that principal is used to change
the password.

Multiple passwords for different users can be changed at the same time,
then the administrator principal will be used.
If the administrator isn't specified on the command prompt, the
principal of the default credential cache will be used.

If a credential cache is given, the **-&#45;admin-principal**
flag is ignored and use the default name of the credential cache is
used instead.

# DIAGNOSTICS

If the password quality check fails or some other error occurs, an
explanation is printed.

# SEE ALSO

kpasswdd(8)

HEIMDAL - January 5, 2005
