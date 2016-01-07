fm-cf-library
=============

Created by Charles Ross, chivalry@mac.com

A FileMaker module that provides a standard custom function libary. With over 400
available functions, this library includes a wide range of readily available tools
for the FileMaker developer.

While I wrote many of these myself, there are quite a few that are from other sources.
I've tried to acknowledge the original author when I could as well as provide a URL to
the web page where the function was originally found. If you find a function that you
wrote without an attribution to you, please open an issue so I can fix that.

Acknowledgements
----------------

Many of these functions are from sources other than myself. I've tried to include
attributions when I knew who originally wrote them, but this information is sometimes
missing. If you know who wrote a particular function for which an attribution is missing
(see the issues for some authors that I'm looking for), please let me know. Among the
FileMaker developers that I can definitively thank for their contributions to the
FileMaker community (in no particular order):

- [Matt Petrowski](http://www.filemakermagazine.com)
- [Jeremy Bante](https://twitter.com/jbante)
- [Winfried Huslik](https://twitter.com/whuslik)
- Matt Wills
- [Kevin Frank](http://www.kevinfrank.com/index.html)
- [Tom Robinson](http://www.tomrobinson.co.nz)
- [Jesse Antunes](http://sixfriedrice.com/wp/about-sfr/)
- [Agnès Barouh](mailto:barouh.agnes@wanadoo.fr)
- [Arnold Kegebein](http://www.kegebein.net/blog/about/)
- [Geoff Coffey](http://sixfriedrice.com/wp/about-sfr/)
- [Andrew Persons](http://www.excelisys.com/our-team-custom-database-consultants.php)
- [Theo Gantos](https://twitter.com/tgantos)
- [Mikhail Edoshin](http://mikhailedoshin.com)
- [The Shadow](http://www.fmfunctions.com/members_display_record.php?memberId=34)
- Vaughan Bromfield
- [Bob Weaver](http://fmforums.com/profile/53726-bobweaver/)
- [LaRetta](http://fmforums.com/profile/59345-laretta/)
- [Fabrice Nordman](https://twitter.com/FabriceN)
- [Joe Scarpetta](http://scarpettagroup.com/filemaker-development-about/)
- [James Scarpetta](http://scarpettagroup.com/filemaker-development-about/)
- [Will M. Baker](https://www.beezwax.net/beez/100)
- Brad Lowry
- Alexander Zueiv
- Jesse Swensen
- [Debi Fuchs](http://www.aptworks.com/welcome.html)
- [Mislav Kos](http://www.soliantconsulting.com/users/mkos)
- [Nicholas Orr](http://www.goya.com.au/about/staff)
- [John Jones](john.christopher@alumni.virginia.edu)
- [Andy Knasinski](http://www.nrgsoft.com/about/leadership.html)

For those of you above which I haven't yet linked to, or if there's a different URL
you'd like a link to, send me a URL that you would like attached to your name.

Requirements
------------

FileMaker Pro 12 Advanced or greater is required to use this module, but FileMaker Pro 14
Advanced is recommended. Not all custom functions may work properly in earlier versions.

Integration Instructions
------------------------

Most interested parties won't require these instructions, and probably already know how
to import custom functions into a FileMaker file, but just in case, here's the procedure.

1. Open your file with FileMaker Pro Advanced using a full access account.
2. Choose File>Manage>Custom Functions from the menu bar.
3. Click the "Import" button.
4. Navigate to the location of `fm-library.fmp12`, select it and click "Open".
5. Select all of the custom functions with Cmd-A or Ctrl-A, depending on your platform.
6. Click one of the checkboxes next to a custom function in the list, which should check
all of them.
7. Click "OK" in the "Import Custom Functions" dialog box.
8. Click "OK" in the "Manage Custom Functions" dialog box. 

Conventions
-----------

Read the [conventions documentation](conventions.md), which covers not only the conventions used in the
custom function library, but also across the fm-library project.

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
