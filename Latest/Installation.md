# Steps to Install

## <u>Prerequisites</u>
- Download and install [AHK v2.0](https://www.autohotkey.com/v2/).
- Download the [latest release](https://github.com/Tomshiii/ahk/releases)
- Download and install either;
   - [Notepad++](https://notepad-plus-plus.org/downloads/)
     - Then download and install the [ahk language for notepad++](https://www.autohotkey.com/boards/viewtopic.php?t=50)
   - [VSCode](https://code.visualstudio.com/)
     - Then install an AHK extension by `thqby` within the program for a more complete package.

## <u>Installation</u>
Once you've followed the steps above, simply run the release `.exe` and follow the onscreen instructions.  
Once you have selected your desired installation directory, be aware the that the installation process will create a new folder in the given directory called `Tomshi AHK` that the installation will take place in.
> [!Warning]
> Please wait patiently, the extraction process may take a moment as it extracts the release.

> If you're a little unsure about running the install `.exe` (as you should be!) feel free to take a look at [`generateUpdate.ahk`](https://github.com/Tomshiii/ahk/blob/main/Support%20Files/Release%20Assets/generateUpdate.ahk) - this is the script I use to generate each release!  
> As you'll be able to see within that script, I use a (now depreciated) [7zip lib](https://github.com/thqby/ahk2_lib/blob/b2c3d1025527cb68b92cd8642b6312a06890fb03/7Zip/SevenZip.ahk) from [thqby](https://github.com/thqby) to compress my entire repo into a `.zip` file, then I use the standard `ahk2exe` script that comes with AHK itself to compile a `.exe` of that `.zip` file alongside the installation GUI you see when you run the `.exe`.
- During the installation process all necessary `SymLinks` will be automatically generated.
- Once the process has completed you'll be met with another GUI that will offer additional installs;

![image](https://github.com/Tomshiii/ahk/assets/53557479/66132612-443b-47a7-957b-cda87af99f35)

- [PremiereRemote](https://github.com/Tomshiii/ahk/wiki/PremiereRemote) can be installed to make some functions faster/more reliable.
>[!Note]
> *However; [NodeJS](https://nodejs.org/en) must already be installed by the user.*  
> If you have a [package manager](https://github.com/Tomshiii/ahk/wiki/Install-Package-Manager) installed, you should be able to also install it through that.  
> *(ie. `choco install nodejs`)*

***
#### With that my repo is essentially *"installed"*. But there are a few more steps that can be taken to customise some scripts to your own workflow.
- Look through [`..\lib\Classes\ptf.ahk`](https://github.com/Tomshiii/ahk/blob/main/lib/Classes/ptf.ahk) for any directories that may not line up with your own setup
    - If you create your own version of `My Scripts.ahk` (and name it something else), ensure you use the `startup {` function `startup.generate()` (see `My Scripts.ahk` to see how to use these startup functions in your own scripts) a `MainScriptName` variable will then be tracked in `settings.ini`. This value is used across a number of scripts for many different reasons.
- If you intend on using any of the `Streamdeck Scripts`, ensure you checkout `..\Support Files\Streamdeck Files\options.ini`
    - ###### **_Although do note; some [`Streamdeck AHK`](https://github.com/Tomshiii/ahk/tree/main/Streamdeck%20AHK) scripts still have hard coded dir's as they are intended for my workflow and may error out if you try to run them from a different location. Most of these dir's can be adjusted in [`ptf.ahk`](https://github.com/Tomshiii/ahk/tree/main/lib/Classes/ptf.ahk)_**
- If you intend on using any of my `Premiere Pro` functions, checkout the section down below
- Adjust the `PC Startup.ahk` file ***or*** create shortcuts to individual scripts in your startup folder (which can be accessed by pressed <kbd>win + r</kbd> and then typing in `shell:startup`)
    - If you don't have a secondary keyboard, don't forget to take a look through QMK Keyboard.ahk to see what functions you can pull out and put on other keys!

#### If you're cloning my repo **OR** something during the installation process goes wrong
- Run `..\Support Files\Release Assets\baselineSettings.ahk` to ensure a `settings.ini` file is properly generated.
- Check `..\Support Files\Release Assets\adobeVers.ahk` to make sure you have the latest versions listed & then run `..\Support Files\Release Assets\generateAdobeSym.ahk`
- Run [`..\Support Files\Release Assets\CreateSymLink.ahk`](https://github.com/Tomshiii/ahk/wiki/CreateSymLink.ahk) manually.
    - ###### **_You will need to rerun this script anytime you move my repo to regenerate the symlink. It is recommended you first follow steps in an above dot point and check/clear adobe SymLinks_**

***
### ⚠️ Premiere Pro ⚠️
- First, ensure you checkout `..\Support Files\KSA\Keyboard Shortcuts.ini` to set any keyboard shortcuts you use so my scripts will send the correct keystrokes
- Then, if you intend on using my repo for my `Premiere Pro` functions there is a little bit of manual setup required of the user. My repo makes use of the [UIA](https://github.com/Tomshiii/ahk/wiki/UIA) lib to interact with some sections of Premiere. Unfortunately though, some of the information required tends to change depending on a few factors.  
It is **required** that the user reads that wiki page and sets the necessary values for themselves or some of my functions will not behave as expected.
> [!Tip]
> Checkout the [PremiereRemote](https://github.com/Tomshiii/ahk/wiki/PremiereRemote) wiki page for more info.

***

# <u>Updating</u>
Updating my repo can sometimes be a little confusing, especially once you've started to adjust things to suite your setup. I try to make a concious effort to separate user settings from common files but sometimes it can be rather easy to accidentally mesh the two together.  
On top of this, as this is a constantly evolving repo, things may change at the drop of a hat which can quickly throw previous steps out the window.

Updating your own install of my repo with a new version will as a result probably always be a bit of a manual task for the user, so for the most part if you aren't experiencing any issues, it's best not to update unless something new really catches your eye.

In that event, the easiest method is probably to create a backup of your current installation, then delete the repo and install the new version using the steps above.

Assuming you haven't heavily modified any lib files, some files you may need to to transfer data from may include;
- `..\lib\Classes\ptf.ahk`
- Be mindful of the `MainScriptName` variable in `settings.ini` if you've decided to create your own version of `My Scripts.ahk` and have named it something else. The user will need to use `startup().generate()` in their own custom script for this value to be set automatically
- Any pixel values at the top of `..\lib\Classes\Apps\Discord.ahk`
- `..\Support Files\UIA\values.ini`
- `..\Support Files\Streamdeck Files\options.ini`
- `..\Support Files\KSA\Keyboard Shortcuts.ini`

Keep in mind that simply replacing new files with your old copies may cause issues if new entries are added, as that would inadvertently wipe any new values.

> [!Caution]
> It is **NOT** recommended to run the installer over a previous installation of my repo. It is not designed to do so (and should prevent the user from doing so) and will likely break or cause issues if it manages to move forward.