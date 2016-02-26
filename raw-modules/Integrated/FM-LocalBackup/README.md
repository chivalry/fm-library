# FM-LocalBackup

Local Backup creates backup copies of non-hosted FileMaker solutions during development. Since some developers prefer to work on files locally, not hosted on a server, they miss out on the backup features of FileMaker Server. This module gives developers a substitute backup mechanism.

## Attributions

This module is inspired by (copied from) solutions by [Kevin Frank][1] (with help from [Bruce Robertson][2]) and [Michael Rocharde][3].

[1]: http://www.filemakerhacks.com/?p=5293 "A Simple Backup Script, revised"
[2]: http://www.concise-design.com "Concise Design"
[3]: http://itunes.apple.com/us/book/filemaker-me/id532231582?mt=11 "FileMaker & Me"

## Usage

To create a local backup right now, run the "Create Local Backup of All Solution Files" script.

To start making local backups automatically every 10 minutes, run the "Start Auto Backup" script. The backup interval can be changed by editing the "Get Local Backup Settings" script. To stop making local backup automatically, just close the auto-backup window, which will stop the OnTimer trigger from firing.

## Installation

As a best practice, I recommend choosing one file to act as your solution's "dispatch" file. Then steps 2-N only have to be performed in the dispatch file.

1. Copy the "Local Backup" script folder into the "Modules" folder of each file in your solution.
2. In each non-dispatch file, edit the "Create Local Backup of All Solution Files" script to call the "Dispatch Backup of All Solution Files" script from the dispatch file.
3. In the dispatch file, edit the "Create Local Backup of Solution File ..." script to reference each file in your solution.
4. In the dispatch file, edit the "Go to Auto Backup Layout" script to specify a layout in your solution to use as the Auto Backup splashscreen. Auto Backups use a dedicated window with an OnTimer trigger to run repeated backups without interfering with any OnTimer triggers you may be using with other windows. This layout specifies what to display in that window.
5. (optional) In the dispatch file, edit the "Get Local Backup Settings" script to use a non-default backup path, auto-backup interval, auto-backup window name, or auto-backup window position. See Configuration Options for more information.

## Configuration Options

By default, Local Backup saves the backup copies of files to a timestamped folder within a "Backup" folder within the same directory as the solution files. Developers can choose to save to a different location by modifying the "Get Local Backup Settings" script to return a different backupFolderPath result.

By default, the auto backup runs every 10 minutes. Developers can choose a different OnTimer interval by modifying the "Get Local Backup Settings" script to return a different backupIntervalSeconds result. If you change the setting while auto-backup is active, the new interval takes effect at the end of the next backup.

The auto-backup window name and initial position can be changed by editing the "Get Local Backup Settings" script.

## License

Anyone may do anything with this software. There is no warranty.