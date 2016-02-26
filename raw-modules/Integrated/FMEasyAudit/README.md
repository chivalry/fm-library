<img src="fmeasyaudit_logo.png" width="30" height="30"> FMEasyAudit
===================================================================

This is my own GitHub fork of Tim Dietrich's excellent FMEasyAudit FileMaker logging solution. At the start, it's just going to be a set up of the project organized for GitHub, but eventually I'll be adding features and perhaps updating the solution to more closely conform to the [modularfilemaker.org](http://modularfilemaker.org) standards. The documentation below is taken directly from Tim's original [fmeasyaudit.com](http://fmeasyaudit.com) web site, and so may be slightly wrong in some cases, particularly with the download links. All that will be corrected at some point in the near future.

FMEasyAudit is an open source solution for implementing logging and auditing of FileMaker
databases.

Here are some of FMEasyAudit's features:

- Supports logging of updates, deletions, imports, and more.
- Logs container fields, repeating fields, etc.
- Uses only native FileMaker functionality.
- Easy setup and configuration.
- No additional files are needed.
- Fast, with little to no impact on performance.
- Provided via an open source license.

FAQ
---

**What is FMEasyAudit?**
FMEasyAudit is a solution that can be used to automatically log the actions that users
take in a FileMaker database. The "audit log" (or "audit trail") that FMEasyAudit
generates includes detailed information about changes that users have made. The log can
be used to review what users have done, and can potentially be used to "rollback" (or
"undo") their actions.

**Why would I want to use FMEasyAudit in my FileMaker solutions?**
Depending on how you implement FMEasyAudit, you can review the audit log to determine who
made changes to a record, who deleted a record, the records that a user viewed, and more.
It is a great way to add an extra level of security to your solutions.

**What is involved in setting up FMEasyAudit?**
Setting up FMEasyAudit in a fairly simple solution (a few tables and layouts) usually
takes less than an hour. However, the process may take a bit longer depending on the
number of layouts that you want to audit changes from, the number of tables that you want
to audit, and the degree to which you want to audit the database. For example, you can
optionally choose to audit deletions, imports, and more. [Setup instructions](#setup) are found below.

**What type of information is included in the log that FMEasyAudit creates?**
The log entries include:

- Transaction ID: A UUID value assigned to related log entries. For example, when making
changes to a parent record and related children, the log entries will be assigned the
same Transaction ID.
- TimeStamp: The date and time that the action was taken.
- Account Name: The name of the FileMaker account that was used to make the change.
- Entry Type: The type of action that the user took, or the type of entry. For example,
"Audit" entries indicate that a user made changes to an existing record or has added a
new record. Additional entry types include Delete, Import, Baseline, Login, Logout, and
more.
- Table Name: The name of the base table to which the changes were made.
- EA UUID: The EasySync-assigned unique ID for the record that was modified.
- Record Mod Count: The modification count of the record.
- Field Name: The name of the field whose value was changed.
- Field Repetition: The repetition of the field whose value has changed. (Particularly
relevant to repeating fields.)
- Previous Field Value: When applicable, the value of the field prior to the change that
the user made.
- Field Value: The value that the user changed the field to.
- Field Value Container: In cases where the field that was changed is a container, this
calculated field can be used to display the the container's contents.
- Note: An optional note or comment about the logged event.

**Where are the log entries stored?**
EasyAudit writes all changes to a separate "EasyAudit" table in the database.

**What types of events does FMEasyAudit log?**
EasyAudit can be used to log the following event types:

- Changes to field values, and values applied to new records.
- Changes made to the fields of multiple records using the Replace Field Contents command.
- Record deletions.
- Records added or modified as the result of an import process.
- Database logins and logouts.
- Baselines, where field values for one or more records are logged, regardless of whether
their values have been changed or not.

You can also use FMEasyAudit to write ad-hoc entries to the log, including errors, the
status of automated processes, etc.

**Does FMEasyAudit support the logging of container fields?**
Yes.

**Does FMEasyAudit support the logging of repeating fields?**
Yes.

**How does FMEasyAudit log changes made to records?**
EasyAudit uses an OnRecordCommit script trigger to initialize a server-side script, which
monitors the database and logs changes that have been successfully committed.

**Does FMEasyAudit support rollbacks?**
The initial beta release of FMEasyAudit does not include support for rollbacks.

We are working on implementing rollbacks in the next beta. You will be able to rollback
individual field-level changes, a batch of related changes, as well as record deletions.

**Does FMEasyAudit require any FileMaker plugins?**
No. FMEasyAudit uses only native FileMaker functions, so no plugins are needed.

**Is a demo database available?**
Yes, and you can [download it here](https://github.com/chivalry/FMEasyAudit/blob/master/EasyAudit_Beta_02/FMEasyAudit_Demo_B2.fmp12).

**What versions of FileMaker are supported?**
EasyAudit works with the FileMaker 13 platform. It supports clients running FileMaker
Pro, FileMaker Pro Advanced, FileMaker Go, and FileMaker WebDirect.

**Does FMEasyAudit work with WebDirect?**
Yes. FMEasyAudit can be used to log the actions of users who are accessing a database via
FileMaker WebDirect.

**Does FMEasyAudit work in databases that are being accessed locally or via peer-to-peer
networking?**
No. FMEasyAudit only works in databases that are being hosted using FileMaker Server 13
(or later).

**How much does FMEasyAudit cost?**
Nothing. FMEasyAudit is being provided via an open source license. You'll find a copy of
the license in the FMEasyAudit zip file.

**Is it possible for some users to bypass FMEasyAudit?**
Yes. Like most auditing solutions, you will need to be careful to configure FMEasyAudit
so that it logs the various actions that users might take, and the means by which they
take those actions. For example, to ensure that all record changes and additions are
logged, you will need to configure all layouts that users might use to perform those
actions. To log certain actions (imports, "replace field contents," etc), you will also
need to script those actions and make the appropriate calls to FMEasyAudit.

**Who developed FMEasyAudit?**
EasyAudit was developed by [Tim Dietrich](http://timdietrich.me/), a database consultant that develops custom
databases using the FileMaker platform. The techniques that FMEasyAudit uses are based in
large part on the work that Tim did on [FMEasySync](http://fmeasysync.com/).

<a name="setup"></a>Setup and Configuration
-----------------------

To configure your database for use with FMEasyAudit, follow these instructions.

1. **Copy (or import) the `EasyAudit` table from the demo file.**

    The `EasyAudit` table is used to store the log entries.

2. **If necessary, add an `EasyAudit` layout to your database.**

    After adding the `EasyAudit` table, FileMaker should have automatically created an
    `EasyAudit` layout for you. If not, create a layout, name it `EasyAudit`, and base it
    on the `EasyAudit` table occurrence.

3. **In the tables that you will be auditing, add the `EA` fields.**

    The `EA` fields include `EA_UUID`, `EA_Modifier`, `EA_Mod_Timestamp`, and
    `EA_Mod_Count`. The easiest way to add these fields is to copy and paste them from
    the demo database into your tables. Please refer to the demo database for the field
    types, auto-enter options, etc.

    Also, for container fields, add the corresponding `B64_` field. (Again, see the demo
    database for the calculation.)

4. **Import the FMEasyAudit script from the demo file.**

5. **For layouts that you want to audit record changes, add an `OnRecordCommit` script
trigger.**

    Configure the script trigger to so that it calls the `EasyAudit` script and passes
    `"Commit"` as a script paramater. Refer to the `Survey - Details` layout of the demo
    database for an example.

6. **If there are existing records in the database, set their `EA_UUID` field values.**

    In the tables that you added the EA fields to, set the value of the `EA_UUID` fields
    in all records using this calculation: `Get ( UUID )`. You can do so using the
    `Replace Field Contents` command.

7. **Optionally, you can perform a "Baseline" audit of the database.**

    This "baseline" will log the current values of all fields and all records in the
    database. Performing the baseline is optional, but recommended. To call FMEasyAudit's
    baseline function, call the `FMEasyAudit` script and pass it a parameter of
    `"Baseline"`. For an example, see the `Example: Baseline (All Records)` script in the
    demo database.

8. **Setup optional auditing.**

    FMEasyAudit also supports the logging of record deletions (via `Delete Record` and
    `Delete All Records`), user Logins and Logouts, changes made via the `Import Records`
    and `Replace Field` Contents" commands, and more. To implement the logging of these
    actions, you will need to script them. See the FMEasyAudit demo for examples.

9. **Enhance the appearance of the FMEasyAudit layout. (Optional)**

    How you present the audit log is entirely up to you. The easiest way to do so is to
    view the layout in table mode. For a very basic example, see the FMEasyAudit demo
    database.

FileMaker Accounts
------------------

There are three accounts set up in the FMEasyAudit database:

|Account Name|Password |Privilege Set  |
|------------|---------|-------------  |
|Admin       |fmezaudit|Full Access    |
|User1       |fmezuser1|Data Entry Only|
|User2       |fmezuser2|Data Entry Only|

Using The FMEasyAudit Demo Database
-----------------------------------

FMEasyAudit must be hosted on a server running FileMaker Server 13 or later.

To access the database, you can use any of the FileMaker 13 platform clients, including FileMaker Pro, FileMaker Pro Advanced, FileMaker Go, and FileMaker WebDirect.

Wish List
---------

Here are some of the feature requests that we've received and are considering.

### User-Definable Field Names

This request is to allow the developer to use existing fields instead of having to add
FMEasySync's `EA` fields (`EA_UUID`, `EA_Mod_Count`, `EA_Modifier`, and so on) to their
tables.

We're hoping to implement this feature in the next release. In the meantime, you can
customize EasyAudit to use your existing fields. The change that you'll need to make is
isolated to a single script step. It's located at around line 155 (just under the comment
that reads, `Add this table to the SELECT statement.`) There you will see a `Set
Variable` script step, with this value:

    If ( not IsEmpty ( $select ); $select & " UNION ALL "; "" ) & "SELECT '" & $table_name & "', EA_UUID, EA_Mod_Count FROM " & $table_name & " WHERE ( NUMVAL ( EA_Mod_Timestamp ) >= " & GetAsNumber ( $TS_Pre_Commit ) & " ) AND ( EA_Modifier = '" & $Account_Name & "' )"

You will need to change the references to the "EA_" fields so that the references are to the names of your own fields.

Special thanks to [Dave Graham](https://twitter.com/bittailor) for making this suggestion!

License
-------

License Agreement for FMEasyAudit

This software is supplied to you by Timothy Dietrich in consideration of your agreement to the following terms, and your use, installation, modification or redistribution of this software constitutes acceptance of these terms. If you do not agree with these terms, please do not use, install, modify or redistribute this software.

In consideration of your agreement to abide by the following terms, and subject to these terms, Timothy Dietrich grants you a personal, non-exclusive license, to use, reproduce, modify and redistribute the software, with or without modifications, in source and/or binary forms; provided that if you redistribute the software in its entirety and without modifications, you must retain this notice and the following text and disclaimers in all such redistributions of the software, and that in all cases attribution of Timothy Dietrich as the original author of EasySync shall be included in all such resulting software products or distributions.

Neither the name, trademarks, service marks or logos of Timothy Dietrich may be used to endorse or promote products derived from the software without specific prior written permission from Timothy Dietrich. Except as expressly stated in this notice, no other rights or licenses, express or implied, are granted by Timothy Dietrich herein, including but not limited to any patent rights that may be infringed by your derivative works or by other works in which the software may be incorporated.

The software is provided by Timothy Dietrich on an "AS IS" basis. TIMOTHY DIETRICH MAKES NO WARRANTIES, EXPRESS OR IMPLIED, INCLUDING WITHOUT LIMITATION THE IMPLIED WARRANTIES OF NON-INFRINGEMENT, MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE, REGARDING THE SOFTWARE OR ITS USE AND OPERATION ALONE OR IN COMBINATION WITH YOUR PRODUCTS.

IN NO EVENT SHALL Timothy Dietrich BE LIABLE FOR ANY SPECIAL, INDIRECT, INCIDENTAL OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) ARISING IN ANY WAY OUT OF THE USE, REPRODUCTION, MODIFICATION AND/OR DISTRIBUTION OF THE SOFTWARE, HOWEVER CAUSED AND WHETHER UNDER THEORY OF CONTRACT, TORT (INCLUDING NEGLIGENCE), STRICT LIABILITY OR OTHERWISE, EVEN IF Timothy Dietrich HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Note: FileMaker® is a registered trademark of FileMaker Inc. 

For additional information, please contact:

Timothy Dietrich
Postal Address: 2711 Buford Road, Suite #163, Richmond, VA 23235-2433 USA
Email: timdietrich@me.com
Web: http://timdietrich.me
Twitter: @tdietrich

Change Log
----------

EasyAudit Demo - Change Log

Beta 2 (11-15-2014)
- The single "EasyAudit" script has been split into several smaller, modularized scripts.
- User-definable `EA_` fields are supported. You'll see settings for these in the `EasyAudit - Settings` script.
- The demo database now includes an `Audit Log` tab, as an example of how you can view related entries in the log, including those of related records. I have added an `EA_UUID_List` field to the Surveys table, and a new relationship between Surveys and the EasyAudit table (as table occurrence "Survey_Log") to illustrate this functionality.
- The "Open Log" function will now display all log entries if no script param is passed, or a list of log entries based on a list of records (if a list of EA_UUID values passed to it). The demo database's "Open Log" button is an example of how you can use this to open the log viewer and see logs for the parent and child records.
- Added a new `$$ea_baseline_deletes` setting. If enabled, EasyAudit will take a baseline of a record (or records) prior to logging the deletion. This is enabled by default.
• Bug Fix: The "Tail" button (on the EasyAudit layout) is now wired up properly to the "EasyAudit - Tail Log" script.
- Bug Fix: Added support for non-SQL-compliant base table names and table occurrence names.
- Renamed a few settings. $$omit_tables is now $$ea_omit_tables. $$timeout_seconds is now $$ea_timeout_seconds.
- Log "Entry Types" now more accurately reflect new and changed values. If the value being logged is in a field that previous had no log entry, then it will appear in the logs as "New Value." Otherwise, it shows as a "Changed Value."

Beta 1 (Posted 09-18-2014)
- Initial beta released.
- Includes examples of all core auditing functions.
- No support for "rollbacks" yet.
