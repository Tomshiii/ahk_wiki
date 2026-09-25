The idea to do this was thought up by [TaranVH](https://github.com/TaranVH/2nd-keyboard) a previous editor for LTT.
***
To paraphrase Taran;

> In just about any Windows application, pressing (and releasing!) the <kbd>alt</kbd> key will highlight the menu bar in a special way, where pressing a letter key immediately after, (Like <kbd>f</kbd>) will result in the menu being opened. Further keystrokes will bring you even deeper into the menu. This is called "menu acceleration."

> Because this system allows you to completely release the <kbd>alt</kbd> key before pressing the next keystrokes, it means that <kbd>alt</kbd> is not really a modifier key... it's an obligatory STICKY KEY

> So, in applications that treat the <kbd>alt</kbd> key as a modifier, like Premiere, you sometimes end up activating the menus when you don't want to! (And there's no reason to use menu acceleration anyway, since Premiere already allows you to bind those actions to custom shortcuts.)

> I noticed that the `File` menu only appears to become activated on the key-up event. However, functionally, it actually activates on the key <kbd>DOWN</kbd> event. Therefore, attempting to block this using `LAlt up::[insert code here]` will never work.

> I also noticed that if I pressed down <kbd>LAlt</kbd>, held it, and then pressed and released <kbd>F12</kbd>, that when I released <kbd>LAlt</kbd>. NOTHING HAPPENED. And, when I then pressed <kbd>f</kbd>, NOTHING CONTINUED TO HAPPEN. Brilliant.

> And it works with any keystroke, not just F12. so, to nullify the menu acceleration, we have to pair <kbd>alt</kbd> with another keystroke. but which key can we sacrifice? IT can't be used for anything else. Some people would think to use <kbd>F13</kbd> through <kbd>F24</kbd>. Those poeple are wrong.

> <kbd>F24</kbd> is just the name that we give to the scan code 76, also known as <kbd>SC076</kbd>. But the scan codes go much higher than this.

So essentially this script is disabling menu accelaration by sending off a scan code keystroke to more or less nullify the alt keystroke.