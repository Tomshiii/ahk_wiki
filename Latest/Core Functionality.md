`Core Functionality.ahk` is a persistent background script that provides shared object access across multiple AutoHotkey scripts using Windows COM registration. This enables scripts to communicate with common class instances (like `prem`, `UserSettings`, etc.) without needing to recreate them in each script.

This is achieved via the `ObjRegisterActive()` function and the `CLSID_Objs` helper class, which registers objects with unique CLSIDs (Class Identifiers) that other scripts can access.

This tool offers multiple advantages for my repo, such as:
- Centralized settings and state management
- Simplified cross-script communication
- Thread-safe access to shared objects via mutex locking

> [!Caution]
> `Core Functionality.ahk` must be running before any script that attempts to access its registered objects. Failure to do so will result in errors.

### Using Registered Objects
Any script can access registered objects using the `CLSID_Objs` helper class. This class provides convenient methods to load or clone objects from `Core Functionality.ahk`.

Examples:
```ahk
; Load a reference to the premiere object
premiere := CLSID_Objs.load("prem")

; Load UserSettings
settings := CLSID_Objs.load("UserSettings")

; Clone an object (creates independent copy)
mySettings := CLSID_Objs.clone("UserSettings")

; Load using raw CLSID
uiaCheck := CLSID_Objs.load("{DCEE88EC-9327-44CF-9D2A-5BC47C624E0E}", false)
```

> [!Caution]
> When using `CLSID_Objs.load()`, you're accessing a shared reference to the object. Changes made to the object will affect all scripts using it. If you need an independent copy, use `CLSID_Objs.clone()` instead.

> [!Warning]
> The `CLSID_Objs` class will automatically throw an error if `Core Functionality.ahk` is not running when any script tries to use it. However if a script has already loaded a connection to the object, then `Core Functionality.ahk` is closed, any further attempts to interact with the object will result in a memory error.

***

## Known Quirks
No system is perfect and as such doing things this way introduces some little annoyances from time to time:
- **`Core Functionality.ahk` must be launched first** - Any script attempting to access registered objects before `Core Functionality.ahk` is running will automatically exit
- **`Core Functionality.ahk` must be closed last** - Closing `Core Functionality.ahk` while other scripts are running will cause those scripts to throw errors when attempting to access registered objects
- **Changes require script restart** - If you modify which objects are registered in `Core Functionality.ahk`, you must restart the script (and potentially dependent scripts) for changes to take effect
- **Mutex timeout errors** - When using `CLSID_Objs.load()`, if the mutex cannot be acquired within the timeout period (default 5000ms), a warning will be thrown
    - This typically indicates another script is holding the lock for an extended period

### Thread Safety with Mutexes
`CLSID_Objs.load()` uses Windows mutexes to provide thread-safe access to shared objects. This prevents data corruption when multiple scripts attempt to modify the same object simultaneously. The mutex is automatically released when the operation completes or if an error occurs.