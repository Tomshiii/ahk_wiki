Sometimes during editing in `Premiere Pro`, if you hit a few hotkeys at the exact right moment, Premiere can end up in a pseudo `fullerscreen` mode, where you lose access to the window controls and all of your coordinates get messed up. This is of course, detrimental to a lot of the functions/macros used across these scripts.

This script aims to rectify that rare scenario. It does this by starting a timer once an adobe program is open that constantly checks the state of the window - even though you already had the window fullscreened, and this pseudo mode looks even more fullscreen, ahk actually detects it as not being maximised.

So if this script notices that the window isn't currently maximised, it will wait until you haven't touched the keyboard for `1.25s`, then it will restore the window to it's proper state.