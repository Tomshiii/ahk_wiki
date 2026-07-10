`Keyboard Shortcut Adjustments` use to be a user maintained `.ini` file that would be read by my scripts and then generated into variables that my scripts could then reuse.  
Now that process is handled completely by my scripts and is automatically generated based off the user's currently set keyboard shortcuts (for `Premiere`, `After Effects`, and `Photoshop`). This elimates the need for the user to configure my repo to their setup and allows for a more seamless experience installing my repo.

***

## override.json
> Found: `A_MyDocuments \tomshi\KSA\override.json`

`override.json` allows the user to make adjustments to any hotkeys that either the system incorrectly determined, or if the user simply wishes for ahk to use another key combination. This file must retain `json` formatting.
Say for example we wanted to change the Premiere `effectControls` and `mediaBrowser` hotkeys;

```json
{
    "effectControls": {
        "hotkey": "^+3",
    },
    "mediaBrowser": {
        "hotkey": "^!p",
    }
}
```

Similarly; the user will need to use this `override.json` functionality to permanently adjust the hotkeys set in `resolve hotkeys.json`, and `windows hotkeys.json`

> [!Caution]
> `json` is very particular about its formatting. Ensure that;
> - All entries are separated by a `,`
> - There is no trailing `,` for the last entry
> - All values are wrapped in `"`
***

> [!Warning]
> Some important things to note:
> - It is recommended that `Core Functionality.ahk` is running to fully utilise `KSA`
> - Any custom keyboard shortcuts you add to the `.json` files in `A_AppData \tomshi\lib\KSA\json files\` WILL NOT get automatically added to future releases. There is not currently any method for the user to add their own KSA values outside of overriding them.
> - If you make an addition to `override.json` do note: because these values are only assigned to variables during runtime, you will need to reload all scripts before any changes to the file will take effect.