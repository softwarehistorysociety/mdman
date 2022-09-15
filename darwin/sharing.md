sharing(8) - System Manager's Manual

# NAME

**sharing** - create share points for smb services.

# SYNOPSIS

**sharing**
\[**-a**&nbsp;*&lt;path&gt;&nbsp;\[options]*]
\[**-e**&nbsp;*&lt;share&nbsp;point&nbsp;name&gt;&nbsp;\[options]*]
\[**-r**&nbsp;*&lt;share&nbsp;point&nbsp;name&gt;*]
\[**-l**]

# DESCRIPTION

A list of flags and their descriptions:

**-a** *&lt;path&gt;*

> Add a new share point for the directory specified by &lt;path&gt;.

**-e** *&lt;share point name&gt;*

> Edit the share point record specified by &lt;share point name&gt;.

**-r** *&lt;share point name&gt;*

> Delete the share point record specified by &lt;share point name&gt;.

**-l**

> List all existing share point records.

The following options modify share point record attributes:

**-S** *&lt;smb name&gt;*

> Use customized name &lt;smb name&gt; when using share points with smb.

**-s** *&lt;flags&gt;*

> Use this option to enable and disable sharing via smb.
> By default a share point is enabled for smb protocol.
> To enable and disable services, use the following flags as required: 001 (enable sharing for smb).
> Specify 000 to turn off sharing of a share point altogether.

**-g** *&lt;guest flag&gt;*

> Use this option to enable and disable guest access for smb.
> By default guest access is enabled for smb.
> To enable and disable guest access services, use the following flags as required: 001 (enable guest for smb).
> Specify 000 to turn off guest access for a share point altogether.

**-n** *&lt;customized record name&gt;*

> Specify a &lt;customized record name&gt; to be used as the share point record name.
> By default the record name is the name of the directory pointed to by the share point record.
> This directory is specified by the &lt;path&gt; when the record is created.

**-R** *&lt;0/1&gt;*

> Make share read only for smb. Specify 1 to enable read only. Specify 0 to disable read only.

**-E** *&lt;0/1&gt;*

> Make share encrypted for smb v3 and later. Specify 1 to enable encryption. Specify 0 to disable encryption.

**-f** *&lt;format&gt;*

> Only used when listing share points and only json format is supported.

# EXAMPLES

	/usr/sbin/sharing -a /SomePath/ShareThisDirectory
	

This example shows how to create a share point for the directory "/SomePath/ShareThisDirectory":

	/usr/sbin/sharing -e ShareThisDirectory -S SP1 -g 001
	

This example shows how to edit the share point record created above,
adding a customized name "SP1" for smb services, and enabling guest access for smb.

# FILES

*/usr/sbin/sharing*

> location of tool

macOS - Thu February 17 2017
