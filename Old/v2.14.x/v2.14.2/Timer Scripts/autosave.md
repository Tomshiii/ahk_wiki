> [!Caution]
> This script requires you to properly set the year version of premiere within `settingsGUI()` (<kbd>win + F1</kbd> by default)

> [!Warning]
> **Known quirks of this script:** 
> - Can in rare cases cause a cut on the `Premiere` timeline.
> - `After Effects` tries to steal focus during its saving process and may disappear from the screen in certain scenarios (explained below).

Adobe products are notoriously known for their instability and overall untrustworthy behaviour. After losing one too many projects to a crash only to find autosave hadn't actually saved at all in the last 30 minutes, I looked to find a solution.  
`autosave.ahk` is that solution.

This script has one main functions;

### **Autosave `unsaved` work every `5min` (by default)**
The order of operations is simple:

- `autosave.ahk` will first grab information about the active window so we can reactivate it later if necessary
- Then it will determine whether `Premiere Pro` or `After Effects` is open and check the title of each window for a little `*` - an asterisk indicates that changes have been made that haven't been saved
- It will then backup the current `.prproj` and `.aep` files
- It will then proceed with attempting to save the unsaved projects

> [!Note]
> If Premiere was the original active window and you were playing back footage on the timeline, this script will attempt to resume playback again once saving is complete.
> - ⚠️ *If you were playing back at any speed other than realtime, unfortunately there's no way to distinguish that and only normal speed playback can be returned.* ⚠️

> [!Note]
> This script behaves differently depending on a few settings that can be set within `settingsGUI()`

If `Premiere Pro` requires saving, this function can do so without needing to bring focus to premiere at all (if it isn't already the active window), so the user will not even realise it is happening.

During the scripts save attempt it will check to determine if the user has been idle for a short period of time before proceeding. If the script determines that you've interacted with the keyboard or mouse recently it will alert the user they have done so and reattempt the process after a few seconds. If the user continues to interact with the PC the script will prompt the user with a few short beeps that it is attempting to save. This reattempt process only happens a handful of times before it will give up on the save attempt and try again after 5min.

## After Effects Quirks
> While saving `Premiere Pro` is rather straight forward and can be done in the background, `After Effects` on the other hand is a bit stranger. Saving After effects, even in the background will **FORCE** it to become the focused window. Annoying. So what this script does to compensate is this:

- If a save is required and After Effects is the `active window` then simple, just save with <kbd>Ctrl + s</kbd>

If After Effects isn't the active window however, things are a little more complicated
- First this script will `WinSetTransparent` After Effects so that it becomes invisible
- Save the current project and wait for the save dialog box to disappear
- `WinMoveBottom` to force After Effects to the bottom making it no longer the active window
- Reactivate the originally active window
- Reset After Effects' transparency so the user can see it again if they tab back into it.

While doing it this way has the benefit of not forcing focus to After Effects (at least visibly to the user) and therefor not flashing it on the screen, it has the downside of seemingly randomly vanishing from view if After Effects is visible on the screen but not the active window.

After all of these steps have taken place the script will attempt to return focus to the originally active window and the user can resume their task almost as if nothing even happened.