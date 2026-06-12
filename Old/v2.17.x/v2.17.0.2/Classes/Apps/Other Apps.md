Within the `..\lib\Classes\Apps\` directory is a collection of any classes designed specifically for certain applications. All (or in case I ever change it, *most*) classes are called like: `class.func()`
***
### Table of Contents:
* [Slack](#class-slack-)
***

# <u>`class Slack {`</u>
This class contains functions designed to interact with Slack.

## <u>`Slack.unread()`</u>
A function designed to quickly click on any unread notifications.
```c#
Slack.unread( [which] )
```
#### *which*
Type: *String*
> This parameter decides which type of notification you wish to action. Either pass `"dm"` or an empty string.
***

## <u>`Slack.button()`</u>
A function designed to quickly access many features that often require a little fiddling to reach.
```c#
Slack.button( [button {, replyInThread := false}] )
```
#### *button*
Type: *String*
> This parameter is the desired button name you wish to click. Supported buttons are; `reaction`, `reply`, `edit`, `delete`

#### *replyInThread*
Type: *Boolean*
> Determines whether `reply` will also enable the `Also send to...` checkbox when replying in a thread. Defaults to `false`
***