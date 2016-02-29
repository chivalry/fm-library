hyper-list
===========

Created by Todd Geist, todd@geistinteractive.com 
Forked by Charles Ross, chivalry@mac.com

This **hyper-list** module is based on Todd Geist's original
**[HyperList](http://www.modularfilemaker.org/module/hyperlist/)** module, but
conforms to my own general standards as outlined in the `conventions` documentation.

According to the web page for the original version from which this is forked:

> HyperList is a very fast, completely abstracted module for capturing a found set of
Primary Keys to a variable, for use in FileMaker
[VirtualList](http://seedcodenext.wordpress.com/2011/11/05/virtual-list/) techniques. It
has been shown to be faster than any other known method for gathering IDs in the current
found set. Yes, it is faster than the Custom List Custom Function. It is capable of
capturing 80,000 primary keys in about 10 seconds. As of version 2.0 it can gather up to
5 fields per record.

> - Works on any found set
> - Uses normal FileMaker sorting order
> - Can handle 10s of thousands of records
> - It works on FileMaker Go and FileMaker Pro

This fork makes the following changes while retaining the functionality of the original
version:

- Moves the storage and retrieval of the default column separator setting into a custom
  function
- Expects custom column separators to be passed as an optional parameter to the script
- Simplifies the loop that concatenates the final result
- Places the duplicated custom separator code within a loop
- Takes advantage of the script parameter functions found in the `cf-library` module
- Formats the various calculations for better readability and `fm-library` conventions

Acknowledgements
----------------

Thank you to Todd Geist for releasing the original version of this module. Todd gives
credit to [Sam and Jess Barnum](http://www.360Works.com) for the initial insight that
FileMaker string variables are immutable, and that writing strings to separate variables
and then concatenating them later can be faster.

Todd also credits Donavan Chan for pointing out Ralph Learmont's technique for using
`GetField` and `GetNthRecord` instead of `Evaluate`.

On the [HyperList web page](http://www.modularfilemaker.org/module/hyperlist/), Todd
mentions that Jason Young of [SeedCode](http://seedcode.com) built the multiple field
support for version 2.0.

Finally, Todd also gives credit to Koe and Corn Walker of The Proof Group for help with
testing and plotting the results.

Requirements
------------

- `cf-library` module for the use of script parameter functions and the
  `hypr.ColumnSeparator` setting function.

Integration Instructions
------------------------

- Install the functions found in the `cf-library` module.
- Copy the `hyper-list` folder into the target file.

Usage
-----

Once you have a found set of records for which you want to capture a list of field data
using **hyper-list**, call the `hyper-list: Found Set Values ( FieldList { ; ColSepList }
)` script, passing it a list of one to five fields to return the values of. Use the
`scpm.Param` custom function to properly format the parameters sent to the script. The
`FieldList` parameter expects a list of field names, so be sure to use `GetFieldName`
when passing these to the script.

    scpm.Param (
      "FieldList" ;
      List ( GetFieldName ( Table::uuid ) ; GetFieldName ( Table::field ) )
    )

The script's second parameter, `ColSepList`, is optional, and if omitted multiple columns
will be separated by the string returned by the `hypr.ColumnSeparator` custom function.
The number of column separators passed to the script should be , at most, one less than
the number of fields.

    scpm.Param (
      "FieldList" ;
      List ( GetFieldName ( Table::uuid ) ; GetFieldName ( Table::field1 ) )
    ) &
    scpm.Param ( "ColSepList" ; "><" )

Version History
---------------

- 2.0.1 - 140129 - Todd's release before fork.
- 3.0.0 - 160228 - Chuck's first version after fork.

To Do
-----

- See if the duplicate code that exists inside and outside the data collection loop can
  be consolidated.

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
