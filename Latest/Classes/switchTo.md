A list of `switchTo` Functions complete with definitions.

All `switchTo` functions are contained within a class called `switchTo` and are called like: `switchTo.X()`

The idea behind these functions was initially showcased by [Taran](https://github.com/TaranVH/2nd-keyboard) a previous editor for LTT.

Their main purpose is to;

* If an instance of the desired program doesn't exist, open it
* If an instance of the desired program DOES exist, activate it
* If multiple instances of the desired program exists, cycle between them based off the last active

A list of `switchTo.` scripts based off this premise includes;

* `switchTo.Explorer()`
    * Includes parameter `toggleFullscreen := false` ; To determine whether you wish for the explorer window to be toggled fullscreen and then back to normal when running a new explorer instance. There are reports that doing this improves explorer responsiveness.
* `switchTo.Premiere()`
* `switchTo.AE()`
    * `switchTo.Premiere()` & `switchTo.AE()` will require the user to properly generate (or manually create) shortcuts that link the the `.exe` for both programs and place them in `..\Support Files\shortcuts\`. This can also be achieved by opening the individual settings menu within `settings()` and either adjusting the `Year` drop down or by toggling the beta checkbox
* `switchTo.Disc()`
    * I have this function move my discord window to a specific position if it's not already. Check that position at the top of the script
* `switchTo.Photoshop()`
* `switchTo.Firefox()`
* `switchTo.OtherFirefoxWindow()`
    * I use this in other functions for various reasons
* `switchTo.Chrome()`
* `switchTo.VSCode()`
* `switchTo.Streamdeck()`
* `switchTo.Excel()`
* `switchTo.Word()`
* `switchTo.WindowSpy()`
* `switchTo.Edge()`
* `switchTo.Music()`
* `switchTo.Slack()`
* `switchTo.ahkDocs()`
***

# Other functions in this file include

## `switchTo.closeOtherWindow()`
This function when called will close all windows of the desired program EXCEPT the active one. Helpful when you accidentally have way too many windows open.
```c#
switchTo.closeOtherWindow( [program {, ttip := true}] )
```
#### *program*
Type: *String - Program Information*
> Either `ahk_exe program.exe` or a `ahk_class x` of the desired program.

#### *ttip*
Type: *Boolean*
> Determine whether the user wishes for the function to present a tooltip upon completion that displays how many windows were closed.
***

## `newWin()`
This function is specifically designed for my secondary keyboard and works in tandom with the [`switchTo()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions) functions.

If the desired program isn't already open, it will run a first instance, if the desired program is already open, it will run a second instance without disrupting the first.
```c#
switchTo.newWin( [classorexe, activate, runval] )
```
#### *classorexe*
Type: *String*
> This parameter is just defining whether the function is trying to grab the `ahk_class` or the `ahk_exe` value of the desired program.

#### *activate*
Type: *String*
> This parameter is whatever usually comes after the `ahk_class` or the `ahk_exe` value of the desired program.

#### *runval*
Type: *String - Filepath*
> This parameter is whatever you would normally need to feed into a `Run()` command to open the desired program. Either a full file path, or something along the lines of `explorer.exe`, `firefox.exe`, etc.
***

## `adobeProject()`
This function opens the current `Premiere Pro`/`After Effects` project filepath in windows explorer.
> If prem/ae isn't open it will attempt to open the `ptf.comms` folder.
```c#
switchTo.adobeProject( [{optionalPath := "", switchCurrentWindow := true}])
```
#### *optionalPath*
Type: *String*
> This parameter allows the user to navigate to a directory beyond (or before) where the project file is located. See example #1 for more.

#### *switchCurrentWindow*
Type: *Boolean*
> Determines whether to change the current active window to the desired path, or whether to always open a new window

#### Return Value
Type: *Boolean*
> returns `true/false` whether the function succeeded or failed

Example #1
```ahk
;// will open the folder before where the project file is located
switchTo.adobeProject("..\")

;// will open the `videos` folder in the same dir as the project folder (if it exists)
switchTo.adobeProject("\videos")
```
***

## `Path()`
A function to nagivate the desired explorer window to the desired path
```c#
switchTo.Path( [FullPath {, hwnd := ""}])
```
#### *FullPath*
Type: *String*
> The full path you wish to navigate to

#### *hwnd*
Type: *String/Boolean*
> The hwnd of the window you wish to operate on. Defaults to the active window