# PremiereRemote
[PremiereRemote](https://github.com/sebinside/PremiereRemote) is a tool developed by [sebinside](https://github.com/sebinside) that gives the user the ability to excecute custom Premiere CEP-based functionality from outside of Premiere. This is achieved via a local webserver and custom extension panel within Premiere. We can then excecute our custom code using AHK and a local http request.

This tool offers multiple advantages for my repo, such as;  
- More directly telling Premiere to `save` resulting in less issues
- Directly change clip properties like `zoom`, `x/y`, `anchor point`, etc. Meaning less keystrokes needing to be sent
- Directly receive the current project path

> [!Caution]
> [NodeJS](https://nodejs.org/) is required before any further steps can be taken. I do not offer any automation to step through this process as it can be a little involved depending on how you choose to install it.

### Installation
You may either follow the installation steps listed in the github repo itself or run the `..\Support Files\Release Assets\Install Packages\installPremRemote.ahk` file within this repo.

Then as long as you have the PremiereRemote extension window open within Premiere, you're set!

> [!Tip]
> If following the installation instructions on the [PremiereRemote](https://github.com/sebinside/PremiereRemote) github page, be aware that the instructions relating to adding the necessary `regedit` string to run unsigned extensions was made for a prior version of CEP (version 11), and since then adobe has moved to higer versions (version 12 with Premiere v25.0, etc). You can run `..\Streamdeck AHK\PremiereRemote\enable unsigned extensions.ahk` in this repo to ensure the correct values are added.

> [!Note]
> If you ever change any of the custom code found in the `A_AppData \Adobe\CEP\extensions\PremiereRemote\host\src\` folder, you will need to run `..\Streamdeck AHK\PremiereRemote\resetNPM.ahk` and then close/reopen the PremiereRemote extension window within Premiere for changes to take effect.  
> All information regarding this is detailed on the `PremiereRemote` github page

The custom code I use for this repo is kept in the `..\Backups\Adobe Backups\Premiere\PremiereRemote\` folder.
> [!Warning]
> It should be noted however that changing the files in the above directory will yield no effect, they must be adjusted in the `A_AppData \Adobe\CEP\extensions\PremiereRemote\host\src\` folder, then the `resetNPM.ahk` script must be run and `PremiereRemote` panel must be reopened.

### Using Custom Code
Any of our custom functions in the `index.tsx` file can then be called using either the basic `Run()` command or my custom `cmd.Run()`/`cmd.Result()` command.  
Example:
```ts
// index.tsx
saveProj: function () {
    app.project.save();
}
```

```ahk
;// directly call function
Run('curl "http://localhost:8081/saveProj?"',, "Hide")

;// call using my function
prem.__remoteFunc("saveProj")

;// an example with a return value
entirePath := prem.__remoteFunc("projPath", true)

;// an example with variables
this.__remoteFunc("setZoomOfCurrentClip",, "zoomLevel=" String(scale), "xPos=" String(x), "yPos=" String(y), "anchorX=" String(anchorX), "anchorY=" String(anchorY))
```
> [!Warning]
> I will always do my best to provide fallback code in scenarios where I use a PremiereRemote function, but as a precautionary warning; this fallback code may not be actively maintained and may, over time, slowly break or stop working.  
> If you ever encounter this scenario please do be sure to let me know by either submitting an `issue` on the github page, or by fixing the problem and submitting a pull request.
***

## Known Quirks
No system is perfect and as such doing things this way introduces some little annoyances from time to time;
- Resetting or changing the current workspace may cause the PremiereRemote server to stop working. They will need to close the extension window within Premiere and reopen it
    - This issue can sometimes extend so far as needing the entire npm server to be reloaded. I have scripts in `..\Streamdeck AHK\PremiereRemote` to quickly reset both of these
- Some files `PremiereRemote` relies on may get broken during various updates causing either it OR other extensions in Premiere to crash.
    - Run `..\Streamdeck AHK\PremiereRemote\checkInstalls.ahk` to check for any problem files, then run `resetNPM.ahk` to reload the server, then restart the extension within premiere