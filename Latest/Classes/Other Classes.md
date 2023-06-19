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
* [cmd](#class-cmd-)
* [keys](#class-keys-)
* [Mip](#class-Mip-)
* [WM](#class-WM-)
* [trim](#class-trim-)
* [ytdlp](#class-ytdlp-)
* [ffmpeg](#class-ffmpeg-)
* [reset](#class-reset-)
***

# <u>`class tool {`</u>
This class contains two tooltip functions that help with tooltip creation and management.

## <u>`tool.Cust()`</u>
This function allows the creation of a tooltip with any message, for a custom duration. This tooltip will then (under most conditions) follow the cursor and only redraw itself if the user has moved the cursor.

> If the user passes either an `x` OR `y` value to this function (but not both), it will offset the tooltips position by that value from the cursor.

> If the user passes both an `x AND y` value to this function, the tooltip will no longer follow the cursor and instead be planted at those coordinates (the function uses the `Screen` coordinate position).
>> *If you wish to replicate typical `ToolTip()` placement behaviour, follow Example #2 below.*

If a second tooltip of the same `WhichToolTip` param is called, the first will be replaced with it.

```c#
tool.Cust( [message, {timeout := 1.0, find := false, x?, y?, WhichToolTip?}] )
```
#### *message*
Type: *String*
> This parameter is whatever you wish the tooltip to display.

#### *timeout*
Type: *Integer/Float*
> This parameter is how many `ms` you want the tooltip to last. This value can be omitted and it will default to `1000`.
>    - If you wish to type in seconds, use a floating point number, ie; `1.0`, `2.5`, etc.

> If 0 is passed, the tooltip that was called with the same `WhichToolTip` parameter will be stopped.

#### *x/y*
Type: *Integer*
> The coordinates you want the tooltip to be placed.

> If you pass either an `x` or `y` coordinate, the tooltip will constantly offset its position by that value from the cursor. If you pass both an `x and y` coordinate, the tooltip will no longer follow the cursor.

#### *WhichToolTip*
Type: *Integer*
> This parameter allows you to indicate which tooltip you want this call of the function to be. Must be a number between 1 & 20. If unspecified, the number is 1.

<u>Example #1</u>
```ahk
tool.Cust("hello",, MouseGetPos(&x, &y) x + 15, y) ; Produces a tooltip that says "hello" next to the cursor when called and will stay at those coordinates for 1 second
```

<u>Example #2</u>
```ahk
tool.Cust("offset", 3000, -30) ; Produces a tooltip that says "offset" 30 pixels to the left of the cursors position and will follow the cursor for 3 seconds
```
***

## <u>`tool.Wait()`</u>
This function will check to see if any tooltips are active and will wait for them to disappear before continuing.
```c#
tool.Wait( [{timeout}] )
```
#### *timeout*
Type: *Integer*
> This parameter allows you to pass in a time value (in seconds) that you want `WinWaitClose` to wait before timing out. This value can be omitted and does not need to be set.
***

## <u>`tool.Tray()`</u>
This function will check to see if any tooltips are active and will wait for them to disappear before continuing.
```c#
tool.Tray( [TrayParams := {text: "", title: "", options: ""}, timeout := 5000] )
```
#### *TrayParams*
Type: *Object*
> This parameter is an object containing the paramaters you wish to pass to `TrayTip`. This includes `{text: "", title: "", options: ""}`.

#### *TrayParams*
Type: *Object*
> This parameter is the time in `ms` you wish to wait before the traytip times out. Pass `0` to disable this function attempting a timeout.
    > *note: This timeout may not work as intended due to windows/if your script is persistent*
***

# <u>`class coord {`</u>
This class contains 4 different coordinate mode definitions that, *by default* set coordmodes to some defaults that I use all throughout my scripts.

These functions can then have parameters passed to them to make them behave more similarly to the base function incase you need it.
```ahk
coord.s()      ; sets coordmode("pixel", "screen")
coord.w()      ; sets coordmode("pixel", "window")
coord.client() ; sets coordmode("pixel", "client")
coord.c()      ; sets coordmode("caret", "window")
```

## <u>`coord.store()`</u>
A function to store all current coordmode settings into an object.
***

# <u>`class block {`</u>
This class contains 2 different block input mode definitions to make setting blockinputs a bit easier during coding.

While the main purpose of these functions is to quickly and easily achieve what I normally want as default, they also support passing parameters to achieve all normal `BlockInput` functionality.
```ahk
block.On()  ; Blocks all user inputs. By default does `BlockInput("SendAndMouse") & BlockInput("MouseMove")`
block.Off() ; Enables all user inputs. By default does `BlockInput("Default") & BlockInput("MouseMoveOff")`
```
***

# <u>`class WinGet {`</u>
This class contains a bunch of useful `get` style functions thats sole purpose is to retrieve and/or set information.

## <u>`WinGet.WinMonitor()`</u>
This function will grab the monitor that the active window is currently within and return it as well as coordinate information in the form of a function object.

*If a window is overlapping multiple monitors, this function may attempt to fullscreen the window first to get the correct monitor.*
```c#
winget.WinMonitor( {title?} )
```
#### *title*
Type: *String*
> This parameter allows the user to pass a custom winTitle into the function instead of using the currently active window

### Return Value
Type: *Object*
> Returns a function object containing; the monitor number, the left most pixel value, the right most pixel value, the top most pixel value and the bottom most pixel value.

<u>Example #1</u>
```autoit
window := winget.WinMonitor()
window.monitor      ;// returns monitor the window is within
window.left         ;// returns left x position
window.right        ;// returns right x position
window.top          ;// returns top y position
window.bottom       ;// returns bottom y position
```

***
## <u>`WinGet.MouseMonitor()`</u>
This function will grab the monitor that the mouse is currently within and return it as well as coordinate information in the form of a function object.
```c#
winget.MouseMonitor( [{x?, y?}] )
```
#### *x & y*
Type: *Integer*
> These parameters allow the user to pass custom coordinates into the function to retrieve the monitor information relating to those coordinates.
>
>> Both `x` & `y` need to be passed to this function or it will default to the current mouse coordinates

### Return Value
Type: *Object*
> Returns a function object containing; the monitor number, the left most pixel value, the right most pixel value, the top most pixel value and the bottom most pixel value.

<u>Example #1</u>
```autoit
;mouse is within monitor 1 (2560x1440)
monitor := winget.MouseMonitor()
monitor.monitor      ;// returns 1
monitor.left         ;// returns 0
monitor.right        ;// returns 2560
monitor.top          ;// returns 0
monitor.bottom       ;// returns 1440
```
***

## <u>`WinGet.Title()`</u>
This function gets and returns the title for the current active window.

**This function will ignore AutoHotkey GUIs.*
```c#
winget.Title( [&title] )
```
#### *&title*
Type: *VarRef*
> Produces a variable `title` that gets populated with the active window.

### Return Value
Type: *String*
> Returns the title as a string.
***

## <u>`WinGet.isFullscreen()`</u>
This function is designed to check what state the active window is in.
```c#
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
> Returns a boolean determining whether the window is fullscreen or not. A return value of 1 means it is maximised.
***

## <u>`WinGet.PremName()`</u>
This function will grab the title of Premiere if it exists and check to see if a save is necessary.
```c#
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
Type: *Object/Boolean*
> Returns an object containing similar information to the VarRefs above.
```autoit
;// if Premiere isn't open `winget.Premiere()` will return 0/false
prem := winget.PremName()
prem.winTitle        ;// is the current title of the open premiere window
prem.titleCheck      ;// a boolean value of if the window is available to save
prem.saveCheck       ;// a boolean value of if a save is currently necessary
```
***

## <u>`WinGet.AEName()`</u>
This function will grab the title of After Effects if it exists and check to see if a save is necessary
```c#
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
Type: *Object/Boolean*
> Returns an object containing similar information to the VarRefs above.
```autoit
;// if AE isn't open `winget.AE()` will return 0/false
ae := winget.AEName()
ae.winTitle        ;// is the current title of the open after effects window
ae.titleCheck      ;// a boolean value of if the window is available to save
ae.saveCheck       ;// a boolean value of if a save is currently necessary
```
***

## <u>`WinGet.ProjClient()`</u>
This function is designed to retrieve the name of the client using some string manipulation of the dir path within Premiere's/After Effect's title. It uses `ptf.comms` as the "root" dir and expects the next folder in the path to be the client name.
```c#
winget.ProjClient()
```
### Return Value
Type: *String*
> Returns a string of the clients name.

<u>Example #1</u>
```ahk
;// ptf.comms = "E:\comms"
;// Current project open: `E:\comms\d0yle\polar bowler\polar bowler.prproj`
client := winget.ProjClient()   ;// returns "d0yle"
```
***

## <u>`WinGet.ID()`</u>
A function to grab the ID of the active window.
```c#
winget.ID( [&id] )
```
#### *&id*
Type: *VarRef*
> This parameter is the processname of the active window, we want to pass this value back to the script.

### Return Value
Type: *Boolean*
> Returns true/false on completion depending on if successful.
***

## <u>`WinGet.ExplorerPath()`</u>
A function to extract the directory path of an open explorer window.
```c#
winget.ExplorerPath( [{hwnd}] )
```
#### *hwnd*
Type: *Integer*
> This parameter is the hwnd number of the window you wish to focus. If no hwnd number is provided, the function will determine the hwnd of the active window instead.
***

## <u>`WinGet.FolderSize()`</u>
A function to return the size of a path in `bytes` by default.
```c#
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

## <u>`WinGet.ProjPath()`</u>
A function to recover the path within the title of either `Premiere Pro` or `After Effects`.
```c#
winget.ProjPath()
```
### Return Value
Type: *Object*
```
projPath := obj.SplitPath("E:\comms\tomshi\video\project.prproj")
projPath.Path       ; E:\comms\tomshi\video\project.prproj
projPath.Name       ; project.prproj
projPath.Dir        ; E:\comms\tomshi\video
projPath.Ext        ; proj
projPath.NameNoExt  ; project
projPath.Drive      ; E:
```
***

# <u>`class Dark {`</u>
This class contains a few functions that makes turning GUI elements to/from `dark mode` easier.

## <u>`Dark.button()`</u>
This function will convert GUI buttons to a dark/light theme.
```c#
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

## <u>`Dark.allButtons()`</u>
This function will convert all buttons defined in the GUI to a dark/light theme.
```c#
dark.allButtons( [guiObj {, DarkorLight := "Dark", changeBG := false}] )
```

#### *guiObj*
Type: *Object*
> This parameter is the gui object you're working on (ie. MyGui, settingsGUI, etc).

#### *DarkorLight*
Type: *String*
> This parameter is a toggle that allows you to switch between light/dark modes.
>
>> This parameter can be omitted and defaults to `"Dark"`. If you wish to change the control to lightmode, pass `"Light"`

#### *changeBG*
Type: *Boolean/Object*
> This parameter gives the ability to modify button bg colours & gui bg colours. Defaults to false and will not adjust either. See Example #1 for more info

<u>Example #1</u>
```ahk
allButtons(guiObj, "DarkorLight", {default: true, LightColour/DarkCoulour: "xxxxxx", LightBG/DarkBG: "xxxxxx"/false})
default: true                    ;// sets 0xF0F0F0 for light mode && 0xd4d4d4 for darkmode. No other parameters are necessary if this is passed
LightColour/DarkColour: "xxxxxx" ;// This value is a hex code (WITHOUT 0x) - sets the bg colour for all buttons for the given colour mode
LightBG/DarkBG: "xxxxxx"         ;// This value is a hex code (WITHOUT 0x) - sets the gui bg colour when in the desired colour mode. If this value is not set, it will default to `LightColour/DarkColour`.
DarkBG/LightBG: false            ;// can be set if you do not wish to adjust the BG colour of a certain colour mode
```
***

## <u>`Dark.menu()`</u>
This function will convert GUI menus to dark/light mode.  
*note: due to limitations with ahk, this function will only alter the drop down menus, not the menu bar colour itself*
```c#
dark.menu( [{DarkorLight := 1}] )
```
#### *DarkorLight*
Type: *Boolean*
> This parameter is to set whether you want the function to change the menu to dark/light mode. This parameter defaults to 1 (for `true` or `dark`), if you wish to change the menu to light mode, pass `0`
***

## <u>`Dark.titleBar()`</u>
his function will convert a GUI windows title bar to a dark/light theme if possible.
```c#
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
# <u>`class Pause {`</u>
This class contains a few functions that minipulate other ahk scripts, either by pausing them or suspending them.

## <u>`Pause.pause()`</u>
A function that toggles the pause state on any `.ahk` script.
***

## <u>`Pause.Suspend()`</u>
This function will suspend/unsuspend other scripts.

Original code for this function [found here](https://stackoverflow.com/questions/14492650/check-if-script-is-suspended-in-autohotkey).
```c#
ScriptSuspend( [ScriptName, SuspendOn] )
```
#### *ScriptName*
Type: *String*
> The name of the script you wish to suspend. eg. `My Scripts.ahk`.

#### *SuspendOn*
Type: *Boolean*
> A true/false value determining whether to suspend or unsuspend the requested script.
***

# <u>`class Move {`</u>
This script is a collection of functions to move various aspects of windows in one way or another. These functions are all contained within the class `Move {` and are called like; `move.func()`

## <u>`Move.Window()`</u>
A function that will check to see if you're holding the left mouse button, then move any window around however you like.

If the activation hotkey is `Rbutton`, this function will minimise the current window.
```c#
move.Window( [key] )
```
#### *key*
Type: *String*
> This parameter is what key(s) you want the function to press to move a window around (etc. #Left/#Right)
***

## <u>`Move.Tab()`</u>
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

## <u>`Move.XorY()`</u>
A quick and dirty way to limit the axis your mouse can move.

This function has specific code for `XButton1/2` and must be activated with 2 hotkeys.
***

## <u>`Move.Adjust()`</u>
This function allows the minorly adjust the width/height & x/y values of the active window.

This function requires the second activation hotkey to be:
- <kbd>-</kbd>/<kbd>=</kbd>
- for `x axis`
    - <kbd>Left</kbd>/<kbd>Right</kbd>
- for `y axis`
    - <kbd>Up</kbd>/<kbd>Down</kbd>
```c#
move.Adjust( [{xORy := "x", window := "A"}] )
```
#### *xORy*
Type: *String*
> This parameter is determining which axis you wish to adjust.

#### *window*
Type: *String*
> This parameter is the title of the window you wish to adjust. By default it will use the active window.
***

## <u>`Move.winCenter()`</u>
This function will on first activation, center the active window in the middle of the active monitor. If activated again it will move the window to the center of the main monitor instead.
> This function has specific code for vlc & youtube windows

> The math for this function can act a bit funky with vertical monitors. Especially with programs like discord that have a minimum width
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

## <u>`clip.clear()`</u>
Ths function stores the current clipboard and then clears it.
```c#
clip.clear( [{&storedClip}] )
```

#### *storedClip*
Type: *VarRef*
> This parameter is the variable you wish to store the clipboard in.

### Return Value
Type: *Object*
> Returns an object containing the stored clipboard.

<u>Example #1</u>
```ahk
clipb := clip.clear(&stored)      ;// clear the clipboard
A_Clipboard := clip.storedClip    ;// return the stored clipboard
A_Clipboard := stored             ;// return the stored clipboard
```
***

## <u>`clip.copyWait()`</u>
This function attempts to copy any highlighted text then waits for the clipboard to contain data.

If the function times out, it will return a boolean false.
```c#
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

## <u>`clip.wait()`</u>
This function will wait for the clipboard to contain data.

If this function times out, it will attempt to return the clipboard to the passed variable.
```c#
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

## <u>`clip.delayReturn()`</u>
This function returns the clipboard to the passed variable on a delay.
```c#
clip.delayReturn( [returnClip {, delay := 1000}] )
```
#### *returnClip*
Type: *Variable*
> This parameter is the variable you're storing the clipboard in.

#### *delay*
Type: *Integer*
> This parameter is the delay in `ms` you want the function to wait before returning the clipboard to the passed variable.
***

## <u>`clip.returnClip()`</u>
This function returns the clipboard to the passed variable or object.
```c#
clip.returnClip( [returnClip] )
```
#### *returnClip*
Type: *Variable/Object*
> This parameter is the variable/Object you're storing the clipboard in.
>> If this parameter is an object it MUST have a parameter `clipObj.storedClip`
***

## <u>`clip.search()`</u>
This function runs a search of highlighted text.
```c#
clip.search( [{url := "https://www.google.com/search?d&q="}] )
```
#### *url*
Type: *String*
> This parameter is the url (search engine) you wish to use. Provide everything before the part of the url that is your search quiry.
***

## <u>`clip.capitilise()`</u>
This function will attempt to determine whether to capitilise or completely lowercase the highlighted text depending on which is more frequent.
***

# <u>`class cmd {`</u>
This class encapsulates often used cmd functions.

## <u>`cmd.run()`</u>
Ths function stores the current clipboard and then clears it.
```c#
cmd.run( [{admin := false, wait := true, runParams*}] )
```
#### *admin*
Type: *Boolean*
> This parameter determine whether you want the commandline to be run elevated or not. This value defaults to false.

#### *wait*
Type: *Boolean*
> This parameter determine whether you want the function to use `Run` or `RunWait`. This function will default to `RunWait`.

#### *runParams*
Type: *Variadic - String*
> This parameter allows the user to pass the remaining `Run` parameters.
>
> In order they are; the command you wish to pass to the command line, the wording directory you wish for the command line to start from & any options you wish for `Run` to use.

### Return Value
Type: *Integer/Object*
> If `wait` is passed as true, this function will return an object containing the exit code & the window PID. Otherwise just the PID will be returned as an integer.
***

## <u>`cmd.result()`</u>
This function attempts to send commands to the command results and return the results.  
This function is originally from the [documentation](https://lexikos.github.io/v2/docs/commands/Run.htm#Examples)
```c#
cmd.result( [command] )
```
#### *command*
Type: *String*
> This parameter is the command you wish to send to the command line.

### Return Value
Type: *String*
> The function will attempt to return the command line response as a string. This may not work in all cases.
***

## <u>`cmd.mapDrive()`</u>
This function will unmap the desired mapped drive location, then remap your desired drive letter to the desired ip address.
```c#
cmd.mapDrive( [driveLocation, networkLocation] )
```
#### *driveLocation*
Type: *String*
> This paramater is the drive letter you wish to remap. Do **not** include `:`

#### *networkLocation*
Type: *String*
> This paramater is the ip location of your network drive.
***

## <u>`cmd.mapDrive()`</u>
This function will unmap the desired mapped drive location, then remap your desired drive letter to the desired ip address.
```c#
cmd.inUseDrives()
```
### Return Value
Type: *Map*
> Returns a map containing which drive letters are already mapped & what their mapped locations are.
***

# <u>`class keys {`</u>
This class encapsulates often used functions relating to keys.

## <u>`keys.allUp()`</u>
This function loops through as many possible SC and vk keys and sends the {Up} keystroke for each respective one in an attempt to unstick as many keys as possible.
***

## <u>`keys.allWait()`</u>
This function is designed to remove the hassle that can sometimes occur by using `KeyWait`. If a function is launched via something like a streamdeck `A_ThisHotkey` will be blank, if you design a function to only be activated with one button but then another user tries to launch it from two an error will be thrown.  
This function will automatically determine what's required and stop errors occuring.
```c#
keys.allWait( [which := "both"] )
```
#### *which*
Type: *String*
> This parameter determines which hotkey should be waited for in the event that the user tries to activate with two hotkeys.

### Return Value
Type: *Object*
> If the user activates the hotkey/function with two hotkeys, this function will return the two hotkeys as an object the same way that [`getHotkeys()`](#getHotkeys) would.
***

## <u>`keys.check()`</u>
This function will check to see if the passed key is virtually stuck down.
```c#
keys.check(key)
```
#### *key*
Type: *String*
> This parameter is the key you wish to check.
***

## <u>`keys.allCheck()`</u>
This function loops through as many possible SC and vk keys and checks whether they are stuck down. If they are, an {UP} keystroke will be sent.  
This function is a variation of `allUp()`
```c#
keys.allCheck( [sendUp] )
```
#### *sendUp*
Type: *Boolean*
> If this variable is set to true it will send an UP keystroke to all keys.
> If it is set to false the function will instead return an array containing the KeyName of all keys that are potentially stuck down.

### Return Value
Type: *Array*
> If sendUp is set to `false` the function will instead return an array containing the names of all keys that are potentially stuck down.
***

# <u>`class Mip {`</u>
This class creates a map with CaseSense automatically set to false.
***
# <u>`class WM {`</u>
This is a collection of WM scripts found scattered through the web/ahk docs.

## <u>`WM.On_WM_MOUSEMOVE()`</u>
This is a function designed to allow tooltips to appear while hovering over certain GUI elements.
> Original code can be found on the ahk website : https://lexikos.github.io/v2/docs/objects/Gui.htm#ExToolTip
```c#
WM.On_WM_MOUSEMOVE( [{wParam, lParam, msg, Hwnd}] )
```

<u>Example #1</u>
```ahk
GuiCtrl.ToolTip := "desired tooltip"
move := WM()
mv := ObjBindMethod(move, "On_WM_MOUSEMOVE")
OnMessage(0x0200, mv)
```

<u>Example #2</u>
```ahk
GuiCtrl.ToolTip := "desired tooltip"
;// a one line version
OnMessage(0x0200, ObjBindMethod(WM(), "On_WM_MOUSEMOVE"))
```
***

## <u>`WM.Send_WM_COPYDATA()`</u>
This function sends the specified string to the specified window and returns the reply.
```c#
WM.Send_WM_COPYDATA( [str, scriptTitle {, timeout := 4000}] )
```
#### *str*
Type: *String*
> This parameter is the string you wish to send.

#### *scriptTitle*
Type: *String*
> This parameter is the title of the script you wish to target.
>> The passed string must be the entire filename (including the `.ahk` extension), eg. `My Scripts.ahk`.

#### *timeout*
Type: *Integer*
> This parameter is the time in `ms` you want the function to wait before timing out.

### Return Value
Type: *Integer*
> Returns the response from the target window. The reply is 1 if the target window processed the message, or 0 if it ignored it.
***

## <u>`WM.Receive_WM_COPYDATA()`</u>
This function recieves a custom string sent by `WM.Send_WM_COPYDATA()`.
```c#
WM.Send_WM_COPYDATA( [{wParam, lParam, msg, hwnd}] )
```

<u>Example #1</u>
```ahk
OnMessage(0x004A, test)  ; 0x004A is WM_COPYDATA
test(wParam, lParam, msg, hwnd) {
    res := WM.Receive_WM_COPYDATA(wParam, lParam, msg, hwnd)
    MsgBox("smelly" res)
}
```
***

# <u>`class ytdlp {`</u>
A class to contain any `ytdlp` wrapper functions to allow for cleaner, more expandable code that allows the user to access common `ytdlp` commands.

## <u>`download()`</u>
This function allows the user to quickly download a video from `twitch`/`youtube` (including clips from both) & requires [yt-dlp](https://github.com/yt-dlp/yt-dlp) to be installed correctly on the users system.
```c#
ytdlp().download( [{args, folder := A_ScriptDir}] )
```
#### *args*
Type: *String*
> This parameter is any arguments you wish to pass to yt-dlp. Arguments can be found [here](https://github.com/yt-dlp/yt-dlp#usage-and-options).

#### *folder*
Type: *String*
> This parameter is the folder you wish the files to save. By default it's this scripts directory.

### Return Value
Type: *String*
> Returns the url that the function worked on.

<u>Example #1</u>
```autoit
ytdlp().download("", "download\path")
;// default command with no passed args;
;// yt-dlp -P "link\to\path" "URL"
```
***

## <u>`reencode()`</u>
A function to handle converting a file to `h264`. This is useful when using video editing programs such as `Premiere Pro` as it doesn't support the filetypes that youtube stores newer videos in (`.webm` & `vp9`/`av1`).
```c#
ytdlp().reencode( [filepath {, title?}] )
```
#### *filepath*
Type: *String*
> This parameter is the filepath of the file you wish to reencode.

#### *title*
Type: *String*
> This parameter is the desired output filename. This parameter can be omitted but the user may encounter issues if the resulting file is the same name (including file extension) as the input file.
***

# <u>`class ffmpeg {`</u>
A class to contain often used functions to quickly and easily access common ffmpeg commands.

## <u>`merge_audio_video()`</u>
This function attempts to merge an audio file with a video file.
```c#
ffmpeg().merge_audio_video( [videoFilePath, audioFilePath] )
```
#### *videoFilePath*
Type: *String*
> This parameter is the filepath of the `video` file you wish to merge.

#### *audioFilePath*
Type: *String*
> This parameter is the filepath of the `audio` file you wish to merge.
***

## <u>`reencode_h26x()`</u>
This function attempts to reencode the desired file into a h264 codec.
```c#
ffmpeg().reencode_h26x( [videoFilePath {, outputFileName?, codec := "libx264", preset := "veryfast", crf := "17"}] )
```
#### *videoFilePath*
Type: *String*
> The filepath to the desired video file.

#### *outputFileName*
Type: *String*
> The desired output name of your file (**NO** file extension). Leaving this variable blank will leave the name the same (which may fail as ffmpeg may not be able to output a file if that name is already taken).

#### *codec*
Type: *String*
> The desired `h26x` codec to use. Defaults to `libx264`

#### *preset*
Type: *String*
> The desired h264 preset to use. Defaults to `veryfast`

#### *crf*
Type: *String*
> The desired crf value to use. Defaults to `17`
***

## <u>`all_XtoY()`</u>
This function attempts to convert all files at the specified filepath, of the input type, to the desired type.
```c#
ffmpeg().all_XtoY( [{path := "A", from := "mkv", to := "mp4"}] )
```
#### *path*
Type: *String*
> The path of the desired files. If no path is provided this parameter defaults to the active windows explorer window.

#### *from*
Type: *String*
> The filetype you wish to convert from.

#### *to*
Type: *String*
> The filetype you wish to convert to.
***

## <u>`trim()`</u>
This function attempts to trim the specified file by the input amount.
```c#
ffmpeg().trim( [path {, startval := 0, durationval?, overwrite := false, commands := ""}] )
```
#### *path*
Type: *String*
> The filepath location of the file being worked on.

#### *startval*
Type: *Integer*
> The number of seconds into the file the user wishes to start the trim.

#### *durationval*
Type: *Integer*
> The number of seconds from the start value the user wishes to trim the file.

#### *overwrite*
Type: *Boolean*
> Whether the originalfile should be overwritten.

#### *commands*
Type: *String*
> Any further commands that will be appended to the command. The default command is `ffmpeg -ss {startval} -i "{filepath}" -t {durationval} {commands} "{outputfile}"`.
***

# <u>`class ffmpeg {`</u>
A class to contain functions used to reload/reset all active ahk scripts.

## <u>`ext_reload()`</u>
A function that will loop through and reload all active ahk scripts.

> This function will ignore `checklist.ahk` unless you set `includeChecklist` to `true`.
```c#
reset.ext_reload( [{includeChecklist := false}] )
```
#### *includeChecklist*
Type: *Any*
> This parameter determines whether the loop will include `checklist.ahk`.
***

## <u>`reset()`</u>
A function that will loop through and hard reset all active ahk scripts.
```c#
reset.reset( [{includeChecklist := false}] )
```
#### *includeChecklist*
Type: *Any*
> This parameter determines whether the loop will include `checklist.ahk`.
***

## <u>`ex_exit()`</u>
A function that will loop through and force close all active ahk scripts.
```c#
reset.ex_exit( [{includeChecklist := false}] )
```
#### *includeChecklist*
Type: *Any*
> This parameter determines whether the loop will include `checklist.ahk`.
***