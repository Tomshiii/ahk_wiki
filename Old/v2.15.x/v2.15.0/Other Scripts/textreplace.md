Within my repo you will find `textreplace.ahk`, this script is maintained in [another repo](https://github.com/Tomshiii/textreplace) and is included in this repo via a git submodule.

If you wish to always have the most up to date version of `textreplace.ahk` instead of using the version that comes alongside this repo;

- Clone the textreplace repo
- Change the `"textreplaceUser"` value in `ptf.ahk` from `this.SupportFiles "\textreplace\textreplace.ahk"` to your directory location
***

The main purpose of this script is to maintain a list of words that I have either mistyped before, or struggle with the spelling of.

![misspell](https://user-images.githubusercontent.com/53557479/203871181-9c11b709-0c5d-4110-bddb-15c5defb8415.gif)

> [!Note]
> `textreplace.ahk` is the only script that you need to run, the other scripts get `#Included` within `textreplace.ahk`

> [!Tip]
> If you wish to make your own additions to this list, by default the hotkey <kbd>#+h::</kbd> is setup to provide a handy GUI to do just that.
***
### Other Uses

This script isn't ***just*** a glorified spell check, it also contains a few little shortcuts to make typing out some of the common functions of my repo faster.

For example;
- Typing `toolc` and pressing `Tab` or `Space` will replace `toolc` with `tool.Cust("")` and move the cursor in between the two quotes
- Typing `toolf` results in `tool.Cust("",, 1)` and moves the cursor in between the two quotes
- Typing `toolw` results in `tool.Wait()`
- Typing `coords`, `coordw` or `coordc` results in; `coord.s()`, `coord.w()` & `coord.c()` respectively
- Typing `blockon` or `blockoff` results in; `block.On()` & `block.Off()`

![tooltip](https://user-images.githubusercontent.com/53557479/203871561-773d0cd3-022f-44f2-a8e7-156f3abc579f.gif)

On top of that it also helps speed up the process of adding `#Include` sections to scripts;

- All `class` libs can be easily added, either individually or all at once
    - `inc[class]` for the individual
    - `incclasses` for all of them

    ![classes](https://user-images.githubusercontent.com/53557479/203871810-48666a32-f9b3-4f4d-a05a-bdc823d48c09.gif)

- `KSA` can be added with `incksa`

> [!Tip]
> Check out `vscCompletions.ahk` to see if there are any more you can take advantage of!