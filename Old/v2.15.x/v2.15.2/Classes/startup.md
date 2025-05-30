`Startup` is a class that contains a list of functions mostly used in `My Scripts.ahk` to perform a variety of actions on script startup.
***

## <u>`generate()`</u>
This function will generate the settings.ini file if it doesn't already exist as well as regenerating it every new release to ensure any new .ini values are added without breaking anything.

> [!Note]
> This function will also automatically set the `MainScriptName` variable within `settings.ini` based off the script name that calls this function. As such it is recommended to use this function in your own version of `My Scripts.ahk` presented in this repo.
```c#
start := Startup()
start.generate()
```
***

## <u>`updateChecker()`</u>
This function will (on script startup, NOT a reload of the script) check which version of the script you're running, cross reference that with the latest release on github and alert the user if there is a newer release available with a prompt to download it. The GUI will offer the user the ability to see the changelog for the latest release, if they chose to do so, the latest release page on github will be loaded in a [`WebView2`](https://github.com/thqby/ahk2_lib/tree/master/WebView2) window

Which branch the user wishes to check for (either beta, or main releases) can be determined by either right clicking on `My Scripts.ahk` in the task bar and clicking  `Settings`, or by accessing `settingsGUI()` (by default <kbd>#F1</kbd>).

This script will also perform a backup of the users current instance of the "ahk" folder this script resides in and will place it in the `\Backups` folder.
```c#
start := Startup()
start.updateChecker()
```
***

## <u>`updatePackages()`</u>
This function will check for any updates in the user's package manager. If any are available they will be prompted asking if they wish to update.
> [!Important]
> The code for this function is designed around `chocolatey` and may not function with other package managers. The code to send the upgrade command specifically is also choco specific
```c#
start := Startup()
start.updatePackages( [{packageManager := "choco", checkOutdated := "choco outdated", noUpdatesString := "has determined 0 package(s) are outdated", nonChocoUpdateCommand := "", ignore := []}] )
```

#### *packageManager*
Type: *String*
> This parameter is the cmdline command for the desired package manager. ie. `choco`

#### *checkOutdated*
Type: *String*
> This parameter is the command for the user's respective package manager to check if any packages are outdated.

#### *checkOutdated*
Type: *String*
> This parameter is the string the cmdline usually gives the user in the event that no updates are available.

#### *checkOutdated*
Type: *String*
> This parameter is an alternative command given to the commandline to update all installed packages as the update code in this function is specific to chocolatey.

#### *ignore*
Type: *Array/String*
> An array of strings with the names of any packages you wish to ignore. ie; `["vcredist"]`
***

## <u>`updateAdobeVerAHK()`</u>
Updates a user's adobe `vers.ahk`/`adobeVers.ahk` file so that they may select newer versions of adobe programs without needing to wait for a full release.
***

## <u>`firstCheck()`</u>
This function checks to see if it is the first time the user is running the `My Scipts.ahk` script. If so, they are then given a GUI containing some general information regarding the script as well as a prompt to check out some useful hotkeys.
```c#
start := Startup()
start.firstCheck()
```
***

## <u>`oldLogs()`</u>
This function will (on script startup, NOT a reload of the script) delete any `\ErrorLog` files older than 30 days.
***

## <u>`adobeTemp()`</u>
This function will (on script startup, NOT a reload of the script) delete any Adobe temp files when they're bigger than the specified amount (in GB). Adobe's "max" limits that you set within their programs is stupid and rarely chooses to work, this function acts as a sanity check.

The minimum value for this function can be adjusted by either right clicking on `My Scripts.ahk` in the task bar and clicking  `Settings`, or by accessing `settingsGUI()` (by default <kbd>#F1</kbd>).

It should be noted I have created a custom location for `After Effects'` temp files to go to so that they're in the same folder as `Premiere's` just to keep things in one place. You will either have to change this folder directory within the function to the actual default or set the cache location within After Effects to the same place.
```c#
start := Startup()
start.adobeTemp()
```
***

## <u>`adobeVerOverride()`</u>
This function will set the current Premiere Pro/After Effects version based off the current .exe version (only if `UserSettings.adobeExeOverride` is set to `true`). If `UserSettings.adobeExeOverride` is set to `false` the user **must** set the version themselves within `settingsGUI()`
> [!Tip]
> This function will also show the user the currently selected Adobe versions during script startup. This functionality can be disabled in `settingsGUI()`
```c#
start := Startup()
start.adobeVerOverride()
```

> [!Caution]
> This function will attempt to also set the correct `Year` variable but may not work as expected under certain circumstances (including if the user has multiple year versions of Premiere installed).  
> It is best to double check that it is set correctly within `settingsGUI()`
***

## <u>`trayMen()`</u>
This function will add right click tray menu items to "My Scripts.ahk" to toggle checking for updates as well as accessing a GUI to modify script settings.
***

## class libs {
`libs` is a collection of information relating to external lib files used by my scripts. It contains; The name, url & script path for each file.

This information is then looped through by `libUpdateCheck()`

***
## <u>`libUpdateCheck()`</u>
This function will (on script startup, NOT a reload of the script) loop through `class libs {` and ensure that all listed libs are up to date.  
This function will first attempt to look for `@version` tags, but if none exist in the file it will simply compare the local file to the downloaded file.
```c#
start := Startup()
start.libUpdateCheck()
```
***

## <u>`updateAHK()`</u>
This function will check for the latest version of AHK and compare it to the current version, if there is a newer version available it will alert the user and prompt a download.
```c#
start := Startup()
start.updateAHK()
```
***

## <u>`monitorAlert()`</u>
This function logs the user's monitor setup so that it may alert the user when their monitor layout has changed.  
This is important as any changes can seriously mess up any scripts that contain hard coded pixel coordinates.
```c#
start := Startup()
start.monitorAlert()
```
***

## <u>`checkShortcuts()`</u>
A function to rudimentarily check if any shortcuts have been generated in the shortcuts folder. If they haven't it will run a script in an attempt to generate them.
> [!Important]
> It should be noted the script mentioned assumes the adobe programs have been installed to their default locations.