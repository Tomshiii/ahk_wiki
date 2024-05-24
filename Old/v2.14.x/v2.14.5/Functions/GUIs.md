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

## <u>`settingsGUI()`</u>
This GUI allows the user to adjust almost all user adjustable settings all within one place. It can be accessed by either pressing the activation hotkey (<kbd>Win</kbd> + <kbd>F1</kbd> by default) or by right clicking on the `My Scripts.ahk` tray icon in the task bar, then selecting `Settings`

![image](https://github.com/Tomshiii/ahk/assets/53557479/157713ab-ab88-4d9f-82ab-640f3f5b9dc2)

> **settingsGUI() as of v2.14*

# <u>`class gameCheckGUI {`</u>

Within `settingsGUI()` is the ability to call another GUI, `gameCheckGUI` which is defined in a class in `..\lib\GUIs\gameCheckGUI.ahk` and can be accessed by pressing the `Add game to 'gameCheck.ahk'` menu option button within `settingsGUI()` or by right clicking on the `gameCheck.ahk` tray icon in the taskbar. This GUI is designed to allow the user to quickly add games to the `Game List.ahk` file that is read by `gameCheck.ahk`. When the user opens `settingsGUI()` it grabs the `winTitle` and `winProcess` of the active window and stores that information, if the user then opens `gameCheckGUI()` that information is prefilled into the edit boxes so the user can edit it accordingly - if `gameCheckGUI` is called via the tray icon, that prefill information is generated then.

![image](https://user-images.githubusercontent.com/53557479/199131020-e705d0b8-0629-4391-8b1d-3540c4598b8f.png)

> **gameCheckGUI() as of v2.6.1*
***

## <u>`musicGUI()`</u>
This GUI offers the user a selection of audio programs at their fingertips. This function is used within [`switchToMusic()`](https://github.com/Tomshiii/ahk/wiki/switchTo-Functions).

![image](https://user-images.githubusercontent.com/53557479/199143747-1ed038a3-b4ac-435e-9775-23f59eeca7c5.png)

> **musicGUI() as of v2.6.1*
***

## <u>`hotkeysGUI()`</u>
This function produces a GUI to remind the user of some helpful macros and their default hotkey combination.

![image](https://user-images.githubusercontent.com/53557479/199144856-6920ff9b-0c4b-4cb4-8ec1-13c5774e1eb1.png)

> **hotkeysGUI() as of v2.6.1*
***

## <u>`todoGUI()`</u>
This GUI is an informational GUI presented to the user as an option during their first time running `My Scripts.ahk` and is called from [`firstCheck()`](https://github.com/Tomshiii/ahk/wiki/Startup-Functions#firstcheck).

This GUI gives the user instructions on where to start with these scripts and is aimed at helping point the user in the right direction.

![image](https://user-images.githubusercontent.com/53557479/236603262-5053fb13-de1f-421b-a280-9a50cde8d0cc.png)

> **todoGUI() as of v2.11*
***

## <u>`activeScripts()`</u>
This GUI gives the user quick access to not only see which of my scripts are currently active, but also gives the user the ability to quickly close/open any of them at the click of a checkbox.

The scripts/checkboxes presented in this GUI are hard coded and not generated at runtime.

![image](https://user-images.githubusercontent.com/53557479/212584843-4379829b-2c9f-48d6-8807-a231c188cb6d.png)

> **activeScripts() as of v2.9.2*
***

# <u>`class trimGUI {`</u>
A class to encapsulate a GUI that allows the user to quickly and easily Trim a file using `ffmpeg`

![image](https://github.com/Tomshiii/ahk/assets/53557479/7baa2f87-b145-410d-88af-53b801a22b31)


> **trimGUI as of v2.12.1*
***

# <u>`remapDrive.ahk`</u>
A GUI that allows the user to quickly and easily remap a network location to a drive.

![image](https://github.com/Tomshiii/ahk/assets/53557479/93343270-468e-4e62-8954-385ac02c33a6)

> **remapDrive.ahk as of v2.12.1*
***

# <u>`reencodeGUI.ahk`</u>


![image](https://github.com/Tomshiii/ahk/assets/53557479/0b04e54b-ea82-48cc-9aed-55129f9e6489)

> **reencodeGUI.ahk as of v2.14.2*