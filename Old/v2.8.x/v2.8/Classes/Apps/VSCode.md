This script contains a class called `vscode` and encompasses all functions I use to manpulate discord.

All functions within this classed are called like: `vscode.func()`
***

## `vscode.script()`
A function to quickly naviate between files in VSCode.

As this function is designed for my repo, it has code so that, if the second activation key is the `function hotkey` (as defined in KSA), it will do extra things to expand that folder.

For this script to work [explorer.autoReveal] must be set to `false` in VSCode's settings (File->Preferences->Settings, search for "explorer" and set "explorer.autoReveal")
```
vscode.script( [script] )
```
#### *script*
Type: *Integer*
> This parameter is the amount of down inputs the script needs to input to get to the required script. Will default to 0.
***

## `vscode.search()`
I have a habit of always trying to `^f` in the explorer window instead of the code window so this function ensures that the code window is in focus.

**This macro REQUIRES `editor.emptySelectionClipboard` to be set to false within VSCode*
***

## `vscode.cut()`
This function is only required because the above function requires `editor.emptySelectionClipboard` to be set to `false`.

This function recreates the default ability of `VSCode` to completely remove a line by pressing `^x`
***

## `vscode.copy()`
This function is only required because the above function requires `editor.emptySelectionClipboard` to be set to `false`.

This function recreates the default ability of `VSCode` to copy a line by pressing `^c`