> [!Warning]
> This script is disabled on release versions of my scripts greater than `v2.13.0` as that version contained breaking changes in how the `My Scripts.ahk` file is laid out. This script is planned to one day be rewritten to accommodate those changes but no rodemap has been laid out at current.

This script is not one you will need during usual interactions with my scripts and is instead designed to help ease you through transitioning to a new release.

I'm under no assumption that you'll want to keep my hotkeys for yourself, quite the opposite, I more than expect you to change them all up. This script is designed to go through `My Scripts.ahk` & `KSA.ini` and replace my default values with the ones you've replaced them with in your own instances of my scripts!

The way it does this:
#### My Scripts.ahk
Searches for the `;xHotkey;` tags above every defined hotkey, stores them within a `Map` and then searches for them within the release and replaces the hotkey with the users value
#### KSA.ini
`StrSplit`'s the entire `.ini` file and appends each key/value pair to a map. This map is then used to replace the release `KSA.ini` with the user's values 
> This is why the user cannot use `=` as a hotkey within `KSA.ini`. `=` is used as the delimiter for `StrSplit` - if the user used `=` within a hotkey it would break the `Map` generation and KSA would silently fail without the user knowing.

> [!Note]
> This script will not replace new tags you add yourself and can't replace any custom code you've added yourself. This script will also require `CreateSymLink.ahk` to have been run successfully.


![image](https://user-images.githubusercontent.com/53557479/213868218-944ac1b6-3621-4beb-a468-dfdece97a50d.png)

> *`Hotkey Replacer.ahk` as of v2.10*