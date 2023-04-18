If you've landed on this page, you're probably looking for something more specific. This page is to collect any remaining functions that haven't been detailed in any other page. The functions on this page are generally found in their own ahk file in `..\lib\Functions\`
***
### Table of Contents:
* [alwaysOnTop()](#alwaysOnTop)
* [errorLog()](#errorlog)
* [change_msgButton()](#change_msgButton)
* [getHotkeys()](#getHotkeys)
* [floorDecimal()](#floorDecimal)
* [reload_reset_exit()](#reload_reset_exit)
* [detect()](#detect)
* [getScriptRelease()](#getScriptRelease)
* [mousedrag()](#mousedrag)
* [getLocalVer()](#getLocalVer)
* [checkInternet()](#checkInternet)
* [getHTML()](#getHTML)
* [getHTMLTitle()](#getHTMLTitle)
* [youMouse()](#youMouse)
* [monitorWarp()](#monitorWarp)
* [jumpChar()](#jumpChar)
* [fastWheel()](#fastWheel)
* [refreshWin()](#refreshWin)
* [checkImg()](#checkImg)
* [delaySI()](#delaySI)
* [isReload()](#isReload)
* [unzip()](#unzip)
* [timeline()](#timeline)
* [pauseYT()](#pauseYT)
***

## <u>`alwaysOnTop()`</u>
This function will toggle the desired window (the active window by default) and attempt to draw an orange border around it (`win11` only).
***

## <u>`change_msgButton()`</u>
Changes the button names of a generated msgbox. This function is best called via a settimer.
```c#
change_msgButton( [title, buttons*] )
```
#### *title*
Type: *String*
> This variable is the title of the message box you wish to wait for.

#### *buttons*
Type: *Varadic/String*
> This variable is to define the new text you wish the buttons to show.

<u>Example #1</u>
```autoit
title := "Change Buttons"
SetTimer(change_msgButton.Bind(title, "OK", "Open Dir"), 16)
;// will wait for a msgbox with a title "Change Buttons" and swap the first two buttons to "OK" & "Open Dir"
```
***

## <u>`errorLog()`</u>
This function logs errors when a script enters a predetermined block of code that would indicate something went wrong.

Errors are logged in `.txt` files in `..\Error Logs` by default. They are separated by day. Errors are also sent via `OutputDebug()`

If a file for the current day doesn't exist, this function will create it, and capture a bunch of system information that could be useful when it comes to determining problems.

If a file for the current day does exist, the current log will simply be appended to the end of the file.
```c#
errorLog( [{err, optMessage?, toolCust := false, doThrow := false}] )
```
#### *err*
Type: *Error Object*
> This variable is an Error Object. These objects contain a bunch of useful information that `errorLog()` will use to display a useful error message to the user

#### *optMessage*
Type: *String*
> If you wish to pass an extra message alongside the main error message, pass a string to this variable and it will be appended to the next like of the error.

#### *toolCust*
Type: *Boolean/Object*
> This parameter tells the function whether you wish for a tooltip of the error to be displayed as the error occurs.
>> If this variable is set to `true` it will simply generate a `tool.Cust()` tooltip of the current error for `1.5s`. If the user wishes to generate a more custom tooltip, pass an object instead. See Example #1 for available options.

#### *doThrow*
Type: *Boolean*
> This parameter tells the function whether you wish to automatically `throw` with the passed in Error Object.
<u>Example #1</u>
```autoit
errorLog(
    Error("This is a generic error", -1)    ;// The error object
    , "This is a second message"            ;// The second message
    , {x: 30, y: 30, time: 3.0, ttip: 5}    ;// Custom tooltip parameter. These set the `x`, `y`, `timeout` & `WhichToolTip` variables in `tool.Cust()`
    , 1                                     ;// Will throw with the passed in Error Object
)
```
***

## <u>`getHotkeys()`</u>
This function is designed to return the names of the first & second hotkeys pressed when two are required to activate a macro.

If the hotkey used with this function is only 2 characters long, it will assign each of those to &first & &second respectively. If one of those characters is a special key (ie. ! or ^) it will return the virtual key so `KeyWait` will still work as expected.
```c#
getHotkeys( [{&first?, &second?}] )
```
#### *first*
Type: *VarRef*
> This parameter is the variable that will be filled with the first activation hotkey.

#### *second*
Type: *VarRef*
> This parameter is the variable that will be filled with the second activation hotkey.

### Return Value
Type: *Object*
> This function returns an object containing the first and second hotkey.

<u>Example #1</u>

```autoit
RAlt & p::
{
    hotkeys := getHotkeys()
    MsgBox(hotkeys.first)  ; returns "RAlt"
    MsgBox(hotkeys.second) ; returns "p"
}

!p::
{
    getHotkeys(&first, &second)
    MsgBox(first)  ; returns "vk12"
    MsgBox(second) ; returns "p"
}
```
***

## <u>`floorDecimal()`</u>
`Floor()` is a built in math function of ahk to round down to the nearest integer, but when you want a decimal place to round down, you don't really have that many options. This function will allow us to round down after a certain amount of decimal places.

Original code [found here](https://www.autohotkey.com/board/topic/50826-solved-round-down-a-number-with-2-digits/).
```c#
floorDecimal( [num, dec] )
```
#### *num*
Type: *Integer*
> This parameter is the number you want this function to evaluate.

#### *dec*
Type: *Integer*
> This parameter is the amount of decimal places you wish the function to evaluate to.
***

## <u>`reload_reset_exit()`</u>
A function that will loop through and either `reload`, `hard reset` (by rerunning the file directly) or `exiting` (by force closing the process) all active AutoHotkey scripts.

This function will ignore `checklist.ahk` unless you set `includeChecklist`.
```c#
reload_reset_exit( [which, {includeChecklist}] )
```
#### *which*
Type: *String*
> This parameter determines whether the loop will reload, reset or exit all scripts.

#### *includeChecklist*
Type: *Any*
> This parameter determines whether the loop will include `checklist.ahk`.
***

## <u>`detect()`</u>
A function to cut repeat code and set `DetectHiddenWindows` & `SetTitleMatchMode`.
```c#
detect( [{windows, title}])
```
#### *windows*
Type: *Boolean*
> This parameter determines whether you wish to enable or disable DetectHiddenWindows. It defaults to `true` and can be omitted.

#### *title*
> This parameter determines what `SetTitleMatchMode` you wish to set. It defaults to `2` and can be omitted.

### Return Value
Type: *Object*
> This function returns an object containing the original `A_DetectHiddenWindows` & `A_TitleMatchMode` states

<u>Example #1</u>
```
dct := detect()
dct.Windows      ;// returns the original `A_DetectHiddenWindows` value
dct.Title        ;// returns the original `A_TitleMatchMode` value
```
***

## <u>`getScriptRelease()`</u>
A function to return the most recent version of my scripts on github. This does NOT use the API and instead downloads a `.atom` of the release page and searches for a certain string to get either the latest full release, or the latest prerelease.
```c#
getScriptRelease( [{beta, &changeVer, user, repo}] )
```
#### *beta*
Type: *Boolean*
> A `true/false` to determine if you want this function to check for a full release, or a prerelease. Can be omitted.

#### *&changeVer*
Type: *VarRef*
> Determines which changelog to show in `updateChecker()` GUI. Either returns "main" or "beta".

#### *user*
Type: *String*
> Determines which github user to check for.

#### *repo*
Type: *String*
> Determines which github repo to check for.

### Return Value
Type: *String*
> This function returns a string containing the latest version number.
***

## <u>`mousedrag()`</u>
This function  allows the user to press a button (best set to a mouse button, eg. `Xbutton1/2`), this script then changes to the desired tool and clicks so the user can drag. Then once the user releases, the function will swap back to a desired tool.
```c#
mousedrag( [tool, toolorig] )
```
#### *tool*
Type: *String/Variable - Hotkey*
> This parameter is the hotkey you want the program to swap TO (ie, hand tool, zoom tool, etc).
>
>> (consider using values in KSA)

#### *toolorig*
Type: *String/Variable - Hotkey*
> This parameter is the button you want the script to press to bring you back to your tool of choice.
>
>> (consider using values in KSA)
***

## <u>`getLocalVer()`</u>
This function retrieves the local version (or the string after a specified tag) and then returns it.

**note: This script will trim whitespace, tabs, newlines & carriage returns*
```c#
getLocalVer( [{varRead, script, searchTag, endField}] )
```

#### *varRead*
Type: *String/Variable*
> If this variable is populated, it will read from the passed string instead of filereading (potentially again).

#### *script*
Type: *String*
> This parameter is the name of the script you wish to read (*if in the root dir*, otherwise the remaining filepath to it)

#### *searchTag*
Type: *String*
> This parameter is what you want the function to search for (your desired return value should come directly after this search tag).

#### *endField*
Type: *String*
> This parameter is what you want "InStr" to search for to be the end of your string. (this should come directly after your desired return value)

### Return Value
Type: *String*
> Returns a string of whatever is between the searchTag and endField.
>
>> **note: This script will trim whitespace, tabs, newlines & carriage returns*
***

## <u>`checkInternet()`</u>
This function will check if the user has an internet connection.
```c#
checkInternet()
```
### Return Value
Type: *Boolean*
> Returns a true/false value to represent if the user has an internet connection.
***

## <u>`getHTML()`</u>
This function creates a `ComObject - WinHttpRequest` and returns the given url as a string
```c#
getHTML( [url] )
```
#### *url*
Type: *String*
> The url you wish to pass into the function that will be returned.

### Return Value
Type: *String*
> Returns a string of the contents of the url parameter.
***

## <u>`getHTMLTitle()`</u>
This function creates a `ComObject - WinHttpRequest` and returns the title of the given url
```c#
getHTMLTitle( [url {, sanitise, replace, params*}] )
```
#### *url*
Type: *String*
> The url you wish to pass into the function that will be be parsed.

#### *sanitise*
Type: *Boolean*
> Whether you want the returned title to be stripped of illegal filename chars.

#### *replace*
Type: *String*
> The default character to replace illegal characters with. This parameter defaults to `_`

#### *params**
Type: *String*
> If you wish to manually replace individual illegal characters from left to right, list them out separated by `,`. Any illegal characters that aren't given a `params` string to be replaced with will default back to `replace`.
>> If this parameter is passed `replace` acts as the first found illegal character and the first `params` counts as the secound found character and so on.

### Return Value
Type: *String*
> Returns a string of the title found from the url parameter.
***

## <u>`youMouse()`</u>
This function is used to skip `forward/backwards` in youtube.

The purpose of this script was to manipulate a youtube video, not only just with a mouse, but also even if youtube is the current active window.
```c#
youMouse( [tenS, fiveS] )
```
#### *tenS*
Type: *String/Variable - Hotkey*
> The hotkey for 10s skip in your direction of choice (`j/l`)

#### *fiveS*
Type: *String/Variable - Hotkey*
> The hotkey for 5s skip in your direction of choice (`Left/Right`)
***

## <u>`monitorWarp()`</u>
Warp anywhere on your desktop
```c#
monitorWarp( [x, y] )
```
#### *x*
Type: *Integer*
> The x value

#### *y*
Type: *Integer*
> The y value
***

## <u>`jumpChar()`</u>
This function is to allow the user to simply jump 10 characters in either direction. Useful when `^Left/^Right` isn't getting you to where you want the cursor to be.
```c#
jumpChar( [{amount}] )
```
#### *amount*
Type: *Integer*
> This parameter is the amount of characters you want this function to jump, by default it is set to 10 and isn't required if you do not wish to override this value.
***

## <u>`fastWheel()`</u>
This function facilitates accelerated scrolling. If the window under the cursor isn't the active window when this function is called, it will activate it.
***

## <u>`refreshWin()`</u>
A function to close a window, then reopen it in an attempt to refresh its information (for example, a txt file).

If the user passes `"A"` into both of the variables to indicate they want to focus on the active window and said active window is either `Notepad*` or `Windows Explorer`, there is added code in this function to retrieve the filepath of said window and reopen it automatically.

**If there are multiple notepad windows open, this function will refresh all of them.*
```c#
refreshWin( [window, runTarget] )
```
#### *window*
Type: *String/Variable*
> This parameter is the window you wish to target and close.

#### *runTarget*
Type: *String - Filepath*
> This parameter is the path of the file you wish to open.
***

## <u>`checkImg()`</u>
A function to check if a file exists and perform an `ImageSearch` at the same time. This can be useful when you need to test for a variety of images due to slight aliasing breaking things.
```c#
checkImg( [checkfilepath, {&returnX, &returnY, x1 := 0, y1 := 0, x2 := A_ScreenWidth, y2 := A_ScreenHeight, tooltips := false}] )
```
#### *checkfilepath*
Type: *String*
> This parameter is the filepath of the image you wish to check

#### *returnX*
Type: *VarRef*
> The `x variable` the imagesearch will return

#### *returnY*
Type: *VarRef*
> The `Y variable` the imagesearch will return

#### *x1/2 & y1/2*
Type: *Integer*
> These parameters are the coordinates you want the imagesearch to check.
>> They will default to: 0, 0, A_ScreenWidth, A_ScreenHeight

#### *tooltips*
Type: *Boolean/Object*
> This parameter is whether you want `errorLog()` to produce tooltips if it runs into an error. This parameter can be a simple true/false or an object that errorLog is capable of understanding
***

## <u>`delaySI()`</u>
A function to send a string of sendinput commands that are staggered out with set sleep value.
```c#
delaySI( [delay, inputs*] )
```
#### *delay*
Type: *Integer*
> This parameter is the amount of sleep you wish to take place between each input
>> This sleep happens **AFTER** each input is sent.

#### *inputs**
Type: *String* - *Varadic*
> This parameter is the inputs (in order) you wish for the function to use. They will be sent with `SendInput`.
>> This parameter can accept any amount of inputs

<u>Example #1</u>
```autoit
delaySI(500, "^a", "^c", "^v")
;// will send `Ctrl+a` & sleep 500ms
;// then `Ctrl+c` & sleep 500ms
;// then finally `Ctrl+v` & sleep 500ms
```
***

## <u>`isReload()`</u>
This function checks to see if the current script was run via a reload.

<u>Example #1</u>
```autoit
if isReload()
    return
;// if the script was reloaded, beyond this point will not fire
```
***

## <u>`unzip()`</u>
This function creates a comObject to unzip a folder.

*Original function from @MiM in ahk discord: https://discord.com/channels/115993023636176902/1068688397947900084/1068710942327722045 (link may die)*
```c#
unzip( [zipPath, unzippedPath] )
```
#### *zipPath*
Type: *String*
> This parameter is the path location of a zip folder you wish to unzip.

#### *unzippedPath*
Type: *String*
> This parameter is the path location you wish the contents of the zip folder to get extracted. If this directory does not already exist, it will be created.

### Return Value
Type: *Boolean*
> On success this function will return `true`.
***

## <u>`timeline()`</u>
This function is a weaker version of the [`right click premiere`](https://github.com/Tomshiii/ahk/wiki/right-click-premiere.ahk) script. Set this to a button (mouse button ideally, or something obscure like ctrl + capslock).
```c#
timeline( [timeline, x1, x2, y1] )
```
#### *timeline*
Type: *Integer*
> This parameter is the `y` pixel value of the top bar in your video editor that allows you to click it to drag along the timeline. Your mouse will be warped to this `y` value to click it.

#### *x1/x2/y1*
Type: *Integer*
> These paramaters are the furthest left/right pixel value & the top most pixel value of your timeline window. Attempting to activate your hotkey outside these bounds will have no effect.
***

## <u>`pauseYT()`</u>
This function will search for the yt logo on your tab bar, then select it and input a <kbd>Space</kbd> to `play/pause`.