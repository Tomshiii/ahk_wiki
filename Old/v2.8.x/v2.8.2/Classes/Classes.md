Within the `..\lib\Classes\` directory is a whole bunch of individual class files that give the user access to useful functions of various nature. All (or in case I ever change it, *most*) classes are called like: `class.func()`
***
### Table of Contents:
* [tool](#class-tool-)
* [coord](#class-coord-)
* [block](#class-block-)
* [WinGet](#class-WinGet-)
* [Pause](#class-Pause-)
* [Move](#class-Move-)
* [Startup](#class-Startup-)
***

## class tool {
This class contains two tooltip functions that help with tooltip creation and management.

## <u>`Cust()`</u>
This function allows the creation of a tooltip with any message, for a custom duration. This tooltip will then (under most conditions) follow the cursor and only redraw itself if the user has moved the cursor.

> *note: If the user passes either an `x OR y` value to this function (but not both), it will offset the tooltips position by that value from the cursor.

>If the user passes both an `x AND y` value to this function, the tooltip will no longer follow the cursor and instead be planted at those coordinates (the function uses the `Screen` coordinate position).*

>> *If you wish to replicate typical `ToolTip()` placement behaviour, follow Example #2 below.*
```
tool.Cust( [message, {timeout, find, x, y, WhichToolTip}] )
```
#### *message*
Type: *String*
> This parameter is whatever you wish the tooltip to display.

#### *timeout*
Type: *Integer/Float*
> This parameter is the duration you wish the tooltip to last. By default, this value is set to `1000ms` (`1s`).

> If you wish to give this variable in ms, pass in a whole integer, eg `2000`, if you wish to give this variable in seconds, pass this variable as a float, eg `2.0`.

#### *find*
Type: *Boolean*
> This variable determines whether you want this function to state "Couldn't find " at the beginning of it's tooltip. Simply add 1 (or true) for this variable if you do, or omit it if you don't.

#### *x*
Type: *Integer*
> The x coordinate you want the tooltip to be placed.

> If you pass either an `x/y` coordinate, the tooltip will offset its position by that value from the cursor. If you pass both an `x/y` coordinate, the tooltip will no longer follow the cursor.

#### *y*
Type: *Integer*
> The y coordinate you want the tooltip to be placed.

> If you pass either an `x/y` coordinate, the tooltip will offset its position by that value from the cursor. If you pass both an `x/y` coordinate, the tooltip will no longer follow the cursor.

#### *WhichToolTip*
Type: *Integer*
> This parameter allows you to indicate which tooltip you want this call of the function to be. Must be a number between 1 & 20. If unspecified, the number is 1.

Example #1
```
tool.Cust("image", 2.0, 1) ; Produces a tooltip that says "Couldn't find image" that will follow the cursor for 2 seconds
```

Example #2
```
tool.Cust("hello",,, MouseGetPos(&x, &y) x + 15, y) ; Produces a tooltip that says "hello" next to the cursor when called and will stay there for 1 second
```

Example #3
```
tool.Cust("offset", 3000,, -30) ; Produces a tooltip that says "offset" 30 pixels to the left of the cursors position and will follow the cursor for 3 seconds
```

## <u>`Wait()`</u>
This function will check to see if any tooltips are active and will wait for them to disappear before continuing.
```
tool.Wait( [{timeout}] )
```
#### *timout*
Type: *Integer*
> This parameter allows you to pass in a time value (in seconds) that you want `WinWaitClose` to wait before timing out. This value can be omitted and does not need to be set.
***

## class coord {
This class contains 3 different coordinate mode definitions to make setting coordmodes a bit easier during coding.

```
coord.s() ; sets coordmode("pixel", "screen")
coord.w() ; sets coordmode("pixel", "window")
coord.c() ; sets coordmode("caret", "window")
```
***

## class block {
This class contains 2 different block input mode definitions to make setting blockinputs a bit easier during coding.
```
block.On() ; Blocks all user inputs
block.Off() ; Enables all user inputs
```
***

## class WinGet {
This class contains a bunch of useful `get` style functions thats sole purpose is to retrieve and/or set information.

## <u>`MouseMonitor()`</u>
This function will grab the monitor that the mouse is currently within and return it as well as coordinate information in the form of a function object.

### Return Value
Type: *Object*
> Returns a function object containing; the monitor number, the left most pixel value, the right most pixel value, the top most pixel value and the bottom most pixel value.

Example #1
```autoit
;used in my main monitor (2560x1440)
monitor := winget.MouseMonitor()
MsgBox(monitor.monitor) ;returns 1
MsgBox(monitor.left) ;returns 0
MsgBox(monitor.right) ;returns 2560
MsgBox(monitor.top) ;returns 0
MsgBox(monitor.bottom) ;returns 1440
```

## <u>`Title()`</u>
This function gets and returns the title for the current active window.

**This function will ignore AutoHotkey GUIs.*
```
winget.Title( [&title] )
```
#### *&title*
Type: *VarRef*
> Produces a variable `title` that gets populated with the active window.

## <u>`isFullscreen()`</u>
This function is designed to check what state the active window is in.
```
winget.isFullscreen( [{&title, window}] )
```
#### *&title*
Type: *VarRef*
> Produces a variable `title` that gets populated with the active window. Can be omitted.

#### *window*
Type: *String/Variable - WinTitle*
> Pass a window title into this variable if you wish to provide the function with the window instead of relying it to try and find it based off the active window. This paramater can be omitted.

### Return Value
Type: *Boolean*
> Returns a boolean determining whether the window is fullscreen or not.


## <u>`PremName()`</u>
This function will grab the title of Premiere if it exists and check to see if a save is necessary.
```
winget.PremName( [&premCheck, &titleCheck, &saveCheck] )
```
#### *&premCheck*
Type: *VarRef*
> This parameter is the title of premiere, we want to pass this value back to the script that called it.

#### *&titleCheck*
Type: *VarRef*
> This parameter is checking to see if the premiere window is available to save (if it's possible), we want to pass this value back to the script. If the title contains necessary values, it will contain a number, otherwise it will contain `0`.

#### *&saveCheck*
Type: *VarRef*
> This parameter is checking for a * in the title to say a save is necessary, we want to pass this value back to the script. If a save is necessary, it will contain a number, otherwise it will contain `0`.

## <u>`AEName()`</u>
This function will grab the title of After Effects if it exists and check to see if a save is necessary
```
winget.AEName( [&aeCheck, &aeSaveCheck] )
```
#### *&aeCheck*
Type: *VarRef*
> This parameter is the title of after effects, we want to pass this value back to the script.

#### *&aeSaveCheck*
> This parameter is checking for a * in the title to say a save is necessary, we want to pass this value back to the script. If a save is necessary, it will contain a number, otherwise it will contain `0`.

## <u>`ID()`</u>
A function to grab the ID of the active window.
```
winget.ID( [&id] )
```
#### *&id*
Type: *VarRef*
> This parameter is the processname of the active window, we want to pass this value back to the script.

## <u>`ExplorerPath()`</u>
A function to extract the directory path of an open explorer window.
```
winget.ExplorerPath( [{hwnd}] )
```
#### *hwnd*
Type: *Integer*
> This parameter is the hwnd number of the window you wish to focus. If no hwnd number is provided, the function will determine the hwnd of the active window instead.

## <u>`FolderSize()`</u>
A function to return the size of a path in `bytes`.
```
winget.ExplorerPath( [path] )
```
#### *path*
Type: *String*
> This parameter is the folder path you wish to find the size of.

### Return Value
Type: *Integer*
> The size of a folder path in `bytes`.
***

## class Pause {
This class contains a few functions that minipulate other ahk scripts, either by pausing them or suspending them.

## <u>`pause()`</u>
A function that toggles the pause state on any `.ahk` script.

## <u>`Suspend()`</u>
This function will suspend/unsuspend other scripts.

Original code for this function [found here](https://stackoverflow.com/questions/14492650/check-if-script-is-suspended-in-autohotkey).
```
ScriptSuspend( [ScriptName, SuspendOn] )
```
#### *ScriptName*
Type: *String*
> The name of the script you wish to suspend. eg. `My Scripts.ahk`.

#### *SuspendOn*
Type: *Boolean*
> A true/false value determining whether to suspend or unsuspend the requested script.
***

## class Move {
This script is a collection of functions to move various aspects of windows in one way or another. These functions are all contained within the class `Move {` and are called like; `move.func()`

## <u>`move.Window()`</u>
A function that will check to see if you're holding the left mouse button, then move any window around however you like.

If the activation hotkey is `Rbutton`, this function will minimise the current window.
```
moveWin( [key] )
```
#### *key*
Type: *String/Variable - Hotkey*
> This parameter is what key(s) you want the function to press to move a window around (etc. #Left/#Right)

## <u>`move.Tab()`</u>
This function allows you to move tabs within certain monitors in windows. I currently have this function set up to cycle between monitors 2 & 4.

By pressing `RButton` and then either `Xbutton1/2` will move the tab either way. This function will check for 2s if you have released the RButton, if you have, it will drop the tab and finish, if you haven't it will be up to the user to press the LButton when you're done moving the tab. This function has hardcoded checks for `XButton1` & `XButton2` and is activated by having the activation hotkey as just one of those two, but then right clicking on a tab and pressing one of those two.

As of firefox version 106, for this function to work it either requires you to follow [these instructions](https://www.askvg.com/tip-remove-tabs-search-arrow-button-from-firefox-title-bar/) to disable the tab search arrow, or it'll require you to make adjustments to the pixel values in this script.

The way my monitors are layed out in windows;

                            -------------
                            |    2      |
                            |           |
        -----               -------------
        |   | ------------- -------------
        | 3 | |    1      | |    4      |
        |   | |           | |           |
        |   | ------------- -------------
        -----

If you use a different monitor layout, this function may require heavy adjustment to work correctly.

## <u>`move.XorY()`</u>
A quick and dirty way to limit the axis your mouse can move.

This function has specific code for `XButton1/2` and must be activated with 2 hotkeys.
***

## class Dark {
This script is a collection of scripts used to turn ahk GUI elements into `dark mode`

## <u>`button()`</u>
This function will convert GUI buttons to a dark/light theme.

Original code found [here](https://www.autohotkey.com/boards/viewtopic.php?f=13&t=94661).
```
buttonDarkMode( [ctrl_hwnd, {DarkorLight}] )
```
#### *ctrl_hwnd*
Type: *String/Variable*
> This parameter is the hwnd value of the button you wish to alter.

#### *DarkorLight*
Type: *String*
> This parameter is a toggle that allows you to call the inverse of this function and return the button to light mode. This parameter can be omitted for dark mode, otherwise pass "Light".

## <u>`menuDarkMode()`</u>
This function will convert GUI menus to dark mode/light mode.

Original code found [here](https://www.autohotkey.com/boards/viewtopic.php?f=13&t=94661).
```
menuDarkMode( [{DarkorLight}] )
```
#### *DarkorLight*
Type: *Boolean*
> This parameter is a toggle that allows you to call the inverse of this function and return the menu to light mode. This parameter can be omitted for dark mode, otherwise pass "0".

## <u>`titleBar()`</u>
This function will convert a windows title bar to a dark/light theme if possible.

Original code found [here](https://www.autohotkey.com/boards/viewtopic.php?f=13&t=94661).
```
titleBar( [hwnd, {dark}] )
```
#### *hwnd*
Type: *String/Variable*
> This parameter is the hwnd value of the window you wish to alter.

#### *dark*
Type: *Boolean*
> This parameter is a toggle that allows you to call the inverse of this function and return the title bar to light mode. This parameter can be omitted for dark mode, otherwise pass false for light mode.
***

## class Startup {
This script is a collection of functions mostly used in `My Scripts.ahk` to perform a variety of actions on script startup.

Information on these functions can be found [here](https://github.com/Tomshiii/ahk/wiki/Startup-Functions)