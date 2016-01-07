fm-library Conventions
======================

Here you'll find the documentation for the various conventions and standards used
throughout the fm-library project. Note that the all the documentation is found within
the fm-library.fmp12 file itself.

Tables
------

- The `Tables` tab of the `Manage Database` dialog is organized by placing tables into
  various groups. Groups are headed by tables that begin with underscore and the name of
  the heading in all capital letters, as in `_____ MAIN TABLES`. These heading tables have
  no fields and no associated table instance. Table groups include:
    - Main Tables (generally tables that provide layout context)
    - Join Tables (generally tables that appear only within portals)
    - Aux Tables (data tables that perhaps don't fit into the above two groups, such as
      `Users` or `Preferences`).
    - Utility Tables (tables controlled solely by the developer, such as `Connector` and
      `Interface`)
- Tables are named with camel case using the plural of the entity to be stored, as in
  `Files` and `LineItems`.

Fields
------

- Fields are grouped using a system similar to that of tables, in this case with global
  number fields that are named beginning with a few underscores, the name of the group,
  and additional underscores to provide separation between groups. An example would be
  `____ DEFAULT FIELDS ________________________`.
- Fields are named in snake case with all lowercase letters, such as `uuid` and
  `date_created`.
- The default groups for field and the default fields within each group include:
    - Default Fields (fields included in every data table)
        - `uuid: the primary key for the table
        - `seq_id: an auto-enter number fields for when a unique number is required by
          users
        - `date_time_created`: an auto-enter of the creation timestamp
        - `date_created`: a calculation that converts the above into a date
        - `date_time_modified`: an auto-enter of the modification timestamp
        - `date_modified`: a conversion of the above into a date
        - `created_by`: auto-enter of the creation account name
        - `modified_by`: auto-enter of the modification account name
        - `table_code`: a calculation that returns the unique three-letter code for the
          table, which must match the main table instance name for the table
        - `table_comment`: a comment explaining the purpose of the table
    - Foreign Keys
    - Developer (fields used solely for the developer)
        - g_one: a calculation that returns `1`, used for utility relationships that have
          boolean keys as the match field on the other side
        - empty: Never used for anything other than record creation through a selector
          relationship
    - Table Specific Fields (fields for the end user)

Relationships
-------------

- Every table gets one automatic table instance with a name that corresponds to the
  table's three-letter code.
- Every table, other than the `Connector` table itself, gets a cross-join relationship to
  `Connector` using the `uuid` field as the match fields on both sides of the
  relationship.
- Table instances are named using the path from the `CON` (`Connector`) table instance
  using the table codes as the names, separated by underscores. The table code of the
  associated table is in capital letters and all other table instances are in lowercase.
  If such a naming convention does not result in a unique name, a tilde (`~`) is
  appended, followed by a descriptive name. This results in table instance names such as
  `inv_lit_PRD` (for a table instance that links to `Products` and has a path through
  `Invoices` and `LineItems`) or `sel_INV~create` (for a table instance that links to
  `Invoices` through the `SEL` table instance and is used to create record in that table).
- Every data table is provided with two relationships to the `SEL` table instance. The
  first is `sel_XXX~create` and the second is `sel_XXX~selected`. The `Selector` table
  has a global text field, `g_create_uuid`, that serves as the match field in the
  `*~create` relationships with the table's `uuid` field serving as the other match
  field. The relationship to `*~create` table instances is set to allow the creation of
  related records. Each data table has an associated field in the `Selector` table, named
  as `g_xxx_uuid`, where "`xxx`" is the table code. The `*~selected` relationships use
  this as the `SEL` match field with `uuid` serving as the other match field.

Scripts
-------

Calculations
------------

Custom Functions
----------------

### Dividers

### Function Names

### Parameters

### Preamble

### Script Variables
