## PluginChecker Version History


### 1.1.0

released 2015-MAY-29

  - add sample config script for Mailit plugin
    - includes an alternate method of defining the versionTest parameter
  - add $registrationExpression to all sample config scripts
  - add $name to all sample config scripts


### 1.0.0

released 2015-MAY-22

  - improved some log messages
  - prevent error dialog in Create Log Entry script
  - delete PluginChecker: ooScriptMaster sample script


### 0.3.0

released 2015-FEB-11

  - add scriptStack when sub-script returns an error
  - clear Get ( LastError ) before exiting script
  - update documentation
  - move all steps from public scripts to private scripts
  - remove config script used to modify the script result. User can now modify the public script to modify the script result.
  - return pluginName and pluginVersion with result when testing a plugin
  - add support for registering a plugin
  - encode time as "TimeStamp" instead of "CurrentTimeUTCMilliseconds" when creating log entry
  - modify Unit Tests and "PluginChecker: BaseElements" script to use versionFunction parameter
    - old versions of a plugin may return an unexpected value to the Get ( InstalledFMPlugins ) function so it's recommended to always use the versionFunction parameter, to ensure compatibility when a client computer has and old version of the plugin already installed. (unless you can ensure that all clients either don't have the plugin already installed, or have a version of the plugin that returns a version to the Get ( InstalledFMPlugins ) function, in an expected format)
  - move this module to a separate file


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
