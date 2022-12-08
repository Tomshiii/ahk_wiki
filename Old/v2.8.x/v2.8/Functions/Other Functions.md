If you've landed on this page, you're probably looking for something more specific. This page is to collect any remaining functions that haven't been detailed in any other page. The functions on this page are generally found in their own ahk file in `..\lib\Functions\`
***
### Table of Contents:
* [errorLog()](#errorlog)
* [getHotkeys()](#getHotkeys)
* [floorDecimal()](#floorDecimal)
* [reload_reset_exit()](#reload_reset_exit)
* [detect()](#detect)
* [SplitPathObj()](#SplitPathObj)
* [getScriptRelease()](#getScriptRelease)
* [mousedrag()](#mousedrag)
***

## `errorLog()`
This function logs errors when a script enters a predetermined block of code that would indicate something went wrong.

Errors are logged in `.txt` files in `..\Error Logs` by default. They are separated by day.

If a file for the current day doesn't exist, this function will create it, and capture a bunch of system information that could be useful when it comes to determining problems.

If a file for the current day does exist, the current log will simply be appended to the end of the file.
```
errorLog( [{err, backupFunc, backupErr, backupLineFile, backupLineNumber}] )
```
#### *err*
Type: *Error Object*
> This variable is an Error Object you can simply pass into the function to prefill all the required information. These error objects are usually found in `try{}/catch{}` blocks.
>
> If the user wishes to log an error outside of a block of code that would throw an Error Object, they can manually input the required information in the remaining parameters and omit this parameter.

#### *backupFunc*
Type: *String/Variable*
> If the user is passing in an Error Object, there is code to still use this variable in the event that the object's `.What` is empty so it is good practice to still include this parameter.
>
> If the user isn't passing in an Error Obkect, this variable is to alert the log if it's being called from a function or a hotkey. If you're calling errorLog() from a function, simply pass `A_ThisFunc "()"`, if you're calling from a hotkey, pass `A_ThisHotkey "::"`.

#### *backupErr*
Type: *String*
> This parameter is a description of the error. This parameter is only necessary if the user isn't passing in an Error Object

#### *backupLineFile*
Type: *String/Variable - Filepath*
> This parameter is the filepath of the script CALLING the function. Simply pass `A_LineFile`. This parameter is only necessary if the user isn't passing in an Error Object

#### *backupLineNumber*
Type: *Integer*
> This parameter is the line number where the error is occuring. Simply pass `A_LineNumber`. This parameter is only necessary if the user isn't passing in an Error Object
***

## `getHotkeys()`
This function is designed to return the names of the first & second hotkeys pressed when two are required to activate a macro.

If the hotkey used with this function is only 2 characters long, it will assign each of those to &first & &second respectively. If one of those characters is a special key (ie. ! or ^) it will return the virtual key so `KeyWait` will still work as expected.
```
getHotkeys( [&first, &second] )
```
#### *first*
Type: *VarRef*
> This parameter is the variable that will be filled with the first activation hotkey.

#### *second*
Type: *VarRef*
> This parameter is the variable that will be filled with the second activation hotkey.

Example
```autoit
RAlt & p::
{
    getHotkeys(&first, &second)
    MsgBox(first) ; returns "RAlt"
    MsgBox(second) ; returns "p"
}

!p::
{
    getHotkeys(&first, &second)
    MsgBox(first) ; returns "vk12"
    MsgBox(second) ; returns "p"
}
```
***

## `floorDecimal()`
`Floor()` is a built in math function of ahk to round down to the nearest integer, but when you want a decimal place to round down, you don't really have that many options. This function will allow us to round down after a certain amount of decimal places.

Original code [found here](https://www.autohotkey.com/board/topic/50826-solved-round-down-a-number-with-2-digits/).
```
floorDecimal( [num, dec] )
```
#### *num*
Type: *Integer*
> This parameter is the number you want this function to evaluate.

#### *dec*
Type: *Integer*
> This parameter is the amount of decimal places you wish the function to evaluate to.
***

## `reload_reset_exit()`
A function that will loop through and either `reload`, `hard reset` (by rerunning the file directly) or `exiting` (by force closing the process) all active AutoHotkey scripts.

This function will ignore `checklist.ahk` unless you set `includeChecklist`.
```
reload_reset_exit( [which, {includeChecklist}] )
```
#### *which*
Type: *String*
> This parameter determines whether the loop will reload, reset or exit all scripts.

#### *includeChecklist*
Type: *Any*
> This parameter determines whether the loop will include `checklist.ahk`.
***

## `detect()`
A function to cut repeat code and set `DetectHiddenWindows` & `SetTitleMatchMode`.
```
detect( [{windows, title}])
```
#### *windows*
Type: *Boolean*
> This parameter determines whether you wish to enable or disable DetectHiddenWindows. It defaults to `true` and can be omitted.

#### *title*
> This parameter determines what `SetTitleMatchMode` you wish to set. It defaults to `2` and can be omitted.
***

## `SplitPathObj()`
This function is a psudo replacement to the built in function `SplitPath` where instead of needing to remember the correct amount of commas for what you need, all variables get returned as an object instead.
```
SplitPathObj( [path] )
```

#### *Path*
Type: *String*
> This parameter is the path you wish to have split by the function.

Example:
```autohotkey
path := "E:\Github\ahk\My Scripts.ahk"
script := SplitPathObj(path)

script.Name       ;returns `My Scripts.ahk`
script.Dir        ;returns `E:\Github\ahk`
script.Ext        ;returns `ahk`
script.NameNoExt  ;returns `My Scripts`
script.Drive      ;returns `E:`
```
***

## `getScriptRelease()`
A function to return the most recent version of my scripts on github. This does NOT use the API and instead downloads a `.atom` of the release page and searches for a certain string to get either the latest full release, or the latest prerelease.
```
getScriptRelease( [{beta}, &changeVer, user, repo] )
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

## `mousedrag()`
This function  allows the user to press a button (best set to a mouse button, eg. `Xbutton1/2`), this script then changes to the desired tool and clicks so the user can drag. Then once the user releases, the function will swap back to a desired tool.
```
mousedrag( [tool, toolorig] )
```
#### *tool*
Type: *String/Variable - Hotkey*
> This parameter is the hotkey you want the program to swap TO (ie, hand tool, zoom tool, etc). (consider using values in KSA)

#### *toolorig*
Type: *String/Variable - Hotkey*
> This parameter is the button you want the script to press to bring you back to your tool of choice. (consider using values in KSA)
***
