AUTOMATOR(1) - General Commands Manual

# NAME

**automator** - Runs Automator workflow.

# SYNOPSIS

**automator**
\[**-v**]
\[**-i**&nbsp;*input*]
\[**-D**&nbsp;*name*=*value*&nbsp;...]
*workflow*

# DESCRIPTION

**automator**
runs the specified workflow.  To create or edit a workflow, use the Automator application.

The following options are available:

**-D** *name*=*value*

> Set variable
> *name*
> to
> *value*
> for this run of
> *workflow*.

**-i** *input*

> Set
> *input*
> as the input to
> *workflow*.
> If
> *input*
> is - then the contents of standard input is used.  Each newline
> (&#92;n)-terminated line is treated as one text input item.

**-v**

> Run in verbose mode.

Mac OS X - April 1, 2007
