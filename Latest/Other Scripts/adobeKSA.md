> [!Warning]
> ***This script is not perfect***  
> The way adobe stores their hotkey values is a *mess* and ***incredibly difficult*** to parse. Some values retrieved may either be incorrect or simply skipped all together.  
> While this script is designed to speed up the process of starting with my scripts, I highly recommend NOT solely relying on this script and still double checking the values.  
> Please report any issues/errors on github and be sure to provide as much detail as possible!
***

`adobeKSA.ahk` is a script designed by me to parse through `KSA.ini` & the `Premiere Pro`/`After Effects` `keyboard shortcuts file` to automatically assign KSA values without the user needing to input them manually.

The adobe keyboard shortcut files are an absolute mess and both programs choose to store things differently which means both programs require separate code to achieve the same goal.  

#### `Premiere` 
Chooses to store its shortcuts in `xml` format converting the key values to some whacky concoction of decimal/hex goodness.   
For example; 
```xml
<item.6 Version="1">
    <commandname>cmd.timeline.nudge.down</commandname>
    <modifier.shift>false</modifier.shift>
    <modifier.alt>false</modifier.alt>
    <modifier.ctrl>true</modifier.ctrl>
    <virtualkey>2147483735</virtualkey>
</item.6>
```
is <kbd>Ctrl</kbd> + <kbd>w</kbd> ...  
just.. why...

> If you're ever wondering how to convert that virtualkey to an ahk hotkey try the following code
```ahk
virtualKey := 2147483735
val := SubStr((Format("{:x}", virtualKey)), -2)
return StrLower(Chr(Integer("0x" . val)))
```
> Be aware that not all hotkeys stored in Premiere's keyboard shortcut file will be laid out in this format, some keys may simply be one or two digits long.

#### `After Effects`
Meanwhile is closer to an `ini` formatted `.txt` file with everything written out as a giant string.  
For example; 
```ini
"SelectPreviousAdd" = "(Ctrl+Shift+UpArrow)"
```
***

These different processes pose their own difficulties and just add to the complexity of the overall project and add multiple points of failure to what should realistically be an easy task.