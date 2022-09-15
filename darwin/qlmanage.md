qlmanage(1) - General Commands Manual

# NAME

**qlmanage** - Quick Look Server debug and management tool

# SYNOPSIS

**qlmanage**
**-r**

**qlmanage**
**-m**
\[*name&nbsp;...*]

**qlmanage**
**-t**
\[**-x**]
\[**-i**]
\[**-s**&nbsp;*size*]
\[**-f**&nbsp;*factor*]
\[**-c**&nbsp;*contentTypeUTI*&nbsp;\[**-g**&nbsp;*generator*]]
\[*file&nbsp;...*]

**qlmanage**
**-p**
\[**-x**]
\[**-c**&nbsp;*contentTypeUTI*&nbsp;\[**-g**&nbsp;*generator*]]
\[*file&nbsp;...*]

**qlmanage**
**-h**

# DESCRIPTION

**qlmanage**
allows you to test your Quick Look generators and manage Quick Look Server.

The following usages are available:

1\.

> **qlmanage**
> **-r**
> resets Quick Look Server and all Quick Look client's generator cache.

2\.

> **qlmanage**
> **-m**
> gets all sort of information on Quick Look server including the list of detected generators.

3\.

> **qlmanage**
> **-t**
> displays the Quick Look generated thumbnails (if available) for the specified files.

4\.

> **qlmanage**
> **-p**
> displays the Quick Look generated previews for the specified files.

5\.

> **qlmanage**
> **-h**
> displays extensive help.

Mac&#160;OS X - March 29, 2007
