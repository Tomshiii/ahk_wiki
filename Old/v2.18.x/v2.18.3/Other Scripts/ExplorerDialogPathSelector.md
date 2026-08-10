`ExplorerDialogPathSelector.ahk` is originally a script by [`ThioJoe`](https://github.com/ThioJoe/) and the original repo can be found [here](https://github.com/ThioJoe/ThioJoe-AHK-Scripts/blob/main/Scripts/ExplorerDialogPathSelector.ahk).

Its original intention is to work only within certain types of explorer windows (generally `save` windows and windows of that nature), however I wanted the functionality expanded to all explorer windows. So with the combination of some [code found on the ahk forums](https://www.autohotkey.com/boards/viewtopic.php?style=19&t=526&start=60) to change the current explorer window to any path, I was able to [fork](https://github.com/Tomshiii/ThioJoe-AHK-Scripts) ThioJoe's repo and implement that functionality. The purpose of these changes are to allow for easier navigation of a project folder while `Premiere Pro` is open.

This functionality can be disabled within [`settingsGUI()`](https://github.com/Tomshiii/ahk/wiki/settingsGUI()) by disabling `Use Thio MButton`.

> [!Warning]
> This script is ultimately not my code (for the vast, vast majority) and as such, any issues you may run into may not be resolved - the use of Thio's script within by repo is fundamentially designed around my own workflow and not a whole lot of consideration has been put into ensuring his expandability/customisability is kept in place.  
> In that same regard, my additions regarding Premiere largly expect the user to be using my [`project folder tree`](https://github.com/Tomshiii/ahk/blob/main/lib/Functions/SD%20Functions/genProjDirs.ahk).

<img src="https://github.com/user-attachments/assets/875278e5-f478-4a21-98a2-2d0615c948a1" width="350"/>