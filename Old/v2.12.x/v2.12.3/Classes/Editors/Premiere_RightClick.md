> ### *This script only gets tested on v22.3.1 of Premiere Pro*.
>  - ##### It *should* work on v23.1+ but development on those versions is not active

> ⚠️ This script **_may not_** function correctly if multiple sequences are open. Unfortunately, attempting to highlight the timeline while it's already active will cycle through sequences. The script will do a pixel search at some of the stored coordinates of the timeline and check for the focus outline to determine if this timeline focusing is required - this *should* mitigate this issue under most cicumstances, but in the event out outlier event occurs, this issue can be somewhat mitigated by toggling whether the function focuses the timeline by calling `prem().__toggleTimelineFocus()`. This particular solution isn't perfect and makes the function somewhat weaker, but can help when keeping multiple sequences open is necessary and you're running into those edge cases. ⚠️

> ⚠️ This script is very particular about where it's placed within other scripts. Other mouse scripts can interfere with it causing issues. Take note of where I have placed it within `My Scripts.ahk` for reference ⚠️
***

> ❗*This script also requires you to:* ❗
> - Properly set the colour values within the script if you don't use the default dark more for Premiere Pro
> - Properly set all KSA values the script uses (all variables that start with `KSA.x` need to be set within `Keyboard Shortcuts.ini`)
>   - Those `KSA` values need to correctly correspond to keyboard shortcuts set within `Premiere`
> - For proper functionality:
>    - Set `Preferences > Timeline > Timeline Playback Auto-Scrolling` within Premiere to `No Scroll`
>    - Ensure `Play In to Out with Preroll/Postroll` **_isn't_** set to <kbd>Shift + Space</kbd> if you use <kbd>Shift + anything</kbd> for hotkeys like `Ripple Delete`. Not doing so won't break this script in any way, it just makes your timeline navigation infinitely less annoying. Setting <kbd>Shift + Space</kbd> to `Play-Stop Toggle` is my preferred hotkey.

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

As I have premiere set to not follow the playhead during playback (if the playhead moves off my screen during playback, the timeline WON'T warp to it to make sure it's always on screen) I also added functionality to check to see if the playhead is on the screen before starting the warp. If the playhead IS on the screen, it will pause playback first, if the playhead ISN'T on screen, it won't. This stops the timeline from warping all over the place after attempting to move the playhead.