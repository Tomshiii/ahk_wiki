A list of `Windows.ahk` Functions complete with definitions.

These functions are used in various places across my scripts and are focused around getting information from things relating to windows, or just performing repetitive tasks.
***

## `youMouse()`
This function is used to skip `forward/backwards` in youtube.

The purpose of this script was to manipulate a youtube video, not only just with a mouse, but also even if youtube is the current active window.
```
youMouse( [tenS, fiveS] )
```
#### *tenS*
Type: *String/Variable - Hotkey*
> The hotkey for 10s skip in your direction of choice (`j/l`)

#### *fiveS*
Type: *String/Variable - Hotkey*
> The hotkey for 5s skip in your direction of choice (`Left/Right`)
***

## `monitorWarp()`
Warp anywhere on your desktop
```
monitorWarp( [x, y] )
```
#### *x*
Type: *Integer*
> The x value

#### *y*
Type: *Integer*
> The y value
***

## `jumpChar()`
This function is to allow the user to simply jump 10 characters in either direction. Useful when `^Left/^Right` isn't getting you to where you want the cursor to be.
```
jumpChar( [{amount}] )
```
#### *amount*
Type: *Integer*
> This parameter is the amount of characters you want this function to jump, by default it is set to 10 and isn't required if you do not wish to override this value.
***

## `fastWheel()`
This function facilitates accelerated scrolling. If the window under the cursor isn't the active window when this function is called, it will activate it.

*This function use to send 10 WheelUp/Down events but that just kept lagging everything out no matter what I tried to do to fix it, so now it sends PgUp/Dn*
***

## `refreshWin()`
A function to close a window, then reopen it in an attempt to refresh its information (for example, a txt file).

If the user passes `"A"` into both of the variables to indicate they want to focus on the active window and said active window is either `Notepad*` or `Windows Explorer`, there is added code in this function to retrieve the filepath of said window and reopen it automatically.

**If there are multiple notepad windows open, this function will refresh all of them.*
```
refreshWin( [window, runTarget] )
```
#### *window*
Type: *String/Variable*
> This parameter is the window you wish to target and close.

#### *runTarget*
Type: *String - Filepath*
> This parameter is the path of the file you wish to open.
***