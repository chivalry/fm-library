# FM-AutoQuickFind

Auto Quick Find is an implementation of search-as-you-type functionality that achieves greater responsiveness by only performing a find when there's a pause in the user's typing.

## Installation

1. Import the "Auto Quick Find" set of scripts.
2. On each layout you want to use Auto Quick Find on, add a field for users to enter their query.
3. Set the layout object name for that field to "AutoQuickFindField".
4. Set the OnObjectModify script trigger for that field to use the "Auto Quick Find OnObjectModify ..." script in the Auto Quick Find/Public folder.

## Options

### showAllOnEmptyQuery

The "Auto Quick Find OnObjectModify ..." script accepts the optional showAllOnEmptyQuery parameter, using [Let notation][1].

[1]: http://filemakerstandards.org/pages/viewpage.action?pageId=5668879 "FileMakerStandards.org: Data Serialization (Let Notation)"

Set showAllOnEmptyQuery to True (1) to Show All Records if the search field is cleared.

	"$showAllOnEmptyQuery = True ;¶"

Set showAllOnEmptyQuery to False (0) to hide all records if the search field is cleared.

	"$showAllOnEmptyQuery = False ;¶"

showAllOnEmptyQuery defaults to False (0).

### Sort OnModeEnter

After performing a find, Auto Quick Find flips to Find Mode, and back to Browse Mode. This allows you to define any sort you want in an OnModeEnter triggered script without having to hard-code a sort order in the Auto Quick Find module.

## License

Anyone may do anything with this software. There is no warranty.