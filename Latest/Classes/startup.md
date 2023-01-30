`Startup` is a class that contains a list of functions mostly used in `My Scripts.ahk` to perform a variety of actions on script startup.
***

## <u>`generate()`</u>
This function will generate the settings.ini file if it doesn't already exist as well as regenerating it every new release to ensure any new .ini values are added without breaking anything.
```c#
generate()
```
***

## <u>`updateChecker()`</u>
This function will (on script startup, NOT a reload of the script) check which version of the script you're running, cross reference that with the latest release on github and alert the user if there is a newer release available with a prompt to download it. The GUI will offer the user the ability to see the changelog for the latest release, if they chose to do so, the latest release page on github will be loaded in a [`WebView2`](https://github.com/thqby/ahk2_lib/tree/master/WebView2) window

Which branch the user wishes to check for (either beta, or main releases) can be determined by either right clicking on `My Scripts.ahk` in the task bar and clicking  `Settings`, or by accessing `settingsGUI()` (by default <kbd>#F1</kbd>).

This script will also perform a backup of the users current instance of the "ahk" folder this script resides in and will place it in the `\Backups` folder.
```c#
updateChecker()
```
***

## <u>`firstCheck()`</u>
This function checks to see if it is the first time the user is running the `My Scipts.ahk` script. If so, they are then given a GUI containing some general information regarding the script as well as a prompt to check out some useful hotkeys.
```c#
firstCheck()
```
***

## <u>`oldError()`</u>
This function will (on script startup, NOT a reload of the script) delete any `\ErrorLog` files older than 30 days.
***

## <u>`adobeTemp()`</u>
This function will (on script startup, NOT a reload of the script) delete any Adobe temp files when they're bigger than the specified amount (in GB). Adobe's "max" limits that you set within their programs is stupid and rarely chooses to work, this function acts as a sanity check.

The minimum value for this function can be adjusted by either right clicking on `My Scripts.ahk` in the task bar and clicking  `Settings`, or by accessing `settingsGUI()` (by default <kbd>#F1</kbd>).

It should be noted I have created a custom location for `After Effects'` temp files to go to so that they're in the same folder as `Premiere's` just to keep things in one place. You will either have to change this folder directory within the function to the actual default or set the cache location within After Effects to the same place.
```c#
adobeTemp()
```
***

## <u>`locationReplace()`</u>
Within my scripts I have a few hard coded references to the directory location I have these scripts. That however would be useless to another user who places them in another location.

To combat this scenario, this function on script startup will check the working directory (and compare it against the value in `settings.ini`) and if they aren't the same, change all instances of MY hard coded dir to the users current working directory.

This script will take note of the users A_WorkingDir and store it in `A_MyDocuments \tomshi\settings.ini` and will check it every launch to ensure location variables are always updated and accurate.
***

## <u>`trayMen()`</u>
This function will add right click tray menu items to "My Scripts.ahk" to toggle checking for updates as well as accessing a GUI to modify script settings.
***

## class libs {
`libs` is a collection of information relating to external lib files used by my scripts. It contains; The name, url & script path for each file.

This information is then looped through by `libUpdateCheck()`


## <u>`libUpdateCheck()`</u>
This function will (on script startup, NOT a reload of the script) loop through `class libs {` and ensure that all listed libs are up to date.

This function will first attempt to look for `@version` tags, but if none exist in the file it will simply compare the local file to the downloaded file.
***

## <u>`updateAHK()`</u>
This function will check for the latest version of AHK and compare it to the current version, if there is a newer version available it will alert the user and prompt a download.
***

## <u>`monitorAlert()`</u>
This function logs the user's monitor setup so that it may alert the user when their monitor layout has changed.

This is important as any changes can seriously mess up any scripts that contain hard coded pixel coordinates.