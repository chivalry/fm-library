## PluginManager Version History


### 1.1.0

released 2015-MAY-29

  - store container data in the FM file instead of externally
  - add button to install plugin on server from UI
  - allow "Install and View" privilege set to import data and re-login
  - allow "Install" privilege set to re-login
  - add button on Installed Plugins portal which allows for viewing the servers plugins (only visible if the file is hosted), and not available from the FM12 UI


### 1.0.0

released 2015-MAY-22

  - add support for FileMaker 14
  - add script for installing a single un-named plugin
  - improved some error messages
  - prevent error dialog in Create Log Entry script
  - update privilege sets to work with all new scripts
  - bug fix: when adding a record to the file portal: "Select File" dialog was shown twice when clicking the "Select File" button


### 0.3.0

released 2015-FEB-11

  - add scriptStack when sub-script returns an error
  - clear Get ( LastError ) before exiting scripts
  - close the current file, if it's hidden, after installing a plugin
  - update documentation
  - move all steps from public scripts to private scripts


### 0.2.0

released 2014-AUG-28

  - bug fixes
  - additional data sent to log script
  - additional documentation
  - add support for installing a plugin on the web publishing engine from Web Direct


### 0.1.0

released 2014-AUG-26

  - initial beta release
  - limiting testing has been done; please test thoroughly before putting this version into production
  - is not installing plugins on the server; not sure why yet
