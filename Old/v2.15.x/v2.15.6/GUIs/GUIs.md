`..\lib\GUIs\` contains all GUI functions not defined within another function.

# <u>`class tomshiBasic {`</u>
`tomshiBasic` is a small class used to share a few settings across all GUIs in my scripts. This class helps me keep a relatively consistent GUI look across all my scripts, and in the event I want to ever change a setting it can be done here and be shared basically project wide.

> Using this gui will automatically do the following:
> - Generate an invisible button to steal focus away from any user generated controls
> - Set the titlebar to dark mode if enabled
> - Set all user generated buttons to dark mode if enabled
> - Set all drop down menus to dark mode if enabled
```c#
MyGui := tomshiBasic( [{FontSize, FontWeight, options, title}] )
```
#### FontSize
Type: Number
> Allows you to pass in a custom default GUI font size. Defaults to 11, can be omitted.

#### FontWeight
Type: Integer
> Allows you to pass in a custom default GUI font weight. Defaults to 500, can be omitted.

#### options
Type: String
> Allows you to pass in all GUI options that you would normally pass to a GUI. Can be omitted.

#### title
Type: String
> Allows you to pass in a title for the GUI. Can be omitted.
***

# <u>`class gameCheckGUI {`</u>

Within `settingsGUI()` is the ability to call another GUI, `gameCheckGUI` which is defined in a class in `..\lib\GUIs\gameCheckGUI.ahk` and can be accessed by pressing the `Add game to 'gameCheck.ahk'` menu option button within `settingsGUI()` or by right clicking on the `gameCheck.ahk` tray icon in the taskbar. This GUI is designed to allow the user to quickly add games to the `games.txt` file that is read by `gameCheck.ahk`. When the user opens `settingsGUI()` it grabs the `winTitle` and `winProcess` of the active window and stores that information, if the user then opens `gameCheckGUI()` that information is prefilled into the edit boxes so the user can edit it accordingly - if `gameCheckGUI` is called via the tray icon, that prefill information is generated then.

![image](https://user-images.githubusercontent.com/53557479/199131020-e705d0b8-0629-4391-8b1d-3540c4598b8f.png)

> *gameCheckGUI() as of v2.6.1*
***

## <u>`musicGUI()`</u>
This GUI offers the user a selection of audio programs at their fingertips. This function is used within [`switchToMusic()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions).

![image](https://user-images.githubusercontent.com/53557479/199143747-1ed038a3-b4ac-435e-9775-23f59eeca7c5.png)

> **musicGUI() as of v2.6.1*
***

## <u>`hotkeysGUI()`</u>
This function produces a GUI to remind the user of some helpful macros and their default hotkey combination.

![image](https://user-images.githubusercontent.com/53557479/199144856-6920ff9b-0c4b-4cb4-8ec1-13c5774e1eb1.png)

> *hotkeysGUI() as of v2.6.1*
***

## <u>`todoGUI()`</u>
This GUI is an informational GUI presented to the user as an option during their first time running `My Scripts.ahk` and is called from [`firstCheck()`](https://github.com/Tomshiii/ahk/wiki/Startup-Functions#firstcheck).

This GUI gives the user instructions on where to start with these scripts and is aimed at helping point the user in the right direction.

![image](https://user-images.githubusercontent.com/53557479/236603262-5053fb13-de1f-421b-a280-9a50cde8d0cc.png)

> *todoGUI() as of v2.11*
***

## <u>`activeScripts()`</u>
This GUI gives the user quick access to not only see which of my scripts are currently active, but also gives the user the ability to quickly close/open any of them at the click of a checkbox.

The scripts/checkboxes presented in this GUI are hard coded and not generated at runtime.

![image](https://user-images.githubusercontent.com/53557479/212584843-4379829b-2c9f-48d6-8807-a231c188cb6d.png)

> *activeScripts() as of v2.9.2*
***

# <u>`class trimGUI {`</u>
A class to encapsulate a GUI that allows the user to quickly and easily Trim a file using `ffmpeg`

![image](https://github.com/user-attachments/assets/495a746e-b589-435f-a733-d2ba173cca6c)


> *trimGUI as of v2.15.2*
***

# <u>`remapDrive.ahk`</u>
A GUI that allows the user to quickly and easily remap a network location to a drive.

![image](https://github.com/Tomshiii/ahk/assets/53557479/93343270-468e-4e62-8954-385ac02c33a6)

> *remapDrive.ahk as of v2.12.1*
***

# <u>`reencodeGUI.ahk`</u>


![image](https://github.com/Tomshiii/ahk/assets/53557479/0b04e54b-ea82-48cc-9aed-55129f9e6489)

> *reencodeGUI.ahk as of v2.14.2*
***

# <u>`enable unsigned extensions.ahk`</u>

![image](https://github.com/user-attachments/assets/f094432b-0883-49fd-bfc3-3ba609df6ce7)

> *enable unsigned extensions.ahk as of v2.14.12*
***

# <u>adjust audio.ahk</u>

![image](https://github.com/user-attachments/assets/21633053-66d0-4573-950d-2a0eff825f2c)

> *adjust audio.ahk as of v2.15.3*
***

# <u>multi-dl.ahk</u>
<img src="https://github.com/user-attachments/assets/a566fb13-945d-4e0c-8b80-dc5c6fb116ad" width="320"/>
<img src="https://github.com/user-attachments/assets/1e790869-0aa2-4cb1-9bd3-1e8e32ed09c4" width="320"/>
<img src="https://github.com/user-attachments/assets/a541d369-b3a6-49d8-b3b0-dee5cd9be87c" width="320"/>

> *multi-dl.ahk as of v2.15.5*

- [ ] ***check dev branch***
> Enabling this checkbox will instruct the **compiled** version of this script to optionally check the dev branch for any updates instead of only checking the main branch. Enabling it for the .ahk script will have no effect as it does not look for updates to itself as later changes to my `yt-dlp.ahk` or `ffmpeg.ahk` may also be required.

- [ ] ***avoid reencode***
> Enabling this checkbox will make `yt-dlp` only download `h264` or `h265` codecs, this will skip the usual required reencoding step - however due to youtube only storing lower quality versions of videos in these formats, this option will likely result in lower quality *(and is usually capped at 1080p)*.
***