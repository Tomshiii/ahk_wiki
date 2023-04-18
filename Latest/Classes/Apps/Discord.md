This script contains a class called `Discord` and encompasses all functions I use to manpulate discord.

All functions within this classed are called like: `discord.func()`
***

## <u>`button()`</u>
This function uses an imagesearch to look for buttons within the right click context menu to perform various tasks.

This function is constantly being broken as discord updates their logo/the @ reply ping button. When this happens you can try taking new screenshots to see if that fixes the issue.

This function may encounter different behaviours depending on the orientation of the monitor that it's on/the resolution. It hasn't been tested on anything higher than a `1440p` monitor.

> ###### This function has code so that, if the `button` variable, is `DiscReply.png`, will find and disable the `@ON ping`
> ###### This function includes specific code for the delete button and requires the passed parameter to be `DiscDelete.png`. It will delete the message without the usual prompt while <kbd>Shift</kbd> is held
```c#
discord.button( [button] )
```
#### *button*
Type: *String - Filename*
> This parameter is the full filename of the button of choice. ie. `DiscEdit.png` or `DiscReply.png`. Will require screenshots of said property in the appropriate ImageSearch folder.

***

## <u>`Unread()`</u>
This function will search for and automatically click on either unread servers or unread channels depending on which image you feed into the function.
```c#
discord.Unread( [which] )
```
#### *which*
Type: *Integer*
> If you feed in nothing it will search for the first unread server and click it. If you feed in `2` it will search for the first unread channel and click on it. Will require screenshots of said property in the appropriate ImageSearch folder.
***

## <u>`surround()`</u>
This function allows the user to wrap the highlighted text with whatever characters they want.
```c#
discord.surround( [char {, onFailSend := A_ThisHotkey}] )
```
#### *char*
Type: *String*
> This parameter is the desired character(s) to wrap the text with.
>> ##### This parameter can be no more than 2 characters long.
>
>> If the passed `char` variable is 2 characters long, the first character will be appended at the beginning of the highlighted text & the second character will be appended to the end of the highlighted text.
>
>> If the passed `char` variable is 2 characters long & you aren't highlighting anything OR it fails to wait for data, this function will attempt to highlight the chat window and send the hotkey that activated the function (by default).

#### *onFailSend*
Type: *String*
> This parameter is the desired character you wish to be sent when `char` is 2 characters long and you aren't highlighting any text.

<u>Example #1</u>
```autoit
text := "This text is highlighted"
; ` is an escape character in ahk and needs to be put twice to pass it as a variable
`::discord.surround("``") ;becomes "`This text is highlighted`"
```
<u>Example #2</u>
```autoit
text := "This text is highlighted"
(::
)::discord.surround("()") ;becomes "(This text is highlighted)"
```
***

## <u>`DMs()`</u>
This function clicks the logo button in discord to access your friends/messages.