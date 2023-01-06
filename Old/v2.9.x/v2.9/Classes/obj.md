# <u>class obj {</u>
This class is a collection of wrapper functions designed to take normal AutoHotkey functions and return their VarRefs as object parameters instead.
**
A lot of functions in this class are likely to end up with the same parameters so instead of copying them over and over I'll define them here;
#### *winTitle*
Type: *String*
> The winTitle you wish to get the position of, this will default to the active window.

#### *winText*
Type: *String*
> The winText you wish to get the position of.

#### *exTitle*
Type: *String*
> The winTitle of any windows you wish to exclude.

#### *exTitle*
Type: *String*
> The winText of any windows you wish to exclude.

***
## <u>`SplitPath()`</u>
This function turns the inbuilt function `SplitPath` into a function that returns an object.
```
obj.SplitPath( [Path] )
```
#### *Path*
Type: *String*
> This parameter is the input path that will be split.

### Return Value
Type: *Object*
```autoit
script := obj.SplitPath("E:\Github\ahk\My Scripts.ahk")
script.Name       ; My Scripts.ahk
script.Dir        ; E:\Github\ahk
script.Ext        ; ahk
script.NameNoExt  ; My Scripts
script.Drive      ; E:
```
***

## <u>`MousePos()`</u>
This function acts as a wrapper for `MouseGetPos()` to return its VarRefs as an object instead.
```
obj.MousePos( [{flags}] )
```
#### *flags*
Type: *String*
> This parameter is to pass in normal flag settings for MouseGetPos. This can be omitted.

### Return Value
Type: *Object*
```autoit
`mouse := getMousePos()`
`mouse.x`       ;passes back the mouse `x coordinate`
`mouse.y`       ;passes back the mouse `y coordinate`
`mouse.win`     ;passes back the `window` the mouse is hovering
`mouse.control` ;passes back the `control` the mouse is hovering
```
***

## <u>`WinPos()`</u>
This function acts as a wrapper for `WinGetPos()` to return its VarRefs as an object instead.
```
obj.WinPos( [{winTitle := "A", winText?, exTitle?, exText?}] )
```

### Return Value
Type: *Object*
```autoit
window := obj.WinPos()
window.x
window.y
window.width
window.height
```
***

## <u>`imgSrch()`</u>
This function acts as a wrapper for `checkImg()` which is a wrapper function for `ImageSearch`. It will verify if the requested file exists and return the x and y coordinates as an object if it does. If the target file doesn't exist or the image cannot be found, the function will return `false`.

By default this function will have the option "*2 " but can be overridden by placing a new option at the beginning of the `imgFile` parameter.
```
obj.imgSrch( [{x1 := 0, y1 := 0, x2 := A_ScreenWidth, y2 := A_ScreenHeight, imgFile}] )
```
#### *x1*, *y1*, *x2*, *y2*
Type: *Integer*
> The `ImageSearch` coordinates you wish to search within. These will default to the entire main screen.

#### *imgFile*
Type: *String*
> The filepath of the image you wish to search for. This variable also accepts all normal `ImageSearch` options if placed at the beginning of the parameter.

### Return Value
Type: *Object*
```autoit
img := obj.imgSrch(,,,, "image.png")
img.x
img.y
```
***

## <u>`ctrlPos()`</u>
This function is a wrapper function for `ControlGetPos()`.
```
obj.ctrlPos( [{ctrl, winTitle := "A", winText?, exTitle?, exText?}] )
```

#### *ctrl*
Type: *String, Integer or Object*
> This parameter is the desired control you wish to find the position of.
>
>> If this parameter is left unset, this function will attempt to use `ControlGetClassNN()` on the active window (by default unless other parameters are set).

### Return Value
Type: *Object*
```autoit
button := obj.ctrlPos()
button.x
button.y
button.width
button.height
button.ctrl     ;// a string containing the control
```