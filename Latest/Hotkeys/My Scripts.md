`My Scripts.ahk` is the main script of my entire repo, it's what helps facility most of the "experience" that helps make my collection of scripts seem less like singular macros and more like an entire package.

Alongside all the functions that run [on startup](https://github.com/Tomshiii/ahk/wiki/Startup-Functions), this script also contains a bunch of macros of it's own.
***

`My Scripts.ahk` starts off by declaring `MyRelease`, a global variable to dictate the release version you are running. We use this variable in some functions.

Then we define some settings.

* `#SingleInstance Force` to ensure only one instance of these scripts is open.
* `SetWorkingDir(A_ScriptDir)` to set a consistent working directory.
* `SetNumLockState("AlwaysOn")` to always have numlock enabled (a personal preference).
* `SetCapsLockState("AlwaysOff")` to set CapsLock to be always disabled. This doesn't stop us from using it as a hotkey.
* `SetScrollLockState("AlwaysOff")` to set ScrollLock to be always disabled. This doesn't stop us from using it as a hotkey.
* `SetDefaultMouseSpeed(0)` to set the default mouse speed to be instant
* `SetWinDelay(0)` to set the default window delay to be instant.

Then we set our tray icon, `#Include` our functions & `right click premiere.ahk` and we're done.

From there, this script will run through it's [startup functions](https://github.com/Tomshiii/ahk/wiki/Startup-Functions) before finally hitting its hotkey definitions.

On this page, I will be referring to macros by their `;Hotkey;` tag and not their keybindings. This is to reduce the need for change in the event that a keybinding changes.
***

### Table of Contents:
* [Windows Macros](#Windows-Macros)
* [Launch Programs](#Launch-Programs)
* [Other](#Other)
    * #HotIf
        * [`WinActive(windows explorer)`](#hotif-winactivewindows-explorer)
        * [`WinActive(VSCode)`](#hotif-winactivevscode)
        * [`WinActive(firefox)`](#hotif-winactivefirefox)
        * [`WinActive(Discord)`](#hotif-winactivediscord)
        * [`WinActive(Photoshop)`](#hotif-winactivephotoshop)
        * [`WinActive(After Effects)`](#hotif-winactiveafter-effects)
        * [`WinActive(Premiere Pro)`](#hotif-winactivepremiere-pro)
            * [Mouse Scripts](#mouse-scripts)
* [Other - NOT an editor](https://github.com/Tomshiii/ahk/wiki/My-Scripts.ahk#other---not-an-editor)
***

# Windows Macros

### #SuspendExempt
*The below hotkeys will function even while the script is suspended.*

## `reloadHotkey`
runs: [`reload_reset_exit("reload")`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#reload_reset_exit)

## `hardresetHotkey`
runs: [`reload_reset_exit("reset")`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#reload_reset_exit)

## `panicExitHotkey`
runs: [`reload_reset_exit("exit")`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#reload_reset_exit)

## `panicExitALLHotkey`
runs: [`reload_reset_exit("exit", true)`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#reload_reset_exit)

## `settingsHotkey`
runs: [`settingsGUI()`](https://github.com/Tomshiii/ahk/wiki/GUI)

## `activescriptsHotkey`
runs: [`activeScripts(MyRelease)`](https://github.com/Tomshiii/ahk/wiki/GUI)

## `handyhotkeysHotkey`
runs [`hotkeysGUI()`](https://github.com/Tomshiii/ahk/wiki/GUI)

## `suspendHotkey`
This hotkey will toggle suspend `My Scripts.ahk`. Useful when booting up a game that hasn't been added to gameCheck yet.

### #SuspendExempt false
*everything below here will no longer work while script is suspended*
***

## `capsHotkey`
This hotkey, on a douple tap of the CapsLock button will toggle the state of CapsLock. This hotkey is only necessary because I have capslock disabled by default.

## `centreHotkey`
This hotkey will centre the active window in the middle of the monitor it is active within. If pressed a second time on the same window, it will move it to the centre of the main monitor.

If the active window is a youtube window, it will be slightly larger to give the user more video viewing space.

## `fullscreenHotkey`
This hotkey will check the state of the active window - if it is not currently fullscreen, it will maximise it, if it is, it will unmaximise it.

## `jump10charLeftHotkey` & `jump10charRightHotkey`
These hotkeys will run: [`jumpChar()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#jumpchar).

## `refreshWinHotkey`
runs [`refreshWin()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#refreshwin) passing the active window as the desired target. If the target window is `Notepad.exe` or `explorer.exe` it is able to determine the filepath of the current window and reopen it.
***

# Launch Programs

## `windowspyHotkey`
runs: [`switchTo.WindowSpy()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions)

## `vscodeHotkey`
runs: [`switchTo.VSC()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions)

## `streamdeckHotkey`
runs: [`switchTo.Streamdeck()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions)

## `taskmanagerHotkey`
Sends `^+{Esc}` to open the taskmanager.

## `excelHotkey`
runs: [`switchTo.Excel()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions)

## `ahkdocuHotkey`
Attempts to open the local documentation, if the file can't be found it will fallback to the [ahk documentation](https://lexikos.github.io/v2/docs/AutoHotkey.htm)

## `ahksearchHotkey`
Attempts to search the highlighted text in the local ahk documentation, before falling back to the online documentation in the event that the local file can't be found.
***

# Other

## `moveXHotkey` & `moveYHotkey`
run: [`move.XorY()`](https://github.com/Tomshiii/ahk/wiki/Other-Classes#movexory)

## #HotIf `WinActive(windows explorer)`
*The below hotkeys only activate while windows explorer is the active window.*

## `explorerbackHotkey`
Remaps `!{Up}` to another button. (I have it set to `WheelLeft`)

## #HotIf `WinActive(VSCode)`
*The below hotkeys only activate while VSCode is the active window.*

## `vscodeHotkeys`
run: [`VSCode.script()`](https://github.com/Tomshiii/ahk/wiki/VSCode.ahk#vscodescript)

## `vscodesearchHotkey`
run: [`VSCode.search()`](https://github.com/Tomshiii/ahk/wiki/VSCode.ahk#vscodesearch)

I have a habit in VSCode of trying to use `^f` to search, while the explorer window is open instead of the code window. To combat this I made a hotkey that would highlight the code window first. In using that I realised that it would start the search field with the previous search. I didn't like this either and only wanted it to contain text if I had text highlighted.

For this hotkey to work `editor.emptySelectionClipboard` must be set to false within VSCode. Because otherwise, sending `^c` to copy text while nothing is selected will copy the entire line which makes it impossible to check and see if the user has something highlighted.

## `vscodecutHotkey`
run: [`VSCode.cut()`](https://github.com/Tomshiii/ahk/wiki/VSCode.ahk#vscodecut)

This hotkey is to return the usual experience of pressing `^x` in vscode (it will delete the entire line if nothing is selected). This experience only occurs while `editor.emptySelectionClipboard` is enabled however, so as we have it disabled, we needed a workaround.

## `vscodeCopyHotkey`
run: [`VSCode.copy()`](https://github.com/Tomshiii/ahk/wiki/VSCode.ahk#vscodecopy)

This hotkey is to return the usual experience of pressing `^c` in vscode (it will copy the entire line if nothing is selected). This experience only occurs while `editor.emptySelectionClipboard` is enabled however, so as we have it disabled, we needed a workaround.

## #HotIf `WinActive(firefox)`
*The below hotkeys only activate while firefox is the active window.*

## `pauseyoutubeHotkey`
This hotkey will search for and pause a youtube video if it exists.

## `numpadytHotkey`
These hotkey assignments disable the numpad while youtube is the active window to stop the user from accidentally bumping the numpad and teleporting somewhere in the video.

## `movetabHotkey`
runs: [`move.Tab()`](https://github.com/Tomshiii/ahk/wiki/Other-Classes#movetab)

## #HotIf `WinActive(Discord)`
*The below hotkeys only activate while discord is the active window.*

## `discHotkeys`
These hotkeys will run their respective: [`discord.button()`](https://github.com/Tomshiii/ahk/wiki/Discord.ahk#button) function.

## `discitalicHotkey`
This hotkey will remap `+*` to `^i` to italicise the highlighted text

## `discserverHotkey`
runs: [`discord.Unread()`](https://github.com/Tomshiii/ahk/wiki/Discord.ahk#discordunread)

## `discmsgHotkey`
runs: [`discord.Unread(2)`](https://github.com/Tomshiii/ahk/wiki/Discord.ahk#discordunread)

## `discdmHotkey`
This hotkey will click a the dm button on discord
***

## #HotIf `WinActive(Photoshop)`
*The below hotkeys only activate while Adobe Photoshop is the active window.*

## `fileTypeHotkeys`
These hotkeys run: [`ps.Type()`](https://github.com/Tomshiii/ahk/wiki/Adobe-Functions#pstype) with the requested filetype as their parameters

## `photoopenHotkey`, `photoselectHotkey` & `photozoomHotkey`
runs: [`mousedrag()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#mousedrag) with different tools
***

## #HotIf `WinActive(After Effects)`
*The below hotkeys only activate while Adobe After Effects is the active window.*

## `aetimelineHotkey`
runs: [`ae.timeline()`](https://github.com/Tomshiii/ahk/wiki/Adobe-Functions#aetimeline)

## `aeselectionHotkey`
runs: [`mousedrag()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#mousedrag)

## `aepreviousframHotkey` & `aenextframeHotkey`
Send the hotkey for either the `previousKeyframe` or `nextKeyframe` which are both set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments)
***

## #HotIf `WinActive(Premiere Pro)`
*The below hotkeys only activate while Adobe Premiere Pro is the active window.*

## `stopTabHotkey`
This hotkey disables `Tab` within Premiere. I find it does nothing but make a mess of things so I opt to disable it completely.

## `linkActivateHotkey`
This hotkey reactivates the clips currently on the timeline after unlinking/linking them as Premiere deselects them by default.

## `prem^DeleteHotkey`
This hotkey returns the normal windows ability to press `Ctrl & BackSpace` to delete an entire word at a time.

## `premzoomoutHotkey`
Sends the hotkey for `zoomOut` which is set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments)

## `premselecttoolHotkey`
While you're editing text, getting back to the selection tool by pressing (in my case) `v` would just type `v` in the text box. This hotkey will attempt to warp to and press the selection tool instead. If that fails, it will focus the tool hotbar and then input `v` instead.
> This function will focus the `Program Monitor` after it is complete

## `premprojectHotkey`
A hotkey to open my editing folder.

## `12forward/backHotkey`
These hotkeys will move the playhead 12 frames in the desired direction.
***

# Mouse Scripts

## `previouseditHotkey` & `nexteditHotkey`
run: [`prem.wheelEditPoint()`](https://github.com/Tomshiii/ahk/wiki/Adobe-Functions#premwheeleditpoint) with their respective directions which is set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments).

## `playstopHotkey`
Sends the hotkey `playStop` (which is set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments)) to stop playback on the timeline. I have this bound to a button on my mouse.

## `nudgeupHotkey` & `nudgedownHotkey`
Send hotkeys relating to their respective direction to nudge tracks on the timeline. Hotkeys are set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments).

## `slowDownHotkey` & `speedUpHotkey`
Send hotkeys relating to the respect speed change, to speed up or slow down playback on the timeline. Hotkeys are set within [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments).

## `mousedragHotkey`
runs: [`prem.mousedrag()`](https://github.com/Tomshiii/ahk/wiki/Adobe-Functions#premmousedrag)

## `bonkHotkey` & `bleepHotkey`
runs: [`prem.audioDrag()`](https://github.com/Tomshiii/ahk/wiki/Adobe-Functions#premaudiodrag) with the respective audiofile name passed as the variable.
***

## Other - NOT an editor

## #HotIf `not WinActive("ahk_group Editors")`
*The below hotkeys only activate while a window in the group `Editors` is NOT the active window.*

## `winHotkeys`
runs: [`move.Window()`](https://github.com/Tomshiii/ahk/wiki/Other-Classes#movewindow) with the respective hotkeys passed in as the variable to manipulate windows with just my mouse.

## `alwaysontopHotkey`
Toggles `AlwaysOnTop` for the active window.

## `searchgoogleHotkey`
Searches the highlighted text in google.

## `capitaliseHotkey`
Will attempt to determine whether to completely capilitilse or lowercase the highlighted text depending on which is more frequent.

## `timeHotkey`
Will send `A_YYYY "-" A_MM "-" A_DD`

## `wheelupHotkey` & `wheeldownHotkey`
runs: [`fastWheel()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#fastwheel) to speed up scrolling.

## `youskipbackHotkey` & `youskipforHotkey`
runs: [`youMouse()`](https://github.com/Tomshiii/ahk/wiki/Other-Functions#youmouse) with the respective hotkeys passed in as the variables to skip ahead/back in youtube.