sql-sugar
===========

Created by Brian Schick, 13-03-15
Forked by Charles Ross, chivalry@mac.com

**sql-sugar** is a FileMaker power SQL tool that "sweetens" creating and maintaining
FileMaker SQL. It is designed to help developers quickly craft robust, readable, elegant
FileMaker SQL (FQL). Think of **sql-sugar** as power steering: It won't steer your car
for you, but it will help make driving more effortless and fun, and let you focus on the
road instead of the mechanics of driving.

**sql-sugar** is designed to focus on the building blocks of SQL queries: the fields,
tables, values, and SQL operators that make up any SQL query. **sql-sugar** makes it easy
to get, modify, and combine these query elements like LEGO blocks. This makes writing SQL
queries light and flexible.

My version of this, forked from Brian Schick's original, has been rolled into the **cf
library** module. Look for the "SQL Sugar" group of custom functions.

Acknowledgements
----------------

Thank you to Brian Schick for creating the original SQL Sugar module. Brian in turn
expressed gratitude to Vincenzo Menanno, Jay Gonzales, Todd Geist, and Matt Petrowsky.

Requirements
------------

None, other than the **cf-library that **sql-sugar** has been rolled into.

Integration Instructions
------------------------

Follow the instructions for **cf-library** integration.

Usage
-----

### Contextual Help

Brian has offerred terrific documentation built into the module's main function,
`sqls.Sugar` (called `@` in his original module). Preferring, as I do, to have the
documentation in the readme file, most of the content you'll find below is taken directly
from his contextual help. Contextual help is still available, however, and can be
accessed with the following commands.

| Command | Description |
| ------- | ----------- |
| `sqls.Sugar ( "" ; "?" )` | List contextual help commands |
| `sqls.Sugar ( "" ; "? intro" )` | An introduction to **sql-sugar**'s core functions |
| `sqls.Sugar ( "" ; "? chaning" )` | How to use **sql-sugar**'s chainable syntax |
| `sqls.Sugar ( "" ; "? query" )` | The `sqls.Query` wrapper function |
| `sqls.Sugar ( "" ; "? execute" )` | The `sqls.Execute` proxy function |
| | |
| `sqls.Sugar ( "" ; "? about" )` | Credits and terms of use (accurate only at the time of the original forking, this file takes that responsibility from now on) |
| `sqls.Sugar ( "" ; "? version" )` | Version number and history (accurate only at the time of the original forking, this file takes that responsibility from now on) |
| | |
| `sqls.Sugar ( "" ; "? fql intro" )` | An introduction to FileMaker's SQL dialect |
| `sqls.Sugar ( "" ; "? fql number" )` | Information about FQL number functions |
| `sqls.Sugar ( "" ; "? fql date" )` | FQL date/time/timestamp functions |
| `sqls.Sugar ( "" ; "? fql text" )` | FQL text/string functions |
| `sqls.Sugar ( "" ; "? fql meta" )` | FQL casting and meta functions |

Basic help commands may be shortened to their first letter. For example:  `sqls.Sugar ( ""; "? c" ) ` will display chainable syntax help.
 
FQL help may be shortened to `"fql"` plus the first letter. For example:  `sqls.Sugar ( ""; "? fql n" ) ` shows FQL number function help.

### Introduction

**sql-sugar** is easy to use, taking only 2 parameters: `sqls.Sugar ( _obj_or_val ;
_params )`.

`sqls.Sugar`'s initial `_obj_or_val` parameter is overloaded, allowing it to take either
a field, object (`Table::field`) or a text, numeric, date, time, or timestamp value,
basically, any object or value you might want in an FQL query.

`sqls.Sugar`'s second `_params` parameter takes a text string informing `sqls.Sugar` how
to parse the object or value passed. Later, in the *Chaining* section of help, we'll see
that params is also overloaded, and the basic funcitonality we'll discuss here is just
the tip of the iceberg. But, first things first…

#### Basic Use with Objects

`sqls.Sugar`'s first and most important function is easing the task of referencing data
objects in FileMaker SQL. In FQL this basic task presents a challenge: On the one hand,
fields and tables should always be wrapped in a `GetFieldName` function to ensure that
renaming tables or fields can't break our queries. But doing this creates a great deal of
visual clutter, making queries difficult to create and even harder to read and maintain.

Out of the box, **sql-sugar** greatly simplifies this task, by providing a light,
context-aware wrapper for objects. For example:

    sqls.Sugar ( Table::field ; "field" )
    // Returns a SQL-formatted field reference: `table.field`.

    sqls.Sugar ( Table::field ; "table" )
    // Returns the SQL-standard: `table`.

**sql-sugar** also compares each table and field referenced to reserved SQL keywords and
tests for multi-word names or other strings that, while valid in FileMaker, may not be
valid SQL names. In any of these cases, **sql-sugar** will automatically double-quote
these object names, making them safe for use in FQL queries without any need for
additional testing.

#### Basic User with Values

**sql-sugar** makes it as easy to reference values as data objects. Even better,
**sql-sugar**'s syntax is completely parallel for both object and value use. In the case
of values, `sqls.Sugar`'s overloaded `_obj_or_val` parameter accepts the value, and its
`_params` argument now takes an initial argument to inform the function how the value
received is to be treated.

Text and numeric values are treated like this:

    sqls.Sugar ( "hello 123" ; "text" )

Returns `'hello 123'`. Note that `sqls.Sugar` automatically places single quotes around
text values, making them ready for direct use in SQL queries.

    sqls.Sugar ( "hello 123" ; "number" )

Evalutes to `123`. When handling numeric values, `sqls.Sugar` automatically casts the
value as a number (in this example, retrieving only the numeric portion of the string
passed). Numeric values are correctly returned without quotation, ready for evaluation in
SQL expressions.

Date, time, and timestamp values can also be extracted as desired. As with numeric
values, `sqls.Sugar` casts these and retrieves the requested portion of the value
received. By default, these are returned in native FileMaker format.

    sqls.Sugar ( Get ( CurrentTimestamp ) ; "timestamp" )

Returns a single-quoted timestamp value in FileMaker-native format, such as
`'3/10/2013 6:15:42 PM'`.

    sqls.Sugar ( Get ( Currenttimestamp ) ; "time" )

Extracts and returns the single-quoted time portion of this value in FileMaker format,
such as `'6:15:42 PM'`.

    sqls.Sugar ( Get ( CurrentTimestamp ) ; "date" )

Returns a single-quoted date value in FileMaker format, such as `'3/10/2013'`.

**sql-sugar** also makes it easy to cast date, time and timestamp value in SQL-standard
format. To do this, simply append `"SQL"` to any of these operators.

    sqls.Sugar ( Get ( CurrentTimestamp ) ; "timestampSQL" )

Returns a single-quoted SQL ANSI timestamp, such as `'2013-03-10 18:21:35'`.

#### Value Literals

**sql-sugar** provides for a special value type of literal. This is intended for cases
where SQL keywords are to be passed directly to a query, without the normal wrapping in
single quotes.

    sqls.Sugar ( "and" ; "literal" )

Returns the SQL keyword `AND` without quotation. Although this may seem trivial at first
glance, this capability can be very helpful in creating consistent, structured queries.
The above could be shortened to `sqls.Sugar ( "and" ; "l" )`.

#### Syntactic Sugar for Objects

**sql-sugar** doesn't try impose a specific style of SQL on developers; in fact, it does
everything it can to empower developers to choose whatever style and form that best suits
their own approach.

One place this is evident is **sql-sugar**'s use of synonyms and shortened forms.
`sqls.Sugar ( <tbl::fld> ; "table" )` can be shortened to `sqls.Sugar ( <tbl::fld> ;
"tbl" )` or simply `sqls.Sugar ( <tbl:fld> ; "t" )`. Similarly, a `"field"` parameter can
be shorted to `"fld"` or even just `"f"`.

**sql-sugar** also understands the use of the more common SQL term, `"column"`, so that
`"field"` can be replaced by `"column"`, `"col"`, or `"c"`.

Finally, if the `_param` string is empty, `sqls.Sugar` will case the object as a field by
default, so that `sqls.Sugar ( <tbl::fld> ; "" )` is equivalent to `sqls.Sugar (
<tbl::fld> ; "field" )`.

#### Syntactic Sugar for Values

**sql-sugar** brings this same approach to values. For values, standard type parameters
can be shortened by using the FileMaker field type equivalent.

    sqls.Sugar ( <val> ; "t" ) // same as `sqls.Sugar ( <val> ; "text" )`
    sqls.Sugar ( <val> ; "n" ) // equivalent to `"number"`
    sqls.Sugar ( <val> ; "m" ) // equivalent to `"timestamp"`
    sqls.Sugar ( <val> ; "i" ) // equivalent to `"time"`
    sqls.Sugar ( <val> ; "d" ) // equivalent to `"date"`

The SQL-formatted variants may also be shortened by appending `SQL` to FileMaker data
types.

    sqls.Sugar ( <val> ; "mSQL" ) // equivalent to `"timestampSQL"`

### Chaining Parameters

Once you've mastered the basics, the real power of **sql-sugar** lies in its powerful and
highly flexible chainable syntax. While atypical in the FileMaker world, this approach is
common in many other environments like Ruby and a number of JavaScript libraries and meta
languages. Chainable syntax is powerful, light, and extensive, and particularly
well-suited to FQL. This ability to overload the `_params` parameter lies at the heart
of **sql-sugar**'s advanced capabiliites.

As we move on to move complex uses of **sql-sugar** using chaining, remember that the
lessons of the previous section still apply. The first word passed to `_param` will
continue to perform the special role of telling **sql-sugar** how to handle the object or
value passed. Everything else we do will build on top of this.

Let's start with a sneak peek at two chaining examples.

    sqls.Sugar ( <tbl::fld> ; "field lower()" )

This wraps a field in a `LOWER` function: `"LOWER ( tbl.fld )"`.

    sqls.Sugar ( <tbl::fld> ; "table inner join >> as:t on" )

This prepends and appends SQL to the table name: `"INNER JOIN <tbl> AS t ON"`.

#### Chaining Basics

**sql-sugar** recognizes that as we construct SQL queries, we typically wan to accomplish
3 tasks:

- Preface the query objects (fields, tables, or values) with SQL operators, string
  literals, delimiters, and spacers
- Append operators, string literals, delimiters, or spacers after a query object
- Wrap query objects within one or more SQL functions

**sql-sugar**'s chainable syntax makes it easy to do any combination of these things in a
concise, highly readable way. **sql-sugar**'s basic chaining rules are:

- Items (words) in a chain are delimited by whitespace.
- The first item in a chain is always special, telling **sql-sugar** how to parse the
  object or value received.
- Each item after the first will by default be placed to the left of the query object.
  For example, `sqls.Sugar ( <tbl::fld> ; "table left join" )` will evaluate as
  `"LEFT JOIN <tbl>"`.
- When the shift operator (`>>`) is used, chain items following it are placed to the
  right of a query object. For example, `sqls.Sugar ( <object> ; "table >> inner join" )`
  evaluates to `"<tbl> INNER JOIN"`.
- SQL functions are denoted by parentheses, such as `"lower()"`. Function items are
  exempt from left/right placement, and always wrap a query object. For example,
  `sqls.Sugar ( <object>; "field trim()" )` becomes `"TRIM ( <fld> )"`.

#### More Sugar

Because even a simple query can contain several objects, and thus will invoke
`sqls.Sugar` many times, even small savings in redundant syntax can make a big difference
in how easy it is to write and read. Again, **sql-sugar** offers several tools to help
developers streamline their chainable SQL to their simplest, most readable form.

##### The Dot Shorthand

One example of this is the dot shorthand. If a parameter chain begins with a dot,
`sqls.Sugar` will cast the object or value to its default type. The following pairs are
equivalent.

    sqls.Sugar ( <tbl::fld> ; "field trim()" )
    sqls.Sugar ( <tbl::fld> ; ". trim()" )

    sqls.Sugar ( <val> ; "field upper()" )
    sqls.Sugar ( <val> ; ". upper()" )

##### Spacers and Delimiters

One of **sql-sugar**'s more subtle but essential goals is to hlep developers create SQL
queries that are readable both as they're entered, but also after they're evaluated. To
aid in this, **sql-sugar** provides a spacer shorthand (`"_"`) and a delimiter shorthand
(`","`). So, for example, `sqls.Sugar ( <tbl::fld> ; ". , _" )` evaluates to
`",   tbl.fld"`.

This is especially useful and important in creating consistently delimited and indented
queries, and can help make otherwise unreadable queries very easy to visually parse.

##### Function Chaining

It's often useful to combine multiple SQL functions in combination in a query snippet.
**sql-sugar** makes this very easy to do, and allows 2 forms:

    sqls.Sugar ( <tbl::fld> ; ". lower() trim()" )
    sqls.Sugar ( <tbl::fld> ; ". lower(trim())" )

Both will evaluate to `"LOWER ( TRIM ( tbl.fld ) )"`.

##### Complex Functions

Many SQL functions simply wrap an object, like `LOWER()` and `TRIM()`. Others, like
`CAST()` and `SUBSTRING()`, require one or more additional parameters beyond the primary
object. **sql-sugar** provides two types of advanced parameter proxies. For functions
that require comma-separated parameters, use a colon separator, like this:

    sqls.Sugar ( <object> ; ". substring(:2:4)" ) // "SUBSTRING ( <object> , 2 , 4 )"

Some SQL functions instead require space-separated arguments. Use the pipe (`"|"`)
character in these cases.

    sqls.Sugar ( <obj> ; ". cast(|as|varchar|)" // "CAST ( <obj> as varchar )"

##### Table and Field Aliases

As our SQL becomes more advanced, it's often helpful to add table and/or field aliases.
**sql-sugar** provides a similar syntax used for complex functions.

    sqls.Sugar ( <obj> ; "t >> as=my_alias" ) // "<table> /* AS=>my_alias */ "

Note that `sqls.Sugar` does not, by itself, apply this alias, and instead packages the
alias in a formatted comment. In the next help section, we'll see how the query-level
function `sqls.Query` will detect aliases wrapped like this and apply them throughout the
query.

#### Care For Some Free Samples?

If this seems abstract, don't worry. A few examples should help make this clear. Let's
start with a basic query that shows basic **sql-sugar** shortcuts, and some left-hand
padding and delimited:

    List (
      "SELECT" ;
        sqls.Sugar ( projects::name ; ". _" ) ;
        sqls.Sugar ( projects::type ; ". ,_" ) ;
      "FROM" ;
        sqls.Sugar ( projects::id ; "t _" )
    )

This becomes:

    SELECT
      projects.name
    , projects.type
    FROM
      projects

Now let's add in a bit more complexity, with some simple and complex chained functions and a shift operator to push some text to the right too.

    List (
      "SELECT"
        sqls.Sugar ( projects::name ; ". _ trim ( substring (:5:10) ) )" ) ;
        sqls.Sugar ( projects::type ; ". , _ upper()" ) ;
      "FROM" ;
        sqls.Sugar ( projects::id ; "t _" ) ;
      "ORDER BY" ;
        sqls.Sugar ( projects::name ; ". _ lower() >> asc" ) ;
    )

The above evaluates to:

    SELECT
      UPPER ( TRIM ( SUBSTRING ( projects.name , 5 , 10 ) ) )
      UPPER ( projects.type )
    FROM
      projects
    ORDER BY
      LOWER ( projects.name ) ASC

Here's one last example with a bit more complexity.

    List (
      "SELECT" ;
        sqls.Sugar ( projects::id ; ". _" ) ;
        sqls.Sugar ( projects::name ; ". ,_ trim ( lower ())" ) ;
        sqls.Sugar ( "type: " ; ". ,_ >> & ) &
          sqls.Sugar ( projects::type ; ". lower()" ) ;
      "FROM" ;
        sqls.Sugar ( projects::id ; "t _ as:p" ) ;
      "WHERE" ;
        sqls.Sugar ( projects::name ; ". _ lower() >> LIKE 'a%' and" ) ;
        sqls.Sugar ( projects::order price ; ". _ >> < 25000" ) ;
      "GROUP BY" ;
        sqls.Sugar ( projects::name ; ". _ lower()" ) ;
      "HAVING" ;
        sqls.Sugar ( projects::order price ; ". _ sum() >> > 1500" )
    )

The above evaluates to:

    SELECT
      projects.id
    , TRIM ( LOWER ( projects.name ) )
    , 'type: ' & LOWER ( projects.type )
    FROM
      projects /* AS=>p */
    WHERE
      LOWER ( projects.name ) LIKE 'a%' AND
      projects."order price" < 25000
    GROUP BY
      LOWER ( projects.name )
    HAVING
      SUM ( projects."order price" ) > 15000

### `sqls.Query` Wrapper Function

The `sqls.Query` function is an optional wrapper function for FQL queries built with
`sqls.Sugar`. It normalizes and enhances these queries, and adds query-level parsing. It
performs three query-level functions:

- Pads and normalizes whitespace for better presentation.
- Analyzes the query passed to determine if it is simple ( contains just one table in its
  `FROM` clause and has no nested clauses) and if so, simplifies the query by removing
  unneeded `table.` prefixes throughout the query.
- Scans the query for table alises wrapped by upstream `sqls.Sugar` calls and if found,
  unpacks them, with the aliases replacing the raw table and field names throughout the
  query.

Version History
---------------

1.0 released by Brian Schick, 13-03-15
2.0 forked by Charles Ross, 16-02-28

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

