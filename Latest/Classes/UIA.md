# <u>`class UIA {`</u>
This library is a wrapper for the UIAutomation framework, which can be used to automate windows that normally might be difficult or impossible to automate with AHK. This library is a third party library and is maintained by [Descolada](https://www.github.com/Descolada).

> To learn more about this library specifically, check out the repo: https://github.com/Descolada/UIA-v2/wiki

This library is currently included within the repo to enhance our abilities within `Premiere Pro` ***BUT*** with the addition of this tool comes a few caviates, including the potential removal of a `plug and play` experience. Some more things may now need to be setup by the user for my repo and its functions to perform as expected.

### <u>`class Premiere_UIA {`</u>
This script contains a miriad of classes that have been written to contain all variables the user may need to adjust to get their scripts working, but taking a quick look at those classes doesn't make it incredibly aparent as to what is going on, nor how to retrieve the information required.  
Within the class you will see variable declorations like so;
```c#
class v23_5 {
    timeline := "YvYY"
}
```
> There may be classes defined for multiple versions of Premiere within this script.

To explain the code snippet;  
First, I've designed the script to work off whatever version of `Premiere Pro` the user has set within `settingsGUI()` which is why the class name is a version number instead of something more descriptive (so make sure that is set correctly before proceeding).  
Then there are multiple variable declorations of a seemingly random string of characters. This string of characters is what defines the individual element we're looking to interact with, with the `UIA {` class.

### Known Quirks
While using this library to interact with Premiere is far more reliable and incredibly faster compared to using keyboard shortcuts and inbuilt ahk functions, it unfortuntely doesn't come without its quirks (that are usually Premieres fault more than anything). Here I will list any odd quirks I encounter alongside any potential ways to avoid the issue;
- These UIA values appears to change from version to version of Premiere as well as change depending on what your window layout within Premiere is set to (and as such may require some manual readjustment if the user ever changes their window layout).
- Depending on window layout, attempting to focus some panels more than once may result in an unrelated panel opening/stealing focus. As an example, in `v23.5` of Premiere with a certain layout, attempting to highlight some panels multiple times would pull up the `Capture` panel. This issue was unintentially mitigated shortly after experiencing it as I changed my window layout (for unrelated reasons). If you experience this issue, you may need to either adjust your window layout, or dig into some of the function code and ensure the window is only being focused once.

## How to retrieve these UIA strings
Once premiere is open, run the `..\lib\Other\UIA\UIA.ahk` script to get presented with a GUI.

![UIA GUI](https://github.com/Tomshiii/ahk/assets/53557479/de009f92-2ef0-4ca8-81ae-e953066c09cc)

Click the <kbd>Start Capturing (F1)</kbd> button in the bottom left corner. Then hover over a panel within Premiere until you see a blue outline around it. Once the correct panel is highlighted, wait until the `UIA Tree` column on the right side of the GUI gets populated with data.  
Once it populates, press <kbd>Esc</kbd>. Then press the <kbd>Show macro sidebar</kbd> button on the bottom right side of the GUI.

![Macro sidebar](https://github.com/Tomshiii/ahk/assets/53557479/668d84d2-6728-4127-9410-d6818282d3ca)

After ensuring that `SetFocus()` is selected within the `Action` dropdown list, click the <kbd>Add element</kbd> button.  
You should be presented with a few lines of code, something similar to;
```c#
AutoHotkeyEl := UIA.ElementFromHandle("[Program Information Here]")
AutoHotkeyEl.ElementFromPath("YvYY").Highlight()
```

You can ignore most of it and simply extract the string within the `ElementFromPath()` function. That string is the desired element you're looking for to fill out the information within my class. Repeat the process for all variables.