# Resolve
These functions may seem either less polished, less logical, or not as optimal as their Premiere counterparts - I don't use resolve, so I haven't had a lot of time to find edge cases, or to find problems that need solving. Think of these functions as a starting place for you to expand on and improve.  
A lot of these functions were created in a rush and as such throughout this wiki you may see me confused at a few things - I can only assume I did things for a reason (but more than likely it was just an initial silly decision that I never got around to fixing).

If you do find the time to improve any of these functions, feel free to try and `Pull Request` them back to the original repo for others to take advantage of!

All Resolve functions are contained within a class called `Resolve` and are called like: `resolve.func()`

These functions are only tested on specific versions of Davinci Resolve. Any version folders listed in `..\Support Files\ImageSearch\Resolve` are supported.
> *There is currently no way to change the version of Resolve my scripts use, but the version can be manually changed within `settings.ini`*
***

## <u>`resolve.scale()`</u>
This function allows you to quickly set the scale of a video
```c#
resolve.scale( [value, property {, plus := 0}] )
```
#### *value*
Type: *Number*
> This parameter is the number you want to type into the text field. *(ie. 100% in reslove requires a 1 here)*

#### *property*
Type: *String - Filename*
> The filename of the property itself - ie. `zoom` NOT `zoom.png` or `zoom2`. Will require screenshots of said property in the appropriate ImageSearch folder.

#### *plus*
Type: *Integer*
> This parameter is described as being - The pixel value you wish to add to the x value to grab the respective value you want to adjust.
> But in all 3 instances I used this in, in `Resolve_Example.ahk` I had this value at `60` so unsure if this variable is useful
***

## <u>`rfElse()`</u>
This function is a relic from the early days of me creating examples for Resolve and is described as - A function that gets nested in the resolve valuehold script.
```c#
; when called from within the class
this.rfElse( [data] )
```
#### *data*
Type: *Integer*
> This parameter is described as being - what the script is typing in the text box to reset its value
***

## <u>`resolve.valhold()`</u>
This function will warp to the desired value of the current track (`scale`, `x/y`, `rotation`, etc), then click and hold it so the user can drag to increase/decrease the value. Tapping the button you assign this function will reset the desired value.
```c#
resolve.valhold( [property, plus, rfelseval] )
```
#### *property*
Type: *String - Filename*
> The filename of the property itself - ie. `scale` NOT `scale.png` or `scale2`. Will require screenshots of said property in the appropriate ImageSearch folder.

#### *plus*
Type: *Integer*
> This parameter is described as being - The pixel value you wish to add to the x value to grab the respective value you want to adjust.
> This parameter could probably be replaced with an alternative method, ie. A pixelsearch/more robust imagesearch

#### *rfelseval*
Type: *Integer*
> This parameter is the value you wish to pass into `rfesle()`
***

## <u>`resolve.Effect()`</u>
This function will apply an effect to the clip you're hovering over.
```c#
resolve.Effect( [folder, effect] )
```
#### *folder*
Type: *String - Filename*
> The filename of the drop down sidebar option itself (in the effects window) - ie. `openfx` NOT `openfx.png` or `openfx2`. Will require screenshots of said property in the appropriate ImageSearch folder.

#### *effect*
Type: *String*
> This parameter is the name of the effect you want this function to type into the search box

This function also requires additional images for a large amount of checks to ensure the proper windows are open.

This function will, in order;

1. Check to see if the effects window is open on the left side of the screen
2. Check to make sure the effects sidebar is expanded
3. Ensure you're clicked on the appropriate drop down
4. Open or close/reopen the search bar
5. Search for your effect of choice, then drag back to the click you were hovering over originally
***

## <u>`resolve.flip()`</u>
This function will search for and press the horizontal/vertical flip button within Resolve
```c#
resolve.flip( [button] )
```
#### *button*
Type: *String - Filename*
> The filename of the direction itself (horizontal/veritcal) - ie. `horizontal` NOT `horizontal.png` or `horizontal2`. Will require screenshots of said property in the appropriate ImageSearch folder.
***

## <u>`resolve.gain()`</u>
This function allows you to adjust the gain of the selected clip within Resolve similar to my gain macros in premiere. You can't pull this off quite as fast as you can in premiere, but it's still pretty useful.
```c#
resolve.gain( [value] )
```
#### *value*
Type: *Number*
> This parameter is how much you want the gain to be adjusted by.