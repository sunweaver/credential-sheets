# credential-sheets: User Account Credential Sheets Tool

## Introduction

After mass import of user accounts (e.g. into LDAP) most site
administrators have to create information sheets (or snippets) containing
those new  credentials (like username, password, policy of usage, etc.).

With this tiny tool, providing these pieces of information to multiple
users, becomes really simple. Account data is taken from a CSV file and
the sheets are output as PDF using easily configurable LaTeX template
files.

## Usage

**Synopsis:** ``credential-sheets [options] <CSV-file-1> [<CSV-file-2> [...]]``

**Options:**
```:
    --help                        -- show this help output.
    --template=<tpl-name>         -- name of the template to use.
    --cols=<x>                    -- render <x> columns per sheet
    --rows=<y>                    -- render <y> rows per sheet
    --zip                         -- do create a ZIP file at the end
    --zipfilename=<zip-file-name> -- alternative ZIP file name (default: name of parent folder)
    --debug                       -- don't remove temporary files
```

## CSV File Column Arrangement

The ``credential-sheets`` tool can handle any sort of column arrangement
in given CSV file(s). It expects the CSV file(s) to have column names in
their first line.

The given column names have to map to the ``VAR-<column-name>``
placeholders in ``credential-sheets``'s LaTeX templates.

The shipped-with templates (``students``, ``teachers``) can handle these
column names:

  * **login** -- The user account's login id (uid)
  * **lastName** -- The user's last name(s)
  * **firstName** -- The user's first name(s)
  * **password** -- The user's password
  * **form** -- The form name/ID (student template only)
  * **subjects** -- A list of subjects taught by a teacher (teacher
    template only)

If you create your own templates, you can be very flexible in using your
own column names and template names. Only make sure that the column names
provided in the CSV file(s)'s first line match the variables used in the
customized LaTeX template.

## Customizations

The shipped-with credential sheets templates are expected to be installed
in ``/usr/share/credential-sheets/`` for system-wide installations. When
customizing templates, simply place a modified copy of any of those files
into ``~/.credential-sheets/`` or ``/etc/credential-sheets/``. For
further details, see below.

The ``credential-sheets`` tool uses these *configuration* files:

  * ``header.tex`` (LaTeX file header)
  * ``<tpl-name>-template.tex`` (where as ``<tpl-name>`` ``students`` and
    ``teachers`` is provided on default installations, this is extensible by
    defining your own template files, see below).
  * ``footer.tex`` (LaTeX file footer)

Search paths for configuration files (in listed order):

  * ``$HOME/.credential-sheets/``
  * ``./``
  * ``/etc/credential-sheets/``
  * ``/usr/local/share/credential-sheets/``
  * ``/usr/share/credential-sheets/``

You can easily customize the resulting PDF files generated with this tool
by placing your own template files, header and footer where appropriate.

## Copyright and License

Copyright © 2012-2016, Mike Gabriel <mike.gabriel@das-netzwerkteam.de

Licensed under GPL-2+ (see COPYING file).
