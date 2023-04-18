This script is not one you will need during the normal operations of my scripts, it's run during the installation process of one of my releases and gives the user the ability to speed up the installation process of my repo.

It currently gives the user the option to;
- Generate a [SymLink](https://github.com/Tomshiii/ahk/wiki/CreateSymLink.ahk)
    - A symlink between `A_MyDocuments \AutoHotkey\Lib\` is necessary for my scripts to function. This option should only be selected if my repo is placed in it's final destination.
    - This option requires the script to be elevated as `cmd` needs to be run as admin to create a symlink
- Run [`HotkeyReplacer.ahk`](https://github.com/Tomshiii/ahk/wiki/Hotkey-Replacer.ahk)
- Run my scripts at PC startup by generating a shortcut between `..\PC Startup\PC Startup.ahk` & `C:\Users\A_UserName\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`
- Run `adobeKSA.ahk` to parse through the user's `Premiere` & `After Effects` keyboard shortcut file and automatically assign their shortcuts to `KSA.ini` values
    > Learn more about [adobeKSA.ahk here](https://github.com/Tomshiii/ahk/wiki/adobeKSA.ahk)

![image](https://user-images.githubusercontent.com/53557479/232787558-6778fad7-f4ec-4e5f-996d-9a6249638088.png)

> **`releaseGUI.ahk` as of v2.11*