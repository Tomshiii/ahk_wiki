# <u>`class UIA {`</u>

> [!Caution]
> This class **requires** correctly set `KSA.ini` values. Please read the [KSA](https://github.com/Tomshiii/ahk/wiki/Keyboard-Shortcut-Adjustments) wiki to learn more and set those values before proceeding.  
> It also requires the user to correctly set their `Premiere` version within `settingsGUI()`. Further instructions below.

This library is a wrapper for the UIAutomation framework, which can be used to automate windows that normally might be difficult or impossible to automate with AHK. This library is a third party library and is maintained by [Descolada](https://www.github.com/Descolada).

> [!Tip]
> To learn more about this library specifically, check out the repo: https://github.com/Descolada/UIA-v2/wiki

This library is currently included within the repo to enhance our abilities within `Premiere Pro` ***BUT*** with the addition of this tool comes a few caviates, including the potential removal of a more `plug and play` experience.
***

# <u>`class Premiere_UIA {`</u>
The class file itself (located `..\lib\Classes\Editors\Premiere_UIA.ahk`) contains code required to systematically parse a json file (located `..\Support Files\UIA\values.ini`) and turns each value for the currently set Premiere version into a class variable that other scripts can initialise and call on.

> [!Caution]
> For this system to work, the correct `Premiere Pro` version **MUST** be set in `settingsGUI()`.  
> While `Startup.adobeVerOverride()` should set this value for you (assuming you've set the correct `Year`/`Beta` value(s)), it's best to double check this value if you're ever encountering issues.  
> Once this value is correctly set and the user has selected `Save & Exit` it is recommended to restart all scripts for these changes to take effect.  
> ![image](https://github.com/Tomshiii/ahk/assets/53557479/c7f43f93-2018-4ea1-bad4-a5b631b41f09)

Once the correct version has been set, anytime the class is initialised it will check the `values.ini` file for the appropriate coordinates. If coordinates aren't set for the currently selected version, it will attempt to set them as long as Premiere is open.

> [!Tip]
> This process to automatically set the values can also be called apon at anytime by calling `premUIA_Values(false).__setNewVal()` (or by right clicking on `My Scripts.ahk` and selecting `Set Prem_UIA values`)

These UIA coordinates are then stored in the `values.ini` file (located `..\Support Files\UIA\values.ini`) and will look something like this;
```json
{
  "v24":{
    "effectsControl":"YY",
    "effectsPanel":"YuY",
    "programMon":"YrYYY",
    "timeline":"YwY",
    "tools":"YtY"
  },
  "v24_2_1":{
    "effectsControl":"YYY",
    "effectsPanel":"YuYY",
    "programMon":"YrYY",
    "timeline":"YwYY",
    "tools":"YtYY"
  },
}
```

In the example shown we have data for versions `24.0` and `24.2.1` of Premiere.  
If the user were to then open version `24.3` of Premiere and attempted to continue as usual, the class would automatically fall back to version `24.0` data (**NOT** `v24.2.1`) and as such may enounter a broken experience until new values are set.  
If the user were to instead open version `25.0` the class would automatically attempt to set new data.

Once values have been set in the `ini` file, the user can then initialise the class in their code by using;
```ahk
premUIA := premUIA_Values()
...
; premUIA.effectsControl == "YYY"
```

> [!Important]
> While the script will attempt to automatically set its data values, either when a version/base version isn't already set, or if the user calls `premUIA_Values(false).__setNewVal()`; it's important to note that this implementation is still rather rudimentary and is achieved by focusing the required Premiere panel and retrieving the UIA value of the current focused panel. As such, if a panel isn't already open, you may run into situations where the panel doesn't open fast enough for the script to grab its data.  
> If any panels aren't required for your workflow, consider removing the entries from the `windowHotkeys` Map found inside `premUIA_Values().__setNewVal()`

## Known Quirks
While using this library to interact with Premiere is far more reliable and incredibly faster compared to using keyboard shortcuts and inbuilt ahk functions, it unfortuntely doesn't come without its quirks (that are usually Premieres fault more than anything). Here I will list any odd quirks I encounter alongside any potential ways to avoid the issue;
- These UIA values appears to change from version to version of Premiere as well as change depending on what your window layout within Premiere is set to (and as such may require constant readjustment if the user ever changes their window layout, or if Premiere decides to change things from one day to the next).
- Depending on window layout, attempting to focus some panels more than once may result in an unrelated panel opening/stealing focus. As an example, in `v23.5` of Premiere with a certain layout, attempting to highlight some panels multiple times would pull up the `Capture` panel. This issue was unintentially mitigated shortly after experiencing it as I changed my window layout (for unrelated reasons). If you experience this issue, you may need to either adjust your window layout, or dig into some of the function code and ensure the window is only being focused once.

## How to manually retrieve these UIA strings
If calling `premUIA_Values(false).__setNewVal()` or selecting `Set Prem_UIA values` in `My Scripts.ahk`'s tray menu isn't working as expected, the user can manually set these values.  
Once premiere is open, run the `..\lib\Other\UIA\UIA.ahk` script to get presented with a GUI. (also open the `values.ini` file located `..\Support Files\UIA\values.ini`)

![UIA GUI](https://github.com/Tomshiii/ahk/assets/53557479/de009f92-2ef0-4ca8-81ae-e953066c09cc)

Click the <kbd>Start Capturing (F1)</kbd> button in the bottom left corner. Then hover over a panel within Premiere until you see a blue outline around it. Once the correct panel is highlighted, wait until the `UIA Tree` column on the right side of the GUI gets populated with data.  
Once it populates, press <kbd>Esc</kbd>. Then in the bottom left of the GUI you should see:

![UIA Path](https://github.com/Tomshiii/ahk/assets/53557479/c4dd2f46-8c64-417a-b39b-9439876ec33f)

You can either manually copy this variable, or right click on it and click `Copy UIA Path` as shown here:

![Copy UIA Path](https://github.com/Tomshiii/ahk/assets/53557479/8d25565c-94ea-4a9a-af0a-995c41d72c76)

Then place that value in the correct version json object (either the version of premiere you're currently using, eg. `v24_1` or just the base object `v24` as long as there isn't a property in a version above it that overrides it). Once completed save the file, restart all scripts to confirm your changes.

> [!Warning]
> Be careful when adding JSON values to not forget any `"` or `,`!  
> If any are missing you may run into some rather annoying issues.