profiles(1) - General Commands Manual

# NAME

**profiles** - Profiles Tool for macOS.

# SYNOPSIS

**profiles**
*verb*
\[*options*]

# DESCRIPTION

**profiles**
is used to handle various profile types on macOS.   Starting with macOS 11.0 (profiles tool 8.0 or later), this tool cannot be
    used to install configuration profiles.  You should add your profiles using the System Preferences Profiles
    preference pane.    Additionally, startup profiles are no longer supported.

# VERBS

Each command verb is listed with its description and optional individual arguments.   Most commands use the -type option to determine which kind of profile should be used in the command.  For those commands, if no type is specified, the default will be to use the configuration profile type.

**help**

> Shows abbreviated help

**list**

> **-type** *profile\_type*
> **-user** *user\_name*
> **-output** *output\_path*  
> List profiles for a user or when running as root, the device.

**show**

> **-type** *profile\_type*
> **-user** *user\_name*
> **-output** *output\_path*  
> Show expanded information for profiles.   For an enrollment, this will show the current DEP configuration, and the call may be rate limited to once every 23 hours.

**remove**

> **-type** *profile\_type*
> **-user** *user\_name*
> **-identifier** *identifier*
> **-uuid** *uuid*
> **-path** *file\_path*
> **-forced**
> **-all**  
> Remove profiles. Attempting to remove a configuration profile requring a removal password without the correct password will fail.

**status**

> **-type** *profile\_type*  
> Display status of the profiles installed on this client.   When displaying the enrollment type status, if the MDM enrollment was user approved, the status output will show "(User Approved)".

**sync**

> **-type configuration**  
> For configuration profiles, synchronize current installed set of profiles with the local users and remove any configuration profiles that belong to users that no longer exist on this computer.

**renew**

> **-type** *profile\_type*
> **-identifier** *identifier*
> **-output** *output\_path*  
> For configuration profiles, renews any certificates for the specified profile.  For Device Enrollment Program (DEP) enrollments, retry to obtain the device enrollment configuration, and re-enable the user notification if enrollment wasn't completed.

**validate**

> **-type** *profile\_type*
> **-path** *file\_path*  
> For provisioning profiles, validate the provisioning profile located at the file\_path.
> For enrollments, re-validate the installed DEP server information and update any local information, displaying any major changes.  If this information is different from the current enrolled server, this will not unenroll the client from the current server.  This call may be rate limited to once every 23 hours.

**version**

> Displays current tool version.

# OPTIONS

**-type** *profile\_type*

> The profile\_type can be one of either: "configuration", "provisioning", "bootstraptoken", or "enrollment" (DEP).  If a command requires a profile type and none is specified, "configuration" will be used.

**-path** *file\_path*

> A file path or "-" to represent stdout.   When used by the remove command for startup profiles, this should only contain the file name of the profile.

**-user** *user\_name*

> An OD short user name.   In most cases if no user was specified, then the current user will be used.   If no user option was specified and the process runs as root, the computer/device profiles will be used in the command.

**-uuid** *profile\_uuid*

> A canonical form UUID to specify a profile's PayloadUUID, such as 5A15247B-899C-474D-B1D7-DBD82BDE5684.   Only used by the remove provisioning profile command.

**-identifier** *profile\_identifier*

> A profile identifier (PayloadIdentifier) to specify a profile.

**-output** *output\_path*

> The output path location.  The output\_path argument must be specified to use this option, Use 'stdout' to send this informaton to the console.  File output will be written as an XML plist file, or you can use 'stdout-xml' to write XML to the console.  The toplevel key of the dictionary will contain either the user name, or \_computerLevel for device or provisioning profile information.

**-password** *password*

> An optional password used when removing a configuration profile which requires the password removal option.

**-forced**

> This will prevent confirmation requests, and when trying to remove all configuration profles for a user, it will ignore any errors during removal.

**-all**

> For configuration profiles, when running as root, the use of this option with the list or show commands will display all profiles installed on the system.   When removing profiles, using this option will remove all profiles for that user (or device).

**-verbose**

> Display additional information.

# PROFILE TYPES

configuration

> A configuration profile.

provisioning

> A provisioning profile.

enrollment

> A device enrollment program (DEP) or mobile device management (MDM) enrollment profile or feature.

bootstraptoken

> Bootstrap Token options.   Requires MDM supervised client.

# EXAMPLES

profiles remove -path /profiles/testfile2.mobileconfig

> Removes the configuration profile file '/profiles/testfile2.mobileconfig' into the current user.

profiles list -type provisioning

> Displays a list of installed provisioning profiles.

profiles list -all

> When running as root, this will list all configuration profiles on the system.

profiles show

> Displays extended information for installed configuration profiles for the current user.

profiles status -type startup

> Displays information on whether or not startup profiles are set up.

profiles remove -identifier com.example.profile1 -password pass

> Removes any installed profiles with the identifier com.example.profile1 in the current user and using a removal password of 'pass'.

profiles show -type enrollment

> Displays the current DEP configuration information.

profiles renew -type enrollment

> Re-enables the DEP user notification enrollment messages.

profiles install -type bootstraptoken

> Creates or updates the Bootstrap Token APFS record and escrows the information to the server.

# SEE ALSO

profiles.old(1)

macOS - November 30, 2021
