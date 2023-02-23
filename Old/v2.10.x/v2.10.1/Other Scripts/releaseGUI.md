This script is not one you will need during the normal operations of my scripts, it's run during the installation process of one of my releases and gives the user the ability to speed up the installation process of my repo.

It currently gives the user the option to;
- Generate a [SymLink](https://github.com/Tomshiii/ahk/wiki/CreateSymLink.ahk)
    - A symlink between `A_MyDocuments \AutoHotkey\Lib\` is necessary for my scripts to function. This option should only be selected if my repo is placed in it's final destination.
    - This option requires the script to be elevated as `cmd` needs to be run as admin to create a symlink
- Run [`HotkeyReplacer.ahk`](https://github.com/Tomshiii/ahk/wiki/Hotkey-Replacer.ahk)
- Run my scripts at PC startup by generating a shortcut between `..\PC Startup\PC Startup.ahk` & `C:\Users\A_UserName\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`

![image](https://user-images.githubusercontent.com/53557479/208209770-f9a2f343-565e-4972-a22b-c6848c27ef53.png)

> **`releaseGUI.ahk` as of v2.8.2*