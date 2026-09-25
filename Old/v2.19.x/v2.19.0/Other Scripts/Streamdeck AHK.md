Not every macro benefits from being linked to a button on a keyboard, whether it be because of the frequency at which you need said macro not being very high, or if you don't need to see `Key Events`. A streamdeck is a tool often used by streamers or just anyone looking to optimise whatever workflow they're in and can be quite a useful tool to run Autohotkey scripts.

In the case of video editing it allows us to have some useful scripts that only pop up every once in a while, still within arms reach.

For me personally, I put less frequently used macros here because I use a secondary keyboard with `QMK.ahk`. If you don't have a secondary keyboard, a streamdeck is a good alternative to put any scripts that don't require seeing either; `Key {Up/Down}` events, or the activation key being held.

> [!Tip]
> All scripts show their dependencies at the top of the script, all of which can be found in the `..\lib\` folder.

## Support Files
Within `..\Support Files\Streamdeck Files\` you will find a `options.ini` file where you can set a few directory locations used throughout some streamdeck scripts. This file is placed in this directory to allow the user to more easily replace the entire `Streamdeck AHK` folder without worrying about custom directories being wiped.
***
## Shared Resources
Some scripts require information that other scripts have already gathered, ie. `Timeline` coordinates in `Adobe Premiere` - but as streamdeck scripts are designed to fire and instantly close this would generally mean that each instance of that script would be required to reretrieve all of that information anytime it is used. Because of this, my scripts take advantage of my `CLSID_Objs {` class alongside the `Core Functionality.ahk` script to share objects with each other, allowing seemless information sharing without needing to waste time regathering information that has already been gathered.

***

## convert scripts
These scripts take advantage of `ffmpeg` to quickly convert files from one file format to another.
> [!Warning]
> If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

Go to any folder that contains the files you wish to convert, then simply run the desired script. It will automatically grab the path of the current explorer window then send the desired command to cmd. It will then send an `ffmpeg` command to convert **all** files of the desired file format to the requested file format.

> *This function may recurse further into folders searching for files to convert.*

- `convert mkv2mp3.ahk`  => converts all `.mkv` files to `.mp3`
- `convert mkv2mp4.ahk`  => converts all `.mkv` files to `.mp4`
- `convert mov2mp4.ahk`  => converts all `.mov` files to `.mp4`
- `convert mp42mp3.ahk`  => converts all `.mp4` files to `.mp3`
- `convert webm2mp3.ahk` => converts all `.webm` files to `.mp3`
- `convert wavOrmp3.ahk` => converts the filepath copied to the clipboard between `.mp3` and `.wav`
***

## hCrop scripts
These scripts take advantage of [`ffmpeg`](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) and offer a variaty of functionality centered around the need to split a video in half along the horizontal axis. These scripts extend off the `encodeGUI {` to offer that basic functionality while also offering some additional options if necessary.
> [!Warning]
> If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

- `hCrop CamAll.ahk`      => offers the user the ability to select which half of every video in the chosen directory they wish to reencode to a new file
- `hCrop CamSingle.ahk`   => offers the user the ability to select which half of the video selected they wish to reencode to a new file
- `hCrop loop.ahk`        => automatically splits every `.mkv` video file in the active directory and reencodes them to two new files
- `hCrop SplitSingle.ahk` => offers the user the ability to split and reencode the selected video to two new files
***

## vCrop scripts
These scripts take advantage of [`ffmpeg`](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) and offer a variaty of functionality centered around the need to split a video in half along the vertical axis. These scripts extend off the `encodeGUI {` to offer that basic functionality while also offering some additional options if necessary.
> [!Warning]
> If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

- `vCrop CamAll.ahk`      => offers the user the ability to select which half of every video in the chosen directory they wish to reencode to a new file
- `vCrop CamSingle.ahk`   => offers the user the ability to select which half of the video selected they wish to reencode to a new file
- `vCrop loop.ahk`        => automatically splits every `.mkv` video file in the active directory and reencodes them to two new files
- `vCrop SplitSingle.ahk` => offers the user the ability to split and reencode the selected video to two new files
***

## Extract Audio scripts
These scripts take advantage of `ffmpeg` to extract all audio streams from files.
> [!Warning]
> If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

- `extractSingle.ahk` => extracts all audio streams from the individually selected file
- `extractAll.ahk`    => extracts all audio streams from all `.mp4`/`.mkv` files in the selected directory
> [!Important]
> `extractAll.ahk` will initially check to see if [Bulk Audio Extract Tool](https://github.com/TimeTravelPenguin/BulkAudioExtractTool) is installed before proceeding.  
> If it is, it will pipe the selected directory to that tool, if it isn't it will simply run the required ffmpeg commands manually.  
> The benefits of this tool are;
> - Offers the user more options/control if they intend on changing the command sent to the command line
> - Provides visual progress bars to show how long the extraction process has left.
***

## Reencode Scripts
These scripts take advantage of `ffmpeg` to reencoded a selected file (or directory) to a desired codec.
> [!Warning]
> If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

- `reencode_h26x.ahk`       => reencodes the selected file to `h264`/`h264` at the selected quality
- `reencode_prores.ahk`     => reencodes the selected file to `prores` at the selected quality
- `reencode_prores_all.ahk` => reencodes the selected directory to `prores` at the selected quality
***

## PremiereRemote Scripts
These scripts are designed to make a few interactions with [PremiereRemote](https://github.com/Tomshiii/ahk/wiki/PremiereRemote) quicker and easier.
> [!Warning]
> If you do **not** have NodeJS & PremiereRemote installed, some of these may (obviously) fail spectacularly.

- `openRemoteDir.ahk`  => opens the `A_AppData \Adobe\CEP\extensions\PremiereRemote\` directory
- `openPremRemote.ahk` => quickly reopen the `PremiereRemote` extenstion within premiere.
    - **note: custom amount of "{Down}" will need to be set by the user*
- `resetNPM.ahk`       => reruns the `npm run build` command in the `A_AppData \Adobe\CEP\extensions\PremiereRemote\host\` directory
- `checkInstalls.ahk`  => reruns the `npm i` command in the `A_AppData \Adobe\CEP\extensions\PremiereRemote\` `client` & `host` directories to check for any files that need fixing
                       => useful to run this script if you're experiencing PremiereRemote/other extensions crashing
***
## Lock Scripts
These scripts are designed to trigger `prem.excalibur.lockTracks()`  
> [!Caution]
> These scripts require the proper shortcuts to be set within `KSA` and require the user to have [`Excalibur`](https://knightsoftheeditingtable.com/excalibur) installed.

These scripts are designed to pop up the corresponding `Excalibur` window to toggle the desired track. The user may then input the track numbers they wish to toggle.  
As excalibur is designed to accept a comma separated list of tracks, a few numpad keys will offer other functions to the user;
- <kbd>Space</kbd> will input <kbd>,</kbd>
- <kbd>Numpad0</kbd> will input <kbd>,</kbd>
- <kbd>NumpadSub</kbd> will input <kbd>BackSpace</kbd>

In addition to the above, if the user instead presses <kbd>NumpadDiv</kbd> they will be able to select a range of numbers that will be automatically toggled. The script with wait for the user to press two number keys per selection or it will wait for the user to press <kbd>NumpadEnter</kbd> before proceeding.
***

## Update Scripts
These scripts are a collection of scripts to quickly update any [`chocolatey`](https://github.com/Tomshiii/ahk/wiki/Install-Package-Manager) repos using the commandline.
***