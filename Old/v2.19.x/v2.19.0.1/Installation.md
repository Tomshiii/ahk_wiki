# Steps to Install

## <u>Prerequisites</u>
> [!Warning]
> `nodejs` & `PremiereRemote` are both **requirements** for my repo's functionality. As of `Release v2.18.0` they will both be installed alongside my repo.

- Download and install [AHK v2.0](https://www.autohotkey.com/v2/).
- Download the [latest release](https://github.com/Tomshiii/ahk/releases)
- Download and install either;
   - [Notepad++](https://notepad-plus-plus.org/downloads/)
     - Then download and install the [ahk language for notepad++](https://www.autohotkey.com/boards/viewtopic.php?t=50)
   - [VSCode](https://code.visualstudio.com/)
     - Then install an AHK extension by `thqby` within the program for a more complete package.

## <u>Installation</u>
Once you've followed the steps above, simply run the release `.exe` and follow the onscreen instructions.  
> [!Warning]
> Please wait patiently, the extraction process may take a moment as it extracts the release.

> [!tip]
> If you're a little unsure about running the install `.exe` (as you should be!) feel free to take a look at [`generateUpdate.ahk`](https://github.com/Tomshiii/ahk/blob/main/Support%20Files/Release%20Assets/generateUpdate.ahk) - this is the script I use to generate each release!  
> As you'll be able to see within that script, I use a (now depreciated) [7zip lib](https://github.com/thqby/ahk2_lib/blob/b2c3d1025527cb68b92cd8642b6312a06890fb03/7Zip/SevenZip.ahk) from [thqby](https://github.com/thqby) to compress my entire repo into a `.zip` file, then I use the standard `ahk2exe` script that comes with AHK itself to compile a `.exe` of that `.zip` file alongside the installation GUI you see when you run the `.exe`.

***
To use any of my classes/functions in your own scripts you can add them like so;
```ahk
#Include '%A_Appdata%\tomshi\lib'
#Include Classes\[script.ahk]
#Include Functions\[script.ahk]
```
> [!Note]
> If you use any scripts that require `Core Functionality.ahk` in any way, you must ensure `Core Functionality.ahk` is open and fully loaded before any of those scripts are run

> [!Caution]
> - Do not store any of your own scripts in the directory you selected to install my repo, that folder may be wiped during any update processes and no backups will be created prior. You **may** lose anything you store in there.
> - If you are using any of my scripts in your own workflow, it is recommended that you always ensure `Core Functionality.ahk` is run before any other script that calls anything from my repo. This can be achieved by following a similar layout to the scripts in `..\PC Startup\`. During installation `Initialise.ahk` has a shortcut created in `shell:startup` to run on pc startup and should launch `Core Functionality.ahk`, but if you don't follow the examples and ensure your own scripts run after this one you may run into some errors.