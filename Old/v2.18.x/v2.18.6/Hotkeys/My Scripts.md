As my scripts have continued to grow in complexity and become more and more integrated with each other, it has become increasingly relevant for the user to create their *own* version of `My Scripts.ahk` instead of attempting to run my own. This philosophy has been soft forced on the user as of `Release v2.17.0` as the repo will no longer run anything other than `Core Functionality.ahk` by default, and then further with `Release v2.18.0` as the `My Scripts.ahk` that comes bundled with the repo is replaced with nothing but a template to help the user get started with my repo.

If the user wishes to maintain maximum compatibility with functions across the repo then the bare minimum template is required;

```autoit
#SingleInstance Force
#Requires AutoHotkey v2.0

; { \\ #Includes
#Include "%A_Appdata%\tomshi\lib"
#Include Classes\Settings.ahk
#Include Classes\ptf.ahk
#Include Classes\Startup.ahk

 ;// add all other required #Include's
; }

;//! THIS FILE SHOULD ONLY SERVE AS AN EXAMPLE, IT WILL BE OVERRIDDEN DURING ANY UPDATES
;//! MAKE YOUR OWN FILES IN THEIR OWN LOCATION

SetWorkingDir(ptf.rootDir)
SetDefaultMouseSpeed(0)
SetWinDelay(0)
A_MaxHotkeysPerInterval := 400
A_MenuMaskKey := "vkD7"

OnExit(__exit)
__exit(ExitReason, ExitCode) {
    try WinEvent.Stop()
    if ExitReason = "Shutdown"
        ExitApp()
}

#+r::reset.ext_reload() ;this reload script will attempt to reload all active ahk scripts, not only this main script
#+^r::reset.reset()     ;this will hard rerun all active ahk scripts

start := Startup()
start.trayMen()
start.oldLogs()

;// if using adobe apps
start.adobeTemp()
start.adobeVerOverride()
start.checkVersJSON()
;//
start.checkShortcuts()
start.__Delete()
start := ""

#HotIf
; ...

;// if using Premiere and wish to use `Premiere_RightClick.ahk`

;//! Premiere
; #HotIf WinActive(editors.Premiere.winTitle) && !GetKeyState("F24")

;#Include My Scripts\Premiere.ahk ;this is MY premiere hotkeys. It is recommended you replace this with your own

;// I have this here instead of running it separately because sometimes if the main script loads after this one things get funky and break because of priorities and stuff
; #Include Classes\Editors\Premiere_RightClick.ahk
; Ctrl & \::return
```