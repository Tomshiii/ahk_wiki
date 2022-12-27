Welcome to the documentation for Tomshi's ahk scripts!

These scripts are designed to make working within `Adobe Premiere Pro` and `Adobe After Effects` more optimised and efficient. They also contain a bunch of features to make navigating windows easier.

### AHK Version Information:
This repo is to maintain work on the `ahk v2.0` versions of my scripts. These scripts **_will not_** work in `ahk v1.1`, the only versions of these scripts that will work with `ahk v1.1` are Releases [1.0](https://github.com/Tomshiii/ahk/releases/tag/v1.0)/[1.1](https://github.com/Tomshiii/ahk/releases/tag/v1.1)/[1.2](https://github.com/Tomshiii/ahk/releases/tag/v1.2) in this repo. They are _severely_ outdated, are practically missing everything found in the current versions of scripts, and those versions are no longer being maintained but you're free to try and backport any later additions if you're willing.
***

## Getting Started

> ### Before Getting Started
> My scripts rely on a `SymLink` to be created in the `A_MyDocuments \AutoHotkey\` folder that links back to `..\lib`. The install `.exe` can do this during the extraction process ***OR*** you can regenerate it manually (if you move my repo this also **MUST** be regenerated) by running [`..\Support Files\Release Assets\CreateSymLink.ahk`](https://github.com/Tomshiii/ahk/wiki/CreateSymLink.ahk). My scripts will fail to load if you do not do this.

> #### The Release Install `.exe`
> If you're a little unsure about running the install .exe (as you should be!) feel free to take a look at [`generateUpdate.ahk`](https://github.com/Tomshiii/ahk/blob/main/Support%20Files/Release%20Assets/generateUpdate.ahk) - this is the script I use to generate each release! As you'll be able to see within that script, I use a [7zip lib](https://github.com/thqby/ahk2_lib/blob/master/7Zip/SevenZip.ahk) from [thqby](https://github.com/thqby) to compress my entire repo into a `.zip` file, then I use the standard `ahk2exe` script that comes with AHK itself to compile a `.exe` of that `.zip` file alongside that same `7zip lib` to automatically unzip it once you install.
>> The install process will require either `7zip` to be installed, or `Powershell 5+` and `.Net4.5 (or greater)`. If the user does not have either installed, the install process will step through installing `PowerShell 7` and `.Net7`


1. Download and install [AHK v2.0](https://www.autohotkey.com/v2/).
1. Download and install either; (You could technically just edit scripts in notepad if you really wanted to, but I honestly don't recommend it)
   - [Notepad++](https://notepad-plus-plus.org/downloads/)
     - Then download and install the [ahk language for notepad++](https://www.autohotkey.com/boards/viewtopic.php?t=50)
   - [VSCode](https://code.visualstudio.com/)
     - Then install an AHK extension within the program for a more complete package.
    ###### **_It is recommended you use VSCode as a lot of my functions have dynamic comments that can be viewed across the entire program that could help you understand what is going on._**
1. Download these scripts by either checking out the latest [release](https://github.com/tomshiii/ahk/releases/latest) or by cloning the repo (in either VSCode or your git manager of choice), then save them wherever you wish.
    - Run the install `.exe` in the directory you wish my repo to be saved in to automatically generate the correct `SymLink` to the `Lib` folder (by selecting the option in the GUI that appears after extracting), else run [`..\Support Files\Release Assets\CreateSymLink.ahk`](https://github.com/Tomshiii/ahk/wiki/CreateSymLink.ahk) manually once you've moved my repo to it's final destination.
      - ###### **_You will need to rerun this script anytime you move my repo to regenerate the symlink_**
1. Take a look at [Keyboard Shortcuts.ini](https://github.com/Tomshiii/ahk/tree/main/lib/KSA) to set your own keyboard shortcuts for programs as well as define some coordinates for a few remaining imagesearches that cannot use variables for various reason, these `KSA` values are used to allow for easy adjustments instead of needing to dig through scripts!
1. Take a look at [ptf.ahk](https://github.com/Tomshiii/ahk/tree/main/lib/Classes/ptf.ahk) in the class `class ptf {` to adjust all assigned filepaths!
1. Run `My Scripts.ahk` to get started! (it's the main "hub" script and handles changing the root directory)
1. You can then edit and run any of the .ahk files to use to your liking!
    - ###### **_Although do note; some [`Streamdeck AHK`](https://github.com/Tomshiii/ahk/tree/main/Streamdeck%20AHK) scripts still have hard coded dir's as they are intended for my workflow and may error out if you try to run them from a different location. Most of these dir's can be adjusted in [`ptf.ahk`](https://github.com/Tomshiii/ahk/tree/main/lib/Classes/ptf.ahk)_**
1. Adjust the `PC Startup.ahk` file ***or*** create shortcuts to individual scripts in your startup folder (which can be accessed by pressed `win + r` and then typing in `shell:startup`)
    - If you don't have a secondary keyboard, don't forget to take a look through QMK Keyboard.ahk to see what functions you can pull out and put on other keys!
***

This wiki contains documentation for just about everything relating to my scripts - feel free to poke around to get a better understanding of what they can do!

#### Just to be aware:
- If you wish to pick and choose scripts, or even try and move code out of my scripts to use elsewhere on your own, take note of any `#Includes` at the top of each script! They will tell you what other scripts the code might need to function correctly!
- Any scripts that still contain pixel coordinates instead of using variables (in either, `Click`, `MouseMove`, `ImageSearch`, `PixelSearch`, etc) rely not only on my monitor layout or the `coordinate mode` set, but also my workspace layout within premiere (or any applicable program) and will not necessarily work out of the box. This wiki aims to rectify some of that concern but might not be perfect, don't be scared to look at the individual comments, as well as any accompanying AHK documentation (make sure you look at the ahk [v2.0](https://lexikos.github.io/v2/docs/AutoHotkey.htm) documentation and **NOT** the [v1.1](https://www.autohotkey.com/docs/AutoHotkey.htm) documentation) to get an idea of what is going on, then adjusting accordingly using `WindowSpy` which gets installed alongside AHK.
- All keyboard shortcuts within programs like Adobe Premiere/After Effects/OBS, etc that I need within a macro (eg. `^+5` to `highlight the media browser` within Premiere, or `d` for `select clip at playhead`) are definied within the [Keyboard Shortcuts.ini](https://github.com/Tomshiii/ahk/tree/main/lib/KSA) file instead of just sending the shortcut itself, which are then assigned variables within the [Keyboard Shortcut Adjustments.ahk](https://github.com/Tomshiii/ahk/blob/main/lib/KSA/Keyboard%20Shortcut%20Adjustments.ahk) script that is then included in other scripts. Edit that ini file with your own keyboard shortcuts (and assign any new values in the ahk script as well) to get things to work.