Across a lot of the codebase of my repo (with the large majority being related to interfacing with `Premiere`) we interact with some UI elements using a library known as `UIA.ahk`.  
`UIA.ahk` itself is a third party library that is maintained by [Descolada](https://www.github.com/Descolada) that acts as a wrapper for the Microsoft UIAutomation framework. We can then make use of this library to interface with various parts of `Premiere` to do a tonne of things we otherwise wouldn't have been able to do programmatically.

> [!Tip]
> To learn more about the `UIA.ahk` library specifically, check out the repo: https://github.com/Descolada/UIA-v2/wiki

When a function that requires `UIA` coordinates is called, it first checks to see if <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` is running; <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` is a persistent helper script (similar to <img width="16" height="16" src="https://github.com/user-attachments/assets/32d2f140-95bb-4047-83fe-a044ee161e41" /> `Core Functionality.ahk`) designed to retrieve, and store, `UIA` ComObjects that other scripts can then call for and retrieve. It is necessary to facilitate this sharing functionality as ~~generating `UIA` coordinates for Premiere can take anywhere from 7-10s+~~ (*This is no longer accurate. This slow initialisation was fixed in Premiere 26.5 and is now near instant again. Sharing around the singular object is still faster than generating the entire tree every single time however*), doing so each time would make large parts of my repo unusable.  
If <img width="16" height="16" src="https://github.com/user-attachments/assets/475aa61e-0055-4831-9f18-1f564b6bd41e" /> `determineUIA.ahk` already exists and UIA objects have already been generated, it will simply pass those objects back to the calling script.

<img width="527" height="212" alt="Adobe_Premiere_Pro_X5naawl7SI_2" src="https://github.com/user-attachments/assets/ee8b9ec6-b9dd-4583-870f-9a19c47c15f6" />

> [!Caution]
> - Due to technical limitations, all required panels must be VISABLE when the UIA tree is being generated. While functions will make an attempt to retrieve a live version of the respective object when using a given function, some panels may not work if they weren't visible during initial initialisation.

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
- Due to the nature of how UIA works, there is unfortunately a large amount of hardcoded `English` values (mostly `Name:` values). If the user's windows installation, or any relevant programs are installed, or using another language it is highly likely they will encounter issues with a lot of functions throughout this entire repo.
- Some UIA objects may go stale, and as such may require re-initialisation, if the user ever changes their window layout.
- Anything not visible to the user essentially does not exist in the UIA tree; this continues to be true as the user is interfacing with Premiere, ie. if a user hides a panel, it disappears from the UIA tree.