A list of `switchTo` Functions complete with definitions.

All `switchTo` functions are contained within a class called `switchTo` and are called like: `switchTo.X()`

The idea behind these functions was initially showcased by [Taran](https://github.com/TaranVH/2nd-keyboard) a previous editor for LTT.

Their main purpose is to;

* If an instance of the desired program doesn't exist, open it
* If an instance of the desired program DOES exist, activate it
* If multiple instances of the desired program exists, cycle between them based off the last active

A list of `switchTo.` scripts based off this premise includes;

* `switchTo.Explorer()`
* `switchTo.Premiere()`
* `switchTo.AE()`
* `switchTo.Disc()`
    * I have this function move my discord window to a specific position if it's not already. Check that position at the top of the script
* `switchTo.Photo()`
* `switchTo.Firefox()`
* `switchTo.OtherFirefoxWindow()`
    * I use this in other functions for various reasons
* `switchTo.VSCode()`
* `switchTo.Streamdeck()`
* `switchTo.Excel()`
* `switchTo.Word()`
* `switchTo.WindowSpy()`
* `switchTo.Edge()`
* `switchTo.Music()`
***

# Other scripts in this file include

## `switchTo.closeOtherWindow()`
This function when called will close all windows of the desired program EXCEPT the active one. Helpful when you accidentally have way too many windows open.
```c#
switchTo.closeOtherWindow( [program] )
```
#### *program*
Type: *String - Program Information*
> Either `ahk_exe program.exe` or a `ahk_class x` of the desired program.
***

## `newWin()`
This function is specifically designed for my secondary keyboard and works in tandom with the [`switchTo()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions) functions.

If the desired program isn't already open, it will run a first instance, if the desired program is already open, it will run a second instance without disrupting the first.
```c#
newWin( [classorexe, activate, runval] )
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