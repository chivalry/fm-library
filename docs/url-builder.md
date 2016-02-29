url-builder
===========

Created by Todd Geist, todd@geistinteractive.com  
Forked by Charles Ross, chivalry@mac.com

**url-builder** is a set of chainable custom functions for building URLs. It takes the
work out of creating any kind of URL, including those using the `fmp://` protocol.

My version of this, forked from Todd Geist's original, retains only the custom functions
from his module and has been rolled into the **cf-library** module. Look for the "URL
Builders" group of custom functions.

Acknowledgements
----------------

Thank you to Todd Geist for releasing the original version of this.

Requirements
------------

None, other than the **cf-library** that **url-builder** has been rolled into.

Integration Instructions
------------------------

Follow the instructions for **cf-library** integration.

Usage
-----

The basic idea of **url-builder** is that URLs are created in steps. You begin the steps
with `urlb.Bookend` (or `urlb.FMP`, as we'll see), add URL parts one at a time, and
indicate that you're finished by again calling `urlb.Bookend`.

The first call to `urlb.Bookend` gets a parameter that indicates the type of URL. At this
time, only `http`, `https` and `fmp` protocols are supported, with `http` being used if
no protocol is supplied.

    urlb.Bookend ( "chivalrysoftware.com" ) &
    urlb.Bookend ( "" ) // Returns "http://chivalrysoftware.com"

    urlb.Bookend ( "https://chivalrysoftware.com ) &
    urlb.Bookend ( "" ) // Returns "https://chivalrysoftware.com"

Besides the protocol and base address, you can various other parts to a URL, including
authorization ID and password, directory paths and arbitrary parameters.

    urlb.Bookend ( "www.geistineteractive.com" ) &
    urlb.Auth ( "admin" ; "password" ) &
    urlb.Path ( "contacts" ) &
    urlb.Path ( "23345" ) &
    urlb.Param ( "max" ; "100" ) &
    urlb.Param ( "skip" ; "50" ) &
    urlb.Bookend ( "" )

    // The final call returns
    // "http://admin:password@www.geistinteractive.com/contacts/23345?max=100&skip=50"

Perhaps the most convenient feature of **url-builder** is the ability to automatically
create valid `fmp` protocol URLs using the `urlb.FMP` function. You can specify the
filename and IP address or, as is likely, you can create a link to the current file on
the current host by passing empty strings to the function

    urlb.FMP ( "" ; "" ) &
    urlb.Param ( "script" ; "New Contact" ) &
    urlb.Param ( "first_name" ; "Clark" ) &
    urlb.Param ( "last_name" ; "Kent" ) &
    urlb.Bookend ( "" )

    // Something like
    // fmp://$/FileName?script=New%20Contact&first_name=Clark&last_name=Kent
    // when executed on a locally hosted system or
    // fmp://192.168.1.5/FileName?script=... on a hosted system

Of course, you can manually specify the filename and host address as well.

    urlb.FMP ( "SolutionFile" ; "10.10.10.51" )

You can string **url-builder** calls together with concatenation, as demonstrated above,
or you can call each function individually using separate `Let` variables or script steps.

    Let (
      [
        _ = urlb.Bookend ( "apple.com" ) ;
        _ = urlb.Path ( "macbook-pro" )
      ] ;
      urlb.Bookend ( "" )
    ) // returns "http://apple.com/macbook-pro"

Only the last function call actually returns anything. Everything leading up to that
builds the URL in a global variable that is cleared out with the final function call.

Version History
---------------

- 1.0 released by Todd Geist, 2014
- 2.0 forked by Charles Ross, 16-02-28

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
