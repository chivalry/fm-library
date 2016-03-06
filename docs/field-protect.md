field-protect
=============

Created by Ted Weil, tedweil@datawranglersllc.com
Forked by Charles Ross, chivalry@mac.com

Simple, context independent triggers that prevent accidental data changes to a field.

Acknowledgements
----------------

Requirements
------------

Integration Instructions
------------------------

1. Copy "FIELD PROTECTION" script folder with all contents into your solution.
2. Set the FieldProtect_enter script as the "OnObjectEnter" script trigger on any field you want to protect.
3. Set the "FieldProtect_exit" trigger as the "OnObjectExit" trigger on the same field.
4. By default the triggers ignore capitalization as a change.
    If you want the triggers to prompt for capitalization changes, add "Exact" as the script parameter on the "OnObjectExit" trigger.

Usage
-----

Prompts the user that the data in the field has changed and allows them to accept or revert the changes.
Eliminates the need to Revert Record, potentially changing other record data.
Allows for initial data entry into an empty field with no prompts.

Version History
---------------

To Do
-----

License
-------

The MIT License (MIT)  
Copyright (c) 2016 Charles Ross, chivalry@mac.com

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

