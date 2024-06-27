Welcome to the documentation for Tomshi's ahk scripts!

These scripts are designed to make working within `Adobe Premiere Pro` and `Adobe After Effects` more optimised and efficient. They also contain a bunch of features to make navigating windows easier.

Due to to customisable nature of Adobe and a few inconsistencies between different instances of windows, my scripts are ***NOT*** plug and play and require a fair amount of initial setup before you can get going. Please be sure to read this page thoroughly as all steps need to be followed or you may run into issues.

***

<div align="center">

### ⚠️ Keep up to date ⚠️
[Known issues](https://github.com/users/Tomshiii/projects/2) and planned [features/changes](https://github.com/users/Tomshiii/projects/1) can be tracked from the [Projects](https://github.com/Tomshiii/ahk/projects?query=is%3Aopen) page.
</div>

***

### AHK Version Information:
This repo is to maintain work on the `ahk v2.0` versions of my scripts.
> [!Warning]
> These scripts *will not* work in `ahk v1.1`

***

### Installation
Checkout the [Installation Page](https://github.com/Tomshiii/ahk/wiki/Installation) for detailed instructions on how to install my repo.

***

This wiki contains documentation for just about everything relating to my scripts - feel free to poke around to get a better understanding of what they can do!

#### Just to be aware:
- If you wish to pick and choose scripts, or even try and move code out of my scripts to use elsewhere on your own, take note of any `#Includes` at the top of each script! They will tell you what other scripts the code might need to function correctly!
- This repo makes **heavy** use of `ImageSearch` and as such things *might* not work right out of the box. If you run into any issues with scripts just not finding their respective images, you may need to take your own screenshots and replace those within `..\Support Files\ImageSearch\`
- Any scripts that still contain pixel coordinates instead of using variables (in either, `Click`, `MouseMove`, `ImageSearch`, `PixelSearch`, etc) rely not only on my monitor layout or the `coordinate mode` set, but also my workspace layout within premiere (or any applicable program) and will not necessarily work out of the box. This wiki aims to rectify some of that concern but might not be perfect, don't be scared to look at the individual comments, as well as any accompanying AHK documentation (make sure you look at the ahk [v2.0](https://lexikos.github.io/v2/docs/AutoHotkey.htm) documentation and **NOT** the [v1.1](https://www.autohotkey.com/docs/AutoHotkey.htm) documentation) to get an idea of what is going on, then adjusting accordingly using `WindowSpy` which gets installed alongside AHK.
- All keyboard shortcuts within programs like Adobe Premiere/After Effects/OBS, etc that I need within a macro (eg. <kbd>^+5</kbd> to `highlight the media browser` within Premiere, or <kbd>d</kbd> for `select clip at playhead`) are definied within the [Keyboard Shortcuts.ini](https://github.com/Tomshiii/ahk/tree/main/Support%20Files/KSA) file instead of just sending the shortcut itself, which are then automatically assigned variables within the [Keyboard Shortcut Adjustments.ahk](https://github.com/Tomshiii/ahk/blob/main/lib/KSA/Keyboard%20Shortcut%20Adjustments.ahk) script that is then included in scripts that require those shortcuts. Edit shortcuts within `KSA.ini` with your own keyboard shortcuts (and reload any scripts that call those shortcuts) to get started!