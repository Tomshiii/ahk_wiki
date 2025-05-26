## <u>`settingsGUI()`</u>
This GUI allows the user to adjust almost all user adjustable settings all within one place. It can be accessed by either pressing the activation hotkey (<kbd>Win</kbd> + <kbd>F1</kbd> by default) or by right clicking on the `My Scripts.ahk` tray icon in the task bar, then selecting `Settings`

![image](https://github.com/user-attachments/assets/9de312d3-2d71-4d40-83d5-dc546b861e2c)

> *settingsGUI() as of v2.15.6*

## Options

### Toggle
- [ ] \> ***Check for Updates***  
Toggling this checkbox will allow for one of three options;
    - Script will check for updates and present the user with a GUI when an update is available
    - Script will check for updates but will only present a tooltip when an update is available
    - Script will not check for updates
> [!Note]
> This requires the user to use the `startup().updateChecker()` function
- [ ] \> ***Check for Pre-Releases***  
Determines whether checks for pre-release/beta updates will occur. These are rather infrequent/rare.
- [ ] \> ***Check for AHK Updates***  
Will determine whether the script will check for AHK version updates and will alert the user if one is available.
> [!Note]
> This requires the user to use the `startup().updateAHK()` function
- [ ] \> ***Check for Library Updates***  
Determines whether checks for new third party library files will occur. These files are found `..\lib\Other\`.  
It may be beneficial to disable this setting unless you are tracking file changes for the repo.
> [!Note]
> This requires the user to use the `startup().libUpdateCheck()` function
- [ ] \> ***Check for Package Updates***  
Whether the cmdline will be checked to see if *package* updates are available through the user's package manager of choice through the `startup().updatePackages()` function.

> [!Caution]
> This function is strictly designed around the `chocolatey` package manager and will likely require additional testing/code for other package managers.
- [ ] \> ***Check for Vers.ahk Updates***  
Checks for updates for the user's adobe `Vers.ahk`/`adobeVers.ahk` file so that they may select newer versions of adobe programs without needing to wait for a full release.

> [!Note]
> This requires the user to use the `startup().start.updateAdobeVerAHK()` function
- [ ] \> ***Adobe Version Override***  
Determines whether an attempt will be made to automatically set the currently installed versions of `Adobe Premiere Pro` & `Adobe After Effects`.

> [!Note]
> This setting requires the use of `startup().adobeVerOverride()`. This function will also only function correctly if only one year version of either program is installed at a time (ie. only a version from 2024 OR only 2023, etc. If multiple year versions are installed it will require the user to manually set the values within the `Editors` dropdown)

- [ ] \> ***Dark Mode***  
Toggles a few GUI dark mode options.

> [!Warning]
> Any GUIs will need to be recreated for this setting to take effect. This setting will also only affect GUIs created using `tomshiBasic`
- [ ] \> ***Disable Discord Reply Ping***  
Determines whether the use of `discord.button("DiscReply.png")` will identify and disable the `@` reply ping when replying to a message on discord.
- [ ] \> ***Run at Startup***  
Enabling this option will generate a shortcut of the current script in the user's `shell:startup` folder. If the user run's the script via another means (ie, `PC Startup.ahk`) then this option should be disabled and ignored.
- [ ] \> ***Show Adobe Versions at Startup***  
When enabled a `Notify {` window will appear at the top right of the user's screen to notify them which `Editors` versions they have selected for `Premiere Pro`, `After Effects` & `Photoshop`.
- [ ] \> ***Use Thio MButton***  
When enabled pressing <kbd>MButton</kbd> within `Windows Explorer` windows will offer a tooltip window to allow the user to instantly change the current window to the desired directory. Has special entries if `Premiere Pro` is open.

> [!Caution]
> The added `Premiere Pro` entries expect the user to be using my [premiere project folder tree](https://github.com/Tomshiii/ahk/blob/main/lib/Functions/SD%20Functions/genProjDirs.ahk)
***

- [ ] \> ***\`autosave.ahk\`***  
    - [ ] ***Always Save***  
    Enabling this setting will cause `autosave.ahk` to always try a save attempt. Disabling it will only attempt to save the active window.
    - [ ] ***Beep***  
    Enabling this setting will prompt the user with a little beep if it is attempting a save attempt but has halted from proceeding due to user input.
    - [ ] ***Check Mouse***  
    When enabled `autosave.ahk` will also wait for reduced mouse activity before proceeding with a save attempt.
    - [ ] ***Restart Playback***  
    Determines whether playback will be checked and resumed after a save attempt.
    - [ ] ***Save Override***  
    If enabled, manually saving will restart the `autosave.ahk` timer.

- [ ] \> ***\`checklist.ahk\`***  
    - [ ] ***Create Hotkey***  
    Determines whether a hotkey will be created using <kbd>Shift</kbd> + <kbd>Media Play/Pause</kbd>.
    - [ ] ***Tooltips***  
    Determines whether tooltips will be generated to alert the user that they have paused the timer.

- [ ] \> ***\`getTimeline()\` Always Check UIA***  
Determines whether all UIA values will be checked on first use or if they will be assumed correct.
    - [ ] ***Limit Daily***  
    Will limit this first time check to once per day if enabled. If disabled, every reload of the scripts will recheck UIA values on first use.
***
### Adjust
- [ ] \> ***\`adobeTemp()\` Limit (GB)***  
How large the user's definied [cache dir](https://github.com/Tomshiii/ahk/wiki/settingsGUI()#editors) can get before `startup().adobeTemp()` will clear it.
- [ ] \> ***\`adobe fullscreen check.ahk\` check rate (sec)***  
- [ ] \> ***\`autosave.ahk\` save rate (min)***  
- [ ] \> ***\`gameCheck.ahk\` check rate (sec)***  
- [ ] \> ***\`Multi-Instance Close.ahk\` check rate (sec)***  

### Editors
![image](https://github.com/user-attachments/assets/b6fb5bb3-1a2c-4206-b028-14ae8fb39799) ![image](https://github.com/user-attachments/assets/3841064e-fa6c-49b7-acd1-d57a2558641c)