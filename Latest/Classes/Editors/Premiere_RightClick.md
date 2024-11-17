> ### *This script only gets constantly tested on the version of Premiere Pro listed at the top of the `prem {` class in my repo*.
>  - ##### It *should* work on most versions beyond at least v22.3.1 but development on those versions is not active nor verified

> [!Warning]
> This script **_may not_** always function correctly if multiple sequences are open and the user isn't using [PremiereRemote](https://github.com/Tomshiii/ahk/wiki/PremiereRemote).  
> Unfortunately, attempting to highlight the timeline while it's already active will cycle through sequences. The script uses multiple methods to focus the timeline without this occurring but sometimes Premiere can just act up.  
>
> This function also makes use of `WinEvent {` by `Descolada` to avoid some of these edge cases. Ideally you'll never come across any of them, but this is simply a warning that it *can* occur.

> [!Caution]
> This script is very particular about where it's placed within other scripts. Other mouse scripts can interfere with it causing issues. Take note of where I have placed it within `My Scripts.ahk` for reference ⚠️
***

> ❗*This script also requires you to:* ❗
> - Properly set the colour values within the script if you don't use the default dark mode for Premiere Pro (or use a different version as Adobe is constantly slightly tweaking things)
> - Properly set all KSA values the script uses (all variables that start with `KSA.x` need to be set within `Keyboard Shortcuts.ini`)
>   - Those `KSA` values need to correctly correspond to keyboard shortcuts set within `Premiere`
> - Properly set all `Premiere_UIA.ahk` values correctly. Check [UIA](https://github.com/Tomshiii/ahk/wiki/UIA) for more details.
> - For proper functionality:
>    - Set `Preferences > Timeline > Timeline Playback Auto-Scrolling` within Premiere to `No Scroll`
>    - Ensure `Play In to Out with Preroll/Postroll` **_isn't_** set to <kbd>Shift + Space</kbd> (which it **_is_** by default) if you use <kbd>Shift + anything</kbd> for hotkeys like `Ripple Delete`. Not doing so won't break this script in any way, it just makes your timeline navigation infinitely less annoying. Setting <kbd>Shift + Space</kbd> to `Play-Stop Toggle` is my preferred hotkey to avoid Premiere not being able to keep up with the flow of inputs properly.
>
> - For increased reliability:
>   - Consider installing [PremiereRemote](https://github.com/Tomshiii/ahk/wiki/PremiereRemote).

> For a version of this script that **doesn't** use UIA. Take a look at the script [here](https://github.com/Tomshiii/ahk/blob/v2.11.3/lib/Classes/Editors/Premiere_RightClick.ahk). Just be aware that this version is an older version and as such may be missing future bug fixes/features.
***

## <u>`rbuttonPrem.movePlayhead()`</u>
This is the class method intended to be called by the user, it handles moving the playhead to the cursor when an activation key is pressed (mainly designed for <kbd>RButton</kbd> & <kbd>XButton1</kbd>).
> [!Note]
> This function has built in checks for <kbd>LButton</kbd> & <kbd>XButton2</kbd> during activation

> [!Note]
> This function should work as intended on both the old UI and the Spectrum UI assuming you use the default darkest themeing for both UI versions. Other themes will require the user to add additional colour values to `timelineColours {`

```c#
rbuttonPrem().movePlayhead( [{allChecks := true, theme := "darkest", version := unset, sendOnFailure := unset}] )
```

#### *allChecks*
Type: *Boolean*
> Determines whether the user wishes for the function to make the necessary checks to determine if the cursor is hovering an empty track on the timeline. Setting this value to false allows the function to move the playhead regardless of where on the timeline the cursor is situated.

> [!Caution]
> It is not recommended to use this value if your activation hotkey is something like <kbd>RButton</kbd> as that removes the ability for the keys native function to operate.

#### *theme*
Type: *String*
> The desired theme the user uses and wishes to use for the required colour values. Currently only "darkest" has mapped values.

#### *version*
Type: *String*
> The currently selected version of premiere within `settingsGUI()`. This parameter can usually be filled in using `prem.currentSetVer`

#### *sendOnFailure*
Type: *String*
> What you wish for the script to send in the event that it needs to fallback. What you set for this parameter will be sent to `SendInput()`. If left unset, sends `"{" A_ThisHotkey "}"`
***

The initial idea to do this was thought up by [TaranVH](https://github.com/TaranVH/2nd-keyboard) a previous editor for LTT. I have since *heavily* edited it to be more useful for myself.
***
The most important/frequent thing you do while video editing is moving around on the timeline. Ideally you want this to be fast, functional and most of all, accurate. This script aims to do all three.

The biggest bottleneck with timeline navigation is always manipulating the playhead (that's the blue line that runs vertical on the screen to signify what frame of footage you're looking at). By default in Premiere, the only ways to move the playhead are;

- Moving the mouse to it, being in the exact right position so the cursor will change and then you can grab it with a left click on the mouse.
- Moving the mouse to the top of the timeline where it shows a lined timecode and left clicking on it to move the playhead to the cursor position.

These methods are fine, but they're slow and awkward - they require too much movement from the user before anything can happen. It might not seem like that big of a deal by itself but overtime these wasted movements add up.

This script takes advantage of a wonderful hotkey within Premiere Pro, `move playhead to cursor`. This hotkey is an absolute game changer and is the only reason this script is so powerful. With it we can create a loop that occurs while the user holds down another button (<kbd>RButton</kbd> by default) that will warp the playhead to the cursor position at the click of a mouse button! awesome!

But that wasn't enough for me, I wanted to manipulate playback even further. I often watch footage in 2x speed to work faster so letting go of <kbd>RButton</kbd> to then either press <kbd>Space + l</kbd> to get to 2x speed or double tap <kbd>l</kbd> was moving my hands around way too much, way too often and wasting a tonne of time (as well as making them sore). So with this in mind I added functionality to this script so that;

- If the user presses the <kbd>LButton</kbd> while holding <kbd>RButton</kbd> and the loop is active, once the user lets go of <kbd>RButton</kbd> the script would automatically restart playback on the timeline
- If the user presses <kbd>XButton2</kbd> while holding <kbd>RButton</kbd> and the loop is active, once the user lets go of <kbd>RButton</kbd> the script would automatically restart playback on the timeline at 2x speed

Awesome!

As I have premiere set to not follow the playhead during playback (if the playhead moves off my screen during playback, the timeline WON'T warp to it to make sure it's always on screen) I also added functionality to check to see if the playhead is on the screen before starting the loop. If the playhead IS on the screen, it will pause playback first, if the playhead ISN'T on screen, it won't. This stops the timeline from warping all over the place after attempting to move the playhead.

> [!Note]
> Now that label colours can be adjusted by the user, it is recommended to NOT use the colour of the playhead as a label colour