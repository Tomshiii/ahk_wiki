As my scripts have continued to grow in complexity and become more and more integrated with each other, it has become increasingly relevant for the user to create their *own* version of `My Scripts.ahk` instead of attempting to run my own. This philosophy has been soft forced on the user as of `Release v2.17.0` as the repo will no longer run anything other than `Core Functionality.ahk` by default.

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

SetWorkingDir(ptf.rootDir)
SetDefaultMouseSpeed(0)
SetWinDelay(0)
A_MaxHotkeysPerInterval := 400
A_MenuMaskKey := "vkD7"

OnError(checkRPC)
checkRPC(err, *) {
    if err.Message = "(0x800706BA) The RPC server is unavailable." { ;(0x800706BA)
        errorLog(TargetError("Script could not interact with ``Core Functionality.ahk``. Script will now close.", -1))
        ExitApp()
    }
}
OnExit(__exit)
__exit(ExitReason, ExitCode) {
    try WinEvent.Stop()
    if ExitReason = "Shutdown"
        ExitApp()
}

start := Startup()
start.generate()
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
errorLog({state:"empty"})

;// so settingsGUI() can interact with multiple scripts
onMsgObj := ObjBindMethod(WM, "__recieveMessage")
OnMessage(0x004A, onMsgObj.Bind())  ; 0x004A is WM_COPYDATA

#HotIf
; ...

;// if using Premiere and wish to use `Premiere_RightClick.ahk`

;//! Premiere
#HotIf WinActive(editors.Premiere.winTitle) && !GetKeyState("F24")

;#Include My Scripts\Premiere.ahk ;this is MY premiere hotkeys. It is recommended you replace this with your own

;// I have this here instead of running it separately because sometimes if the main script loads after this one things get funky and break because of priorities and stuff
#Include Classes\Editors\Premiere_RightClick.ahk
```