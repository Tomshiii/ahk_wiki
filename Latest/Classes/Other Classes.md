Within the `..\lib\Classes\` directory is a whole bunch of individual class files that give the user access to useful functions of various nature. All (or in case I ever change it, *most*) classes are called like: `class.func()`
***
### Table of Contents:
* [tool](#class-tool-)
* [coord](#class-coord-)
* [block](#class-block-)
* [WinGet](#class-WinGet-)
* [Dark](#class-Dark-)
* [Pause](#class-Pause-)
* [Move](#class-Move-)
* [Startup](#class-Startup-)
* [timer](#class-timer-)
* [obj](#class-obj-)
* [clip](#class-clip-)
***

# <u>class tool {</u>
This class contains two tooltip functions that help with tooltip creation and management.

## <u>`Cust()`</u>
This function allows the creation of a tooltip with any message, for a custom duration. This tooltip will then (under most conditions) follow the cursor and only redraw itself if the user has moved the cursor.

> *note: If the user passes either an `x OR y` value to this function (but not both), it will offset the tooltips position by that value from the cursor.

>If the user passes both an `x AND y` value to this function, the tooltip will no longer follow the cursor and instead be planted at those coordinates (the function uses the `Screen` coordinate position).*

>> *If you wish to replicate typical `ToolTip()` placement behaviour, follow Example #2 below.*
```
tool.Cust( [message, {timeout := 1.0, find := false, x?, y?, WhichToolTip?}] )
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

<u>Example #1</u>
```
tool.Cust("image", 2.0, 1) ; Produces a tooltip that says "Couldn't find image" that will follow the cursor for 2 seconds
```

<u>Example #2</u>
```
tool.Cust("hello",,, MouseGetPos(&x, &y) x + 15, y) ; Produces a tooltip that says "hello" next to the cursor when called and will stay there for 1 second
```

<u>Example #3</u>
```
tool.Cust("offset", 3000,, -30) ; Produces a tooltip that says "offset" 30 pixels to the left of the cursors position and will follow the cursor for 3 seconds
```
***

## <u>`Wait()`</u>
This function will check to see if any tooltips are active and will wait for them to disappear before continuing.
```
tool.Wait( [{timeout}] )
```
#### *timout*
Type: *Integer*
> This parameter allows you to pass in a time value (in seconds) that you want `WinWaitClose` to wait before timing out. This value can be omitted and does not need to be set.
***

# <u>class coord {</u>
This class contains 4 different coordinate mode definitions that, *by default* set coordmodes to some defaults that I use all throughout my scripts.

These functions can then have parameters passed to them to make them behave more similarly to the base function incase you need it.
```
coord.s()      ; sets coordmode("pixel", "screen")
coord.w()      ; sets coordmode("pixel", "window")
coord.client() ; sets coordmode("pixel", "client")
coord.c()      ; sets coordmode("caret", "window")
```
***

# <u>class block {</u>
This class contains 2 different block input mode definitions to make setting blockinputs a bit easier during coding.

While the main purpose of these functions is to quickly and easily achieve what I normally want as default, they also support passing parameters to achieve all normal `BlockInput` functionality.
```
block.On()  ; Blocks all user inputs. By default does `BlockInput("SendAndMouse") & BlockInput("MouseMove")`
block.Off() ; Enables all user inputs. By default does `BlockInput("Default") & BlockInput("MouseMoveOff")`
```
***

# <u>class WinGet {</u>
This class contains a bunch of useful `get` style functions thats sole purpose is to retrieve and/or set information.

## <u>`MouseMonitor()`</u>
This function will grab the monitor that the mouse is currently within and return it as well as coordinate information in the form of a function object.

### Return Value
Type: *Object*
> Returns a function object containing; the monitor number, the left most pixel value, the right most pixel value, the top most pixel value and the bottom most pixel value.

<u>Example #1</u>
```autoit
;used in my main monitor (2560x1440)
monitor := winget.MouseMonitor()
MsgBox(monitor.monitor) ;returns 1
MsgBox(monitor.left)    ;returns 0
MsgBox(monitor.right)   ;returns 2560
MsgBox(monitor.top)     ;returns 0
MsgBox(monitor.bottom)  ;returns 1440
```
***

## <u>`Title()`</u>
This function gets and returns the title for the current active window.

**This function will ignore AutoHotkey GUIs.*
```
winget.Title( [&title] )
```
#### *&title*
Type: *VarRef*
> Produces a variable `title` that gets populated with the active window.
***

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
***

## <u>`PremName()`</u>
This function will grab the title of Premiere if it exists and check to see if a save is necessary.
```
winget.PremName( [{&premCheck, &titleCheck, &saveCheck}] )
```
#### *&premCheck*
Type: *VarRef*
> This parameter is the complete title of premiere.

#### *&titleCheck*
Type: *VarRef*
> This parameter is checking to see if the premiere window is available to save based off what's found in the current title. Will return unset if premiere cannot be found or a boolean false if unavailable to save. Otherwise it will contain a number greater than 0

#### *&saveCheck*
Type: *VarRef*
> This parameter is checking for a * in the title to see if a save is necessary.  Will return unset if premiere cannot be found or a boolean false if save is not required. Otherwise it will return boolean true

### Return Value
Type: *Object*
> Returns an object containing similar information to the VarRefs above.
```autoit
prem := winget.PremName()
prem.winTitle        ;// is the current title of the open premiere window
prem.titleCheck      ;// a boolean value of if the window is available to save
prem.saveCheck       ;// a boolean value of if a save is currently necessary
```
***

## <u>`AEName()`</u>
This function will grab the title of After Effects if it exists and check to see if a save is necessary
```
winget.AEName( [{&aeCheck, &titleCheck, &saveCheck}] )
```
#### *&aeCheck*
Type: *VarRef*
> This parameter is the complete title of after effects.

#### *&titleCheck*
Type: *VarRef*
> This parameter is checking to see if the after effects window is available to save based off what's found in the current title. Will return unset if after effects cannot be found or a boolean false if unavailable to save. Otherwise it will contain a number greater than 0

#### *&saveCheck*
> This parameter is checking for a * in the title to see if a save is necessary.  Will return unset if after effects cannot be found or a boolean false if save is not required. Otherwise it will return boolean true

### Return Value
Type: *Object*
> Returns an object containing similar information to the VarRefs above.
```autoit
ae := winget.AEName()
ae.winTitle        ;// is the current title of the open after effects window
ae.titleCheck      ;// a boolean value of if the window is available to save
ae.saveCheck       ;// a boolean value of if a save is currently necessary
```
***

## <u>`ProjClient()`</u>
This function is designed to retrieve the name of the client using some string manipulation of the dir path within Premiere's/After Effect's title. It uses `ptf.comms` as the "root" dir and expects the next folder in the path to be the client name.
```
winget.ProjClient()
```
### Return Value
Type: *String*
> Returns a string of the clients name.
***

## <u>`ID()`</u>
A function to grab the ID of the active window.
```
winget.ID( [&id] )
```
#### *&id*
Type: *VarRef*
> This parameter is the processname of the active window, we want to pass this value back to the script.
***

## <u>`ExplorerPath()`</u>
A function to extract the directory path of an open explorer window.
```
winget.ExplorerPath( [{hwnd}] )
```
#### *hwnd*
Type: *Integer*
> This parameter is the hwnd number of the window you wish to focus. If no hwnd number is provided, the function will determine the hwnd of the active window instead.
***

## <u>`FolderSize()`</u>
A function to return the size of a path in `bytes` by default.
```
winget.ExplorerPath( [path {, option}] )
```
#### *path*
Type: *String*
> This parameter is the folder path you wish to find the size of.

#### *option*
Type: *Integer*
> This parameter is to optionally have the value returned in `MB`, `GB` or `TB`.

### Return Value
Type: *Integer*
> The size of a folder path in `bytes` *by default* or in the selected format.
***

# <u>class Dark {</u>
This class contains a few functions that makes turning GUI elements to/from `dark mode` easier.

## <u>`button()`</u>
This function will convert GUI buttons to a dark/light theme.
```
dark.button( [ctrl_hwnd {, DarkorLight := "Dark"}] )
```

#### *ctrl_hwnd*
Type: *Integer*
> This parameter is the hwnd value of the control you wish to alter.

#### *DarkorLight*
Type: *String*
> This parameter is a toggle that allows you to switch between light/dark modes.
>
>> This parameter can be omitted and defaults to `"Dark"`. If you wish to change the control to lightmode, pass `"Light"`
***

## <u>`menu()`</u>
This function will convert GUI menus to dark/light mode.  
*note: due to limitations with ahk, this function will only alter the drop down menus, not the menu bar colour itself*
```
dark.menu( [{DarkorLight := 1}] )
```
#### *DarkorLight*
Type: *Boolean*
> This parameter is to set whether you want the function to change the menu to dark/light mode. This parameter defaults to 1 (for `true` or `dark`), if you wish to change the menu to light mode, pass `0`
***

## <u>`titleBar()`</u>
his function will convert a GUI windows title bar to a dark/light theme if possible.
```
dark.titleBar( [hwnd {, dark := true}] )
```
#### *hwnd*
Type: *Integer*
> This parameter is the hwnd value of the window you wish to alter.

#### *dark*
Type: *Boolean*
> This parameter determines whether you want the function to turn the desired windows titlebar to light or darkmode.
>
> This parameter defaults to `true` for `dark`, if you wish to change the titlebar to light mode, pass `false` or `0`
***
# <u>class Pause {</u>
This class contains a few functions that minipulate other ahk scripts, either by pausing them or suspending them.

## <u>`pause()`</u>
A function that toggles the pause state on any `.ahk` script.
***

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

# <u>class Move {</u>
This script is a collection of functions to move various aspects of windows in one way or another. These functions are all contained within the class `Move {` and are called like; `move.func()`

## <u>`Window()`</u>
A function that will check to see if you're holding the left mouse button, then move any window around however you like.

If the activation hotkey is `Rbutton`, this function will minimise the current window.
```
move.Window( [key] )
```
#### *key*
Type: *String*
> This parameter is what key(s) you want the function to press to move a window around (etc. #Left/#Right)
***

## <u>`Tab()`</u>
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
***

## <u>`XorY()`</u>
A quick and dirty way to limit the axis your mouse can move.

This function has specific code for `XButton1/2` and must be activated with 2 hotkeys.
***

# <u>`class Startup {`</u>
This class is a collection of functions mostly used in `My Scripts.ahk` to perform a variety of actions on script startup.

Information on these functions can be found [here](https://github.com/Tomshiii/ahk/wiki/Startup-Functions).
***

# <u>`class timer {`</u>
This class allows a timer to be easily generated and expanded on through the use of extending classes.
***

# <u>`class obj {`</u>
This class is a collection of wrapper functions designed to take normal AutoHotkey functions and return their VarRefs as object parameters instead.

Information on these functions can be found [here](https://github.com/Tomshiii/ahk/wiki/Obj-Functions).
***

# <u>`class clip {`</u>
This class encapsulates often used functions to manipulate the clipboard.

## <u>`clear()`</u>
Ths function stores the current clipboard and then clears it.
```
clip.clear( [{&storedClip}] )
```

#### *storedClip*
Type: *VarRef*
> This parameter is the variable you wish to store the clipboard in.

### Return Value
Type: *Object*
> Returns an object containing the stored clipboard.

<u>Example #1</u>
```
clipb := clip.clear(&stored)      ;// clear the clipboard
A_Clipboard := clip.storedClip    ;// return the stored clipboard
A_Clipboard := stored             ;// return the stored clipboard
```
***

## <u>`copyWait()`</u>
This function attempts to copy any highlighted text then waits for the clipboard to contain data.

If the function times out, it will return a boolean false.
```
clip.copyWait( [{storedClip, waitSec := 0.1}] )
```
#### *storedClip*
Type: *Variable*
> This parameter is the variable you're storing the clipboard in. If the clipwait times out, this function will attempt to return the clipboard to this variable if it has been set.

#### *waitSec*
Type: *Integer*
> This parameter is the time in `seconds` you want the clipwait to wait. This parameter defaults to `0.1s`

### Return Value
Type: *Object*
> Returns a boolean `True/False` depending on if the clipboard recieved any data.
***

## <u>`wait()`</u>
This function will wait for the clipboard to contain data.

If this function times out, it will attempt to return the clipboard to the passed variable.
```
clip.wait( [{storedClip, waitSec := 0.1}] )
```
#### *storedClip*
Type: *Variable*
> This parameter is the variable you're storing the clipboard in. If the clipwait times out, this function will attempt to return the clipboard to this variable if it has been set.

#### *waitSec*
Type: *Integer*
> This parameter is the time in `seconds` you want the clipwait to wait. This parameter defaults to `0.1s`

### Return Value
Type: *Object*
> Returns a boolean `True/False` depending on if the clipboard recieved any data.
***

## <u>`delayReturn()`</u>
This function returns the clipboard to the passed variable on a delay.
```
clip.delayReturn( [returnClip {, delay := 1000}] )
```
#### *returnClip*
Type: *Variable*
> This parameter is the variable you're storing the clipboard in.

#### *delay*
Type: *Integer*
> This parameter is the delay in `ms` you want the function to wait before returning the clipboard to the passed variable.
***

## <u>`returnClip()`</u>
This function returns the clipboard to the passed variable or object.
```
clip.returnClip( returnClip )
```
#### *returnClip*
Type: *Variable/Object*
> This parameter is the variable/Object you're storing the clipboard in.
>> If this parameter is an object it MUST have a parameter `clipObj.storedClip`