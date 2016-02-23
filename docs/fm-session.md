FMSessions
==========

Created by Todd Geist, todd@geistinteractive.com  
Forked by Charles Ross, chivalry@mac.com

A FileMaker module that provides the table and scripting to maintain a session record
for each user who connects to the database. This can be useful to track who is currently
logged into a database system and will eventually be the basis for a general Perform
Script on Client module.

The latest development build and release can always be found on
[GitHub](https://github.com/chivalry/fm-sessions), where you'll also find a more readable
version of this documentation.

This fork adds flexibility features to Todd Geist's original
[Sessions module](http://www.modularfilemaker.org/module/sessions/). While integration
can import the table structure included with the module, it can alternatively use an
existing table with existing fields. It also stores the current session ID in a global
variable by default, although this can be changed by the integrator. It also adds the
ability to suppress script triggers during session manipulation, restoration of calling
script error capture and allow abort states and removes various custom functions, fields,
and scripts that aren't required by the module. Finally, it makes use of custom functions
instead of a script for customized settings as well as for increased readability and self
documenting script code.

Requirements
------------

- FileMaker Pro 12 Advanced or greater during integration. FileMaker Pro 12 or greater
for daily use.
- A table to store sessions into. You can copy the module's table if you don't already
have one.
- A layout whose context is linked to a table occurrence of the session table.
- A primary key field in the session table.
- A persistent id field in the session table.
- A global storage location for the current session. This can be a global text field or a
global variable.

Integration Instructions
------------------------

Integration requires access to FileMaker Pro Advanced 12 or greater. These instructions
assume you are familiar with using FileMaker Pro Advanced to alter your solution's
tables, layouts, etc.

### Creating the Sessions Table

If you don't already have a session table, you'll need to either create one or copy the
session table from the module file.

1. Use FileMaker Pro Advanced to copy the `Sessions` table to your solution.
2. Confirm that doing so automatically created a `Sessions` table occurrence and a
`Sessions` layout.

The module's `Sessions` table is very sparse on fields, including only what is absolutely
required for the module's features, which means a `uuid` field for the primary key and a
`persistent_id` field. You can add additional fields at this time, such as
`date_time_created` and `modified_by` at this time. You're also free to rename the
existing fields now if you wish, although doing so later will save you a bit of work.

If you want to store the current session id in a global field instead of a global
variable (which is the default), add a global text field to the `Sessions` table.

### Importing the Custom Functions

**FMSessions** uses custom functions for storing settings as well as convenience and
automatic commenting of scripts. Use FileMaker Pro Advanced to import the module's custom
functions into your solution. If you're already using version 2.0 or greater of the
custom library found on
[GitHub](https://github.com/chivalry/filemaker-custom-functions/archive/2.0.1.zip), you
have most of the required functions, but will still need to import the `sess` functions
from the module file.

Once the custom functions are in place, there are seven that store the module's settings.
The default behavior is as follows:

- The current session ID should be stored in `$$_CURRENT_SESSION_ID`.
- The layout name for manipulating sessions is `Sessions`.
- The session table's primary key is named `Sessions::uuid`.
- The session table's persistent id field is named `Sessions::persistent_id`.
- Script triggers should be disabled during session record creation and deletion.
- Calling `trig.Disable` will disable script triggers.
- Calling `trig.Enable` will enable script triggers.

If these defaults work for you, you're done with the custom functions. Instructions for
overriding the defaults of each setting are found below.

- Current Session ID Storage

    This setting is found in the `sess.CurrentIDStorage` custom function and returns the 
*name* of the storage location, not the storage location itself. By default it returns
`"$$_CURRENT_SESION_ID"` (note that it's quoted). If you use a different global variable
naming convention, just set the name you want the current session ID store in here. You
must include the double dollar sign.

    Alternatively, you can store the current session ID in a global field. A commented
out example of doing so is found in the custom function, using `GetFieldName` to return
the fully-qualified field name. If you do this, uncomment the custom function's
`GetFieldName` line and provide a direct reference to the field. Then either comment out
or delete the string that references the global variable.

- Sessions Layout Name

    Set the `sess.LayoutName` custom function to return the name of the layout that
should be navigated to for session manipulation . Note that the layout name should be
unique within your solution.

- Primary Key Field Name

    Use `sess.PrimaryKeyFieldName` to return the name of the primary key field of your
sessions table. Best practices advise using `GetFieldName` to provide a direct reference
to the field in case you later change it.

- Persistent ID Field Name

    Use `sess.PersistantIDFieldName` to return the name of the field that should store
the sessions' persistent ID. This is used to at least reduce the liklihood of duplicate
session records created by a single client. Again, best practices advise using
`GetFieldName` to provide a direct reference to the field to prevent broken functionality
should you later change the field name.

- Disable Triggers

    **FMSessions** needs to move to the session layout and back to perform it's
functionality. Since this could fire script triggers, this setting offers the ability to
disable script triggers during session record manipulation. If `sess.DisableTriggers`
returns `True`, the code found in `sess.TrigDisable` and `sess.TrigEnable` will be used
to turn triggers off and on.

- Script Trigger Disabling and Enabling

    The **FMSessions** module includes the script trigger control functions written by
[Jeremy Bante](https://twitter.com/jbante). These are very useful in that they don't just
set a global variable, but also keep track of which scripts have disabled triggers and
only re-enables them once each script that disabled them also enables them.

    However, if you already have your own trigger control mechanism in place, use
`sess.TrigDisable` and `sess.TrigEnable` to provide a string that when evaluated will
perform the needed actions. A commented-out example of doing so with a `Let` function
that sets a global variable is found in both `sess.TrigEnable` and `sess.TrigDisable`.

    If you are returning `False` with `sess.DisableTriggers`, you can delete the
`sess.Trig*` and `trig*` custom functions.

### Running the Test Script

If you've made changes to the custom functions and want to make sure, to some extent at
least, that all of the settings work, run the `FMSess: Test Settings` script. This will
check the following:

- That the named layout is not empty, is an existing layout and is uniquely named.
- That the two required field settings refer to actual fields that are accessible from
the named layout.
- That the current ID storage is either a global variable or a global field.
- That the calculation code stored in sess.TrigDisable and sess.TrigEnable is executable. 

### Setting up Script Execution

By now you should have everything ready and can configure your file to use the sessions
feature. Simply add calls to `FMSess: OnFirstWindowOpen` and `FMSess: OnLastWindowClose`
to your own scripts that are connected to those script triggers.

License
-------

The MIT License (MIT)  
Copyright (c) 2013 Todd Geist, todd@geistinteractive.com  
Copyright (c) 2015 Charles Ross, chivalry@mac.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this
software and associated documentation files (the "Software"), to deal in the Software
without restriction, including without limitation the rights to use, copy, modify, merge,
publish, distribute, sublicense, and/or sell copies of the Software, and to permit
persons to whom the Software is furnished to do so, subject to the following conditions

The above copyright notice and this permission notice shall be included in all copies or
substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
