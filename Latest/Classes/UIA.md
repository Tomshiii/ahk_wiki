Across a lot of the codebase of my repo (with the large majority being related to interfacing with `Premiere`) we interact with some UI elements using a library known as `UIA.ahk`.  
`UIA.ahk` itself is a third party library that is maintained by [Descolada](https://www.github.com/Descolada) that acts as a wrapper for the Microsoft UIAutomation framework. We can then make use of this library to interface with various parts of `Premiere` to do a tonne of things we otherwise wouldn't have been able to do programmatically.

> [!Tip]
> To learn more about the `UIA.ahk` library specifically, check out the repo: https://github.com/Descolada/UIA-v2/wiki

When a function that requires `UIA` coordinates is called, it first checks to see if <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` is running; <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` is a persistent helper script (similar to <img width="16" height="16" src="https://github.com/user-attachments/assets/32d2f140-95bb-4047-83fe-a044ee161e41" /> `Core Functionality.ahk`) designed to retrieve, and store, `UIA` ComObjects that other scripts can then call for and retrieve. It is necessary to facilitate this sharing functionality as generating `UIA` coordinates for Premiere can take anywhere from 7-10s+, doing so each time would make large parts of my repo unusable.  
If <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` already exists and UIA objects have already been generated, it will simply pass those objects back to the calling script.

<img width="527" height="212" alt="Adobe_Premiere_Pro_X5naawl7SI_2" src="https://github.com/user-attachments/assets/ee8b9ec6-b9dd-4583-870f-9a19c47c15f6" />

> [!Caution]
> - Due to technical limitations, all required panels must be VISABLE when the UIA tree is being generated. As a result, determining UIA values **requires** correctly set `KSA.ini` values as it will quickly activate all required panels before attempting to generate the UIA tree.
>     - This means that any required panels can **NOT** be tabbed away next to any other required panels. Unfortunately due to the way that UIA objects are generated (and the way Premiere is coded), attempting to interact with a panel that was tabbed away during tree generation will just result in a stale object reference (if it could even be generated to begin with).  
>     - Keyboard shortcuts to activate all required panels (listed in `Premiere_UIA.ahk`) **MUST** be set within Premiere

To check if `UIA` objects have already been set the following code can be written;
```
#Include '%A_Appdata%\tomshi\lib'
#Include Classes\Editors\Premiere_UIA.ahk

if !premUIA := premUIA_Values.initialise()
    return
; ...
```
***

## Known Quirks
While using this library to interact with Premiere is far more reliable and much faster compared to using keyboard shortcuts and inbuilt ahk functions, it unfortuntely doesn't come without its quirks (that are usually Premieres fault more than anything). Here I will list any odd quirks I encounter alongside any potential ways to avoid the issue;
- These UIA values appear to change depending on what your window layout within Premiere *is* (and as such may require a reload if the user ever changes their window layout).
- Depending on window layout, attempting to focus some panels more than once may result in an unrelated panel opening/stealing focus. As an example, in `v23.5` of Premiere with a certain layout, attempting to highlight some panels multiple times would pull up the `Capture` panel. This issue was unintentially mitigated shortly after experiencing it as I changed my window layout (for unrelated reasons). If you experience this issue, you may need to either adjust your window layout.
- Sometimes UIA will fail to actually generate a UIA tree resulting in it perpetually "attempting" to do so. Usually restarting Premiere is enough to fix the issue but sometimes a full system reboot is required. Currently I am unsure of the cause of this issue, I can only imagine it's something goes on the fritz with Premiere
- Anything not visible to the user essentially does not exist in the UIA tree; this continues to be true as the user is interfacing with Premiere, ie. if a user hides a panel, it disappears from the UIA tree.