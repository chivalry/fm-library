auto-quick-find
===============

Created by Jeremy Bante, [http://scr.im/jbante](http://scr.im/jbante)
Forked by Charles Ross, chivalry@mac.com

**auto-quick-find** is an implementation of search-as-you-type functionality that
achieves greater responsiveness by only performing the search when there's a sufficient
pause in the user's typing.

Acknowledgements
----------------

Thank you to Jeremy Bante for creating the original project from which this version was
forked. The original version can be found on
[GitHub]( https://github.com/jbante/FM-AutoQuickFind)

Requirements
------------

- **cf-library**, which contains the settings function for this module.

Integration Instructions
------------------------

1. Install the functions found in **cf-library**.
2. Import the `auto-quick-find` script folder.
3. Decide what name you want to give quick find fields on the layouts where they are used
and store this string in the `auqf.FindFieldName` custom function. The default value for
this will be `"field.auto_quick_find"`. 
4. Decide whether you want to show all records when the query field is empty. The default
is `True`, meaning that when the search field is cleared all records will be shown. If
you prefer no records to be shown, return `False` from the `auqf.ShowAllOnEmptyQuery`
custom function.

Usage
-----

1. On each layout you want to use **auto-quick-find** on, add a field for users to enter
their query.
2. Set the name of this field to the string returned by the `auqf.FindFieldName` custom
function.
3. Make sure that the `OnObjectModify` script trigger for the field will execute the
script `auto-quick-find: OnObjectModify`.
4. If you want to ensure that found records are sorted in a particular order after the
find has been executed, attach a script to the layout's `OnModeEnter` trigger for browse
mode and perform the sort within that script. **auto-quick-find** will toggle between
Find and Browse mode to ensure any such script gets triggered.

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
