# ParamConverter

Converting dictionary formats in FileMaker Pro

## Overview

This module provides a means for systems employing SFR format to easily integrate Let-based modules with minimal effort. You can also integrate SFR-based scripts into Let-based systems if you wish. Let me know if you're interested in other conversions and we can talk about extending the functionality.

#### Let Format

As outlined [here](http://www.modularfilemaker.org/documentation/#Passing_Parameters), ModularFileMaker.org suggests using “Let Variables” for passing named parameters to scripts. This method for constructing name-value pairs is popular in large part because it leverages native functionality and doesn’t require any custom functions.

````
"$name = \"Calvin\" ;
$age = 5 ;"
````

#### SFR Format

Still, others prefer to use alternative dictionary formats. One such format is the one created and popularized by Jesse Antunes of Six Fried Rice. (Let’s call it SFR format.)

````
"<:name:=Calvin:>
<:age:=5:>"
````

## Usage

The ParamConverter module provides one script for converting from SFR format to Let Variables and one for converting from Let Variables to SFR format. The most straightforward approach is to create a wrapper script for each script you’d like to call using a different parameter format. This wrapper script will convert the parameters and script results for you. The module includes an example script that shows you how. You can also see it in action in the enhanced demo file for the [ErrorHandling](http://www.modularfilemaker.org/2013/11/errorhandling/) module.

To call a Let-based script, just copy the example script from this module and redirect it to the Let-based one.

You also have the option of adding a prefix to your variables. For example, you can set the variable prefix to "__" to have ````"<:name:=Calvin:>```` converted to a variable named ````$__name```` or vice versa.

## Integration

Just import the ParamConverter script folder and begin making wrapper scripts. Remember also to add the initialization script to your launch routine.

## Download and Installation

There should be a "Download ZIP" button on the [GitHub page](https://github.com/DonovanChan/ParamConverter).

To install, just import the ParamConverter script folder from ParamConverter.fmp12 into your solution.

## Contact

Donovan Chandler  
donovan_c@beezwax.net
