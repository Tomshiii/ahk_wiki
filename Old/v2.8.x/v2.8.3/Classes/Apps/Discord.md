This script contains a class called `Discord` and encompasses all functions I use to manpulate discord.

All functions within this classed are called like: `discord.func()`
***

## `button()`
This function uses an imagesearch to look for buttons within the right click context menu to perform various tasks.

This function has code so that, if the `button` variable, is `DiscReply.png`, will find and disable the `@ping`
```
discord.button( [button] )
```
#### *button*
Type: *String - Filename*
> This parameter is the full filename of the button of choice. ie. `DiscEdit.png` or `DiscReply.png`. Will require screenshots of said property in the appropriate ImageSearch folder.

***
## `discord.Unread()`
This function will search for and automatically click on either unread servers or unread channels depending on which image you feed into the function.
```
discord.Unread( [which] )
```
#### *which*
Type: *Integer*
> If you feed in nothing it will search for the first unread server and click it. If you feed in `2` it will search for the first unread channel and click on it. Will require screenshots of said property in the appropriate ImageSearch folder.